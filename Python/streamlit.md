### Functions
```python
import streamlit as st

st.title("Super Simple Title")
st.header("This is a header")
st.subheader('Subheader')
st.markdown("This is _Markdown_")
st.caption("small text")
st.warning("Fill All Detials")
st.success("Successful")
st.balloons()
code_example="
def greet (name):
	print('hello', name)
"
st.code(code_example, Language="python")
st.divider()
```
### Tables
```python
import streamlit as st
import pandas as pd

# Title
st.title("Streamlit Elements Demo")

# Dataframe Section
st.subheader("Dataframe")

df = pd.DataFrame({
'Name': ['Alice', 'Bob', 'Charlie', 'David'],
'Age': [25, 32, 37, 45],
'Occupation': ['Engineer', 'Doctor', 'Artist', 'Chef']
})

dic={
'Name': ['Alice', 'Bob', 'Charlie', 'David'],
'Age': [25, 32, 37, 45],
'Occupation': ['Engineer', 'Doctor', 'Artist', 'Chef']
}
st.dataframe(df)
st.dataframe(dic)

# Data Editor Section (Editable dataframe)
st.subheader("Data Editor")

editable_df = st.data_editor(df)
print(editable_df)

edited_dic = st.data_editor(dic)
print(edited_dic)


# Static Table Section
st.subheader("Static Table")
st.table(df)
st.table(dic)

```
### Plots
```python
import streamlit as st
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

# Title
st.title("Streamlit Charts Demo")

# Generate sample data
chart_data = pd.DataFrame(
np.random.randn (20, 3),
columns=['A', 'B', 'C']
)

# Area Chart Section
st.subheader("Area Chart")
st.area_chart(chart_data)

# Bar Chart Section
st.subheader("Bar Chart")
st.bar_chart (chart_data)

# Line Chart Section
st.subheader("Line Chart")
st.line_chart(chart_data)

# Scatter Chart Section
st.subheader("Scatter Chart")
scatter_data=pd.DataFrame({
'x': np.random.randn(100),
'y': np.random.randn(100)
})
st.scatter_chart(scatter_data)

# Map Section (displaying random points on a map)
st.subheader("Map")
map_data = pd.DataFrame(
np.random.randn(100, 2) / [50, 50] + [37.76, -122.4], # Coordinates around SF
columns=['lat', 'lon']
)
st.map(map_data)

#Pyplot Section
st.subheader("Pyplot Chart")
fig, ax = plt.subplots()
ax.plot(chart_data['A'], label='A')
ax.plot(chart_data['B'], label='B')
ax.plot(chart_data['C'], label='C')
ax.set_title("Pyplot Line Chart")
ax.legend()
st.pyplot(fig)
```

### Counter

```python
import streamlit as st

if "counter" not in st.session_state:
    st.session_state.counter = 0
if st.button("Increment Counter"):
    st.session_state.counter += 1
    st.write(f"Counter incremented to {st.session_state.counter}")
if st.button("Reset"):
    st.session_state.counter = 0
    st.write(f"Counter value:{st.session_state.counter}")
```

### Layouts
```python
import streamlit as st

# Sidebar layout
st.sidebar.title("This is the Sidebar")
st.sidebar.write("You can place elements like sliders, buttons, and text here.")
sidebar_input = st.sidebar.text_input("Enter something in the sidebar")

# Tabs layout
tab1, tab2, tab3 = st.tabs(["Tab 1", "Tab 2", "Tab 3"])
with tab1:
    st.write("You are in Tab 1")
with tab2:
    st.write("You are in Tab 2")
with tab3:
    st.write("You are in Tab 3")

# Columns layout
col1, col2 = st.columns(2)
with col1:
    st.header("Column 1")
    st.write("Content for column 1")
with col2:
    st.header("Column 2")
    st.write("Content for column 2")

# Containers example
with st.container (border=True):
    st.write("This is inside a container.")
    st.write("You can think of containers as a grouping for elements.")
    st.write("Containers help manage sections of the page.")

# Empty placeholder
placeholder = st.empty()
placeholder.write("This is an empty placeholder, useful for dynamic content.")
if st.button("Update Placeholder"):
    placeholder.write("The content of this placeholder has been updated.")

# Expander
with st.expander ("Expand for more details"):
    st.write("This is additional information that is hidden by default.")
    st.write("You can use expanders to keep your interface cleaner.")
    # Popover (Tooltip)
    st.write("Hover over this button for a tooltip")
    st.button("Button with Tooltip", help="This is a tooltip or popover on hover.")

# Sidebar input handling
if sidebar_input:
    st.write(f"You entered in the sidebar: {sidebar_input}")
```

### Cache

```py
import streamlit as st
import time
@st.cache_data(ttl=60) # Cache this data for 60 seconds
def fetch_data():
    # Simulate a slow data-fetching process
    time.sleep(3) #Delays to mimic an API call
    return {"data": "This is cached data!"}

st.write("Fetching data...")
data=fetch_data()
st.write(data)
```

### Fragments

```python
import streamlit as st
st.title("My Awesome App")

@st.fragment()
def toggle_and_text():
    cols = st.columns(2)
    cols[0].toggle("Toggle")
    cols[1].text_area("Enter text")

@st.fragment()
def filter_and_file():
    new_cols=st.columns(5)
    new_cols[0].checkbox("Filter")
    new_cols[1].file_uploader("Upload image")
    new_cols[2].selectbox("Choose option", ["Option 1", "Option 2", "Option 3"])
    new_cols[3].slider("Select value", 0, 100, 50)
    new_cols[4].text_input("Enter text")
    return "hello world"

toggle_and_text()
cols=st.columns(2)
cols[0].selectbox("Select", [1, 2, 3], None)
cols[1].button("Update")
filter_and_file()
```

### Image Model

```python
import streamlit as st
import numpy as np
from PIL import Image

def preprocess_image(image):
    image = image.resize((224, 224))  # Resize to model's expected input size
    image = np.array(image) / 255.0  # Normalize pixel values
    image = np.expand_dims(image, axis=0)  # Add batch dimension
    return image

st.title("Skin Disease Identifier")
st.write("Upload an image of your skin condition to identify the disease.")

choosen_model=st.selectbox("Choose Model", ["Model 1", "Model 2", "Model 3", "Model 4"])
uploaded_file = st.file_uploader("Choose an image...", type=["jpg", "png", "jpeg"])

if uploaded_file is not None:
    image = Image.open(uploaded_file)
    st.image(image, caption="Uploaded Image", use_container_width=True)
    st.write("")
    
    if st.button("Submit"):
        processed_image = preprocess_image(image)
        st.success(f"Identified Skin Disease {choosen_model}")
        
```