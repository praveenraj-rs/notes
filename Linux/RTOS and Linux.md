## Fork
### Create Single Child from Parent
```c
#include <stdio.h>
#include <unistd.h>
#include <sys/wait.h>

int main() {
    pid_t pid = fork();

    if (pid == 0) {
        // CHILD PROCESS
        printf("Child: PID = %d\n", getpid());
        printf("Child: Parent PID = %d\n", getppid());
    } else {
        // PARENT PROCESS
        printf("Parent: PID = %d\n", getpid());
        printf("Parent: Waiting for child...\n");
        wait(NULL);   // parent waits for child to finish
        printf("Parent: Child finished.\n");
    }

    return 0;
}

```

```
Parent: PID = 4500
Parent: Waiting for child...
Child: PID = 4501
Child: Parent PID = 4500
Parent: Child finished.
```

### Creating Two Child from Single Parent

```c
#include <stdio.h>
#include <unistd.h>
#include <sys/wait.h>

int main() {
    pid_t c1, c2;

    // First child
    c1 = fork();

    if (c1 == 0) {
        printf("I am CHILD 1, PID = %d, Parent PID = %d\n", getpid(), getppid());
        return 0;  // child exits
    }

    // Only parent will reach this point
    // Second child
    c2 = fork();

    if (c2 == 0) {
        printf("I am CHILD 2, PID = %d, Parent PID = %d\n", getpid(), getppid());
        return 0;  // child exits
    }

    // Parent waits for both children
    wait(NULL);
    wait(NULL);

    printf("I am the PARENT, PID = %d. I created two children (%d, %d).\n",
           getpid(), c1, c2);

    return 0;
}
```

```yaml
I am CHILD 1, PID = 5010, Parent PID = 5009
I am CHILD 2, PID = 5011, Parent PID = 5009
I am the PARENT, PID = 5009. I created two children (5010, 5011).
```

## Pipe

### Creating Two Child with Single Pipe for Data Exchange
```c
#include <stdio.h>
#include <unistd.h>
#include <sys/wait.h>

int main(void)
{
	pid_t c1,c2;
	int fd[2];
	char buffer[100];

	pipe(fd);
	printf("fd[0]: %d\n",fd[0]);
	printf("fd[1]: %d\n\n",fd[1]);
	
	write(fd[1],"p Hello", 7);

	c1 = fork();
	if (c1==0)
	{
		printf("C1 Process: %d\n",(int)getpid());
		printf("Parent Process: %d\n\n",(int)getppid());
		read(fd[0], buffer, 100);
		printf("%s\n\n", buffer);
		write(fd[1],"c1 Hello",9);
		return 0;
	}

	c2 = fork();
	if (c2==0)
	{
		printf("C2 Process: %d\n",(int)getpid());
		printf("Parent Process: %d\n\n",(int)getppid());
		read(fd[0], buffer, 100);
		write(fd[1],"c2 Hello", 9);
		printf("%s\n\n", buffer);
		return 0;

	}

	wait(NULL);
	wait(NULL);

	printf("From Parent\n");
	printf("Parent Process: %d\n\n", (int)getpid());
	read(fd[0], buffer, 100);
	printf("%s\n\n", buffer);
	return 0;
}
```

## Thread
```c
#include <stdio.h>  
#include <pthread.h>  
  
void* addfunc(void *value)  
{  
    int n = *(int*)value;  
    for(int i = 1; i <= n; i++)  
    {  
        printf("%d ", i);  
    }  
    return NULL;  
}  
  
int main()  
{  
    pthread_t a;  
    int n = 10;  
    pthread_create(&a, NULL, addfunc, &n);  
    pthread_join(a, NULL);  
    return 0;  
}
```


## Shared Memory

### Shared Memory Write

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/shm.h>
#include <string.h>

int main()
{
    void *shared_mem;
    char buff[100];
    int shmid;

    shmid = shmget((key_t)1345, 1024, 0666|IPC_CREAT);
    printf("Key of shared memory: %d\n", shmid);
    
    shared_mem = shmat(shmid,NULL,0);
    read(0,buff,100);
    strcpy(shared_mem,buff);
    printf("stored: %s\n",(char *)shared_mem);

    return 0;
}
```

### Shared Memory Access

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/shm.h>
#include <string.h>

int main()
{
    void *shared_mem;
    char buff[100];
    int shmid;

//   shmid = shmget((key_t)2345, 1024, 0666|IPC_CREAT);
//   printf("Key of shared memory: %d\n", shmid);
    
    shmid = shmget((key_t)1345, 1024, 0666);
    shared_mem = shmat(shmid,NULL,0);
    // read(0,buff,100);
    // strcpy(shared_mem,buff);
    printf("stored: %s\n",(char *)shared_mem);

    return 0;
}
```