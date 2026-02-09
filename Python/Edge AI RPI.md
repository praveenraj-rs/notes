```sh
sudo apt update && sudo apt upgrade -y
python3 -m venv --system-site-packages venv
source venv/bin/activate
pip install ultralytics ncnn
```

- YOLO - You Only Look Once
- COCO - Common Object in Context
### YOLO Ultralytics

```py
from ultralytics import YOLO
import cv2

# Load lightweight YOLO model
model = YOLO("yolov8n.pt")   # nano model

cap = cv2.VideoCapture(0)

if not cap.isOpened():
    print("Camera not opened")
    exit()

print("YOLO live detection started. Press q to exit.")

while True:
    ret, frame = cap.read()
    if not ret:
        break

    # Run YOLO inference
    results = model(frame, stream=True)

    for r in results:
        for box in r.boxes:
            cls_id = int(box.cls[0])
            conf = float(box.conf[0])
            label = model.names[cls_id]

            # Filter only required classes
            if label in ["person", "laptop", "mouse"]:
                x1, y1, x2, y2 = map(int, box.xyxy[0])
                text = f"{label} {conf:.2f}"

                cv2.rectangle(frame, (x1,y1), (x2,y2), (0,255,0), 2)
                cv2.putText(frame, text, (x1, y1-5),
                            cv2.FONT_HERSHEY_SIMPLEX, 0.6,
                            (0,255,0), 2)

    cv2.imshow("YOLO Live Detection", frame)

    if cv2.waitKey(1) & 0xFF == ord('q'):
        break

cap.release()
cv2.destroyAllWindows()
```