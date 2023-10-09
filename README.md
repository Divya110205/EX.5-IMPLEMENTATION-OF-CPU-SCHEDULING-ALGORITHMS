# EX.5-IMPLEMENTATION-OF-CPU-SCHEDULING-ALGORITHMS

### AIM: 

To implement First-Come-First-Serve (FCFS) Scheduling

### ALGORITHM:

1. Start the process 
2. Get the number of processes to be inserted 
3. Get the value for burst time of each process from the user 
4. Having allocated the burst time(bt) for individual processes , Start with the first process from its initial position let other process to be in queue 
5. Calculate the waiting time(wt) and turnaround time(tat) as 
6. Wt(pi) = wt(pi-1) + tat(pi-1) (i.e. wt of current process = wt of previous process + tat of previous process) 
7. tat(pi) = wt(pi) + bt(pi) (i.e. tat of current process = wt of current process + bt of current process) 
8. Calculate the total and average waiting time and turnaround time 
9. Display the values 
10. Stop the process

### PROGRAM:
```
#include<stdio.h> 
int main() 
{ 
int bt[20],p[20],wt[20],tat[20],i,j,n,total=0,pos,temp; float 
avg_wt,avg_tat; 
printf("Enter number of process: "); 
scanf("%d",&n); 
printf("\nEnter Burst Time:\n"); 
for(i=0;i<n;i++) 
{ 
printf("p % d : ",i+1); 
scanf("%d",&bt[i]); 
p[i]=i+1; //contains process number 
} 
wt[0]=0; //waiting time for first process will be zero 
//calculate waiting time 
for(i=1;i<n;i++) 
{ 
wt[i]=0; 
for(j=0;j<i;j++) 
wt[i]+=bt[j]; 
 
total+=wt[i]; 
} 
avg_wt=(float)total/n; //average waiting time 
total=0; 
printf("\nProcess\t Burst Time \tWaiting Time\tTurnaround Time"); 
for(i=0;i<n;i++) 
{ 
tat[i]=bt[i]+wt[i]; //calculate turnaround time 
total+=tat[i]; 
printf("\n\t p%d\t\t\t %d\t\t\t\t %d\t\t\t\t %d",p[i],bt[i],wt[i],tat[i]); 
} 
 
avg_tat=(float)total/n; //average turnaround time 
printf("\n\nAverage Waiting Time = %f",avg_wt); 
printf("\nAverage Turnaround Time = %f\n",avg_tat); 
}
```

### OUTPUT:
![1](https://github.com/Divya110205/EX.5-IMPLEMENTATION-OF-CPU-SCHEDULING-ALGORITHMS/assets/119404855/c89a3cfc-1644-4ae5-9b9a-8ed1e5541bfc)

### RESULT:
First-Come-First-Serve Scheduling is implemented successfully.

### AIM: 

To implement Shortest Job First (SJF) Preemptive Scheduling

### ALGORITHM:

Initialize variables and arrays to store process information, such as process ID (p), arrival time (at), burst time (bt), start time (st), finish time (ft), waiting time (wt), turnaround time (tt), response ratio (rr), and a flag to mark completed processes (iscompleted).Read the number of processes (n) from the user.Read the process ID, arrival time, and burst time for each process and store them in respective arrays (p, at, bt).Initialize variables, such as nextst (next start time) and counters.

Loop until all processes are completed: 

a. Find the process with the minimum burst time among the processes that have arrived and are not completed.

b. Update the start time, finish time, waiting time, and turnaround time for the selected process.

c. Calculate the response ratio (rr) for the selected process (rr = turnaround time / burst time).

d. Mark the selected process as completed.

e. Update the nextst to the finish time of the selected process.Calculate the average waiting time (AWT) and average turnaround time (ATT) by summing up the individual waiting times and turnaround times and dividing by the total number of processes,Display the process information, including process ID, arrival time, burst time, start time, finish time, waiting time, turnaround time, and response ratio.Display the average waiting time and average turnaround time.

### PROGRAM:
```
#include<stdio.h>
int main()
{
int i,n,p[10],st[10],at[10],bt[10],ft[10],wt[10],tt[10];
int nextst,count,minsrt,minpos;
static int  iscompleted[10];
float rr[10],awt=0,att=0;
printf("\n\t SHORTEST JOB FIRST\n\t ******************");
printf("\nEnter the no. of process to be executed : ");
scanf("%d",&n);
printf("\nEnter the process,arrival time and burst time:\n");
for(i=0;i<n;i++)
{
scanf("%d %d %d",&p[i],&at[i],&bt[i]);
}
nextst=0;
for(count=0;count<n;count++)
{
minsrt=100;
minpos=0;
for(i=0;i<n;i++)
{
if(at[i]<=nextst&&iscompleted[i]==0)
{
if(minsrt>bt[i])
{
minsrt=bt[i];
minpos=i;
}
}
}
i=minpos;
st[i]=nextst;
ft[i]=st[i]+bt[i];
wt[i]=st[i]-at[i];
tt[i]=wt[i]+bt[i];
rr[i]=tt[i]/bt[i];
iscompleted[i]=1;
nextst=ft[i];
}
printf("\n---------------------------------------");
printf("\nPRO AT bT ST FT WT TT RR \n");
printf("---------------------------------------\n");
for(i=0;i<n;i++)
{
printf("%3d %2d %2d",p[i],at[i],bt[i]);
printf(" %3d %2d %2d %2d %4.2f\n",st[i],ft[i],wt[i],tt[i],rr[i]);
}
printf("---------------------------------------");
for(i=0;i<n;i++)
{
awt=awt+wt[i];
att=att+tt[i];
}
awt=awt/n;
att=att/n;
printf("\nAverage waiting time is %5.2f",awt);
printf("\nAverage turn around time is %5.2f",att);
}
```

### OUTPUT:
![2](https://github.com/Divya110205/EX.5-IMPLEMENTATION-OF-CPU-SCHEDULING-ALGORITHMS/assets/119404855/f4519161-2138-44d8-a47f-7291f069eb71)

### RESULT: 

Shortest Job First (SJF) preemptive scheduling is implemented successfully.

### AIM:

To implement Shortest Job First (SJF) Non-Preemptive Scheduling

### ALGORITHM:

1. Start the process 
2. Get the number of processes to be inserted 
3. Sort the processes according to the burst tiine and allocate the one with shortest burst to execute first 
4. If two process have same burst length then FCFS scheduling algorithm is used 
5. Calculate the total and average waiting time and turn around time 
6. Display the values 
7. Stop the process
   
### PROGRAM:
```
#include<stdio.h> 
int main() 
{ 
int bt[20],p[20],wt[20],tat[20],i,j,n,total=0,pos,temp; float 
avg_wt,avg_tat; 
printf("Enter number of process : "); 
scanf("%d",&n); 
 
printf("\nEnter Burst Time:\n"); 
for(i=0;i<n;i++) 
{ 
printf("p%d : ",i+1); 
scanf("%d",&bt[i]); 
p[i]=i+1; //contains process number 
} 
//sorting burst time in ascending order using selection sort 
for(i=0;i<n;i++) 
{ 
pos=i; 
for(j=i+1;j<n;j++) 
{ 
if(bt[j]<bt[pos]) 
pos=j; 
} 
temp=bt[i]; 
bt[i]=bt[pos]; 
bt[pos]=temp; 
 
temp=p[i]; 
p[i]=p[pos]; 
p[pos]=temp; 
} 
wt[0]=0; //waiting time for first process will be zero 
 
//calculate waiting time 
for(i=1;i<n;i++) 
{ 
wt[i]=0; 
 
for(j=0;j<i;j++) 
wt[i]+=bt[j]; 
total+=wt[i]; 
} 
 
avg_wt=(float)total/n; //average waiting time 
total=0; 
 
printf("\n Process\t Burst Time \tWaiting Time\tTurnaround Time"); 
for(i=0;i<n;i++) 
{ 
tat[i]=bt[i]+wt[i]; //calculate turnaround time 
total+=tat[i]; 
printf("\n\t p%d\t\t %d\t\t\t\t %d\t\t\t%d",p[i],bt[i],wt[i],tat[i]); 
} 
 
avg_tat=(float)total/n; //average turnaround time 
printf("\n\nAverage Waiting Time = %f",avg_wt); 
printf("\nAverage Turnaround Time = %f\n",avg_tat); 
} 

```

### OUTPUT:
![3](https://github.com/Divya110205/EX.5-IMPLEMENTATION-OF-CPU-SCHEDULING-ALGORITHMS/assets/119404855/9ac1ebac-16e1-49fd-aa50-b9c0e197fcdf)

### RESULT: 

Shortest Job First (SJF) Non-preemptive scheduling is implemented successfully.

### AIM: 

To implement Round Robin (RR) Scheduling

### ALGORITHM:

1. Start the process 
2. Get the number of elements to be inserted 
3. Get the value for burst time for individual processes 
4. Get the value for time quantum 
5. Make the CPU scheduler go around the ready queue allocating CPU to each process for the time interval specified 
6. Make the CPU scheduler pick the first process and set time to interrupt after quantum. And after it's expiry dispatch the process 
7. If the process has burst time less than the time quantum then the process is released by the CPU 
8. If the process has burst time greater than time quantum then it is interrupted by the OS and the process is put to the tail of ready queue and the schedule selects next process from head of the queue 
9. Calculate the total and average waiting time and turnaround time 
10. Display the results

### PROGRAM:
```
#include<stdio.h> 
int main() 
{ 
int st[10],bt[10],wt[10],tat[10],n,tq; int 
i,count=0,swt=0,stat=0,temp,sq=0; 
float awt,atat; 
printf("enter the number of processes : "); 
scanf("%d",&n); 
printf("enter the burst time of each process\n"); 
for(i=0;i<n;i++) 
{ 
printf("p%d : ",i+1); 
scanf("%d",&bt[i]); 
st[i]=bt[i]; 
} 
printf("enter the time quantum : "); 
scanf("%d",&tq); 
while(1) 
{ 
for(i=0,count=0;i<n;i++) 
{ 
temp=tq; 
if(st[i]==0) 
{ 
count++; 
continue; 
} 
if(st[i]>tq) 
st[i]=st[i]-tq; 
else 
if(st[i]>=0) 
{ 
temp=st[i]; 
st[i]=0; 
} 
sq=sq+temp; 
tat[i]=sq; 
} 
if(n==count) 
break; 
} 
for(i=0;i<n;i++) 
{ 
wt[i]=tat[i]-bt[i]; 
swt=swt+wt[i]; 
stat=stat+tat[i]; 
} 
awt=(float)swt/n; 
atat=(float)stat/n; 
printf("process no\t burst time\t waiting time\t turnaround time\n"); 
for(i=0;i<n;i++) 
printf("\t\t %d\t\t %d\t\t\t %d\t\t\t %d\n",i+1,bt[i],wt[i],tat[i]); 
printf("avg wt time = %f \navg turn around time = %f ",awt,atat); 
} 
```

### OUTPUT:
![4](https://github.com/Divya110205/EX.5-IMPLEMENTATION-OF-CPU-SCHEDULING-ALGORITHMS/assets/119404855/e3e06e36-fe82-4d4d-aa35-d7ab3048fa13)

### RESULT:

Round Robin (RR) Scheduling is implemented successfully.

### AIM:

To implement Priority Preemptive Scheduling

### ALGORITHM:

Initialize the necessary variables and data structures, including the struct Process represent each process.Read the number of processes (n) from the userCreate an array of struct Process to store information for each process.Input process information for each process, including arrival time, burst time, and priority. Store this information in the struct Process array.Initialize the current time (time) to 0 and the completed process count (completed) to 0.Display the Gantt Chart header.

Enter the main scheduling loop that continues until all processes have completed execution (completed equals n).Inside the loop,find the highest priority process that has arrived (arrival_time <= time) and has remaining burst time (remaining_time > 0).If a process with the highest priority is found, execute it for 1 unit of time by decrementing its remaining_time and updating the Gantt Chart.If the process has completed its execution (remaining_time becomes 0), increment the completed process count.

If no process is available to run at the current time, display a message indicating that no process is running at that time.Repeat the loop until all processes are completed.Display the scheduling results, including the Gantt Chart, process ID, and execution time for each process.

### PROGRAM:
```
#include<stdio.h>
int main()
{
int i,n,pid[10],at[10],srt[10],st[10],ft[10],wt[10],tt[10],pri[10];
int timer,totalsrt,tempsrt[10],minsrt,minpos; static int iscompleted[10],isstarted[10];
float rr[10],awt,atat;
printf("\n\t PRIORITY PRE-EMPTIVE\n\t ********************");
printf("\nENTER THE NO.OF PROCESSES TO BE EXECUTED\n");
scanf("%d",&n);
printf("ENTER THE PROCESSES ID,ARRIVAL TIME,BURST TIME AND PRIORITY \n");
for(i=0;i<n;i++)
scanf("%d %d %d %d",&pid[i],&at[i],&srt[i],&pri[i]);

totalsrt=0;
for(i=0;i<n;i++)
{
totalsrt=totalsrt+srt[i];
tempsrt[i]=srt[i];
}
timer=0;
while(timer<totalsrt)
{
minsrt=100;
minpos=0;
for(i=0;i<n;i++)
{
if(at[i]<=timer && iscompleted[i]==0)
{
if(minsrt>pri[i])
{
minsrt=pri[i];
minpos=i;
}
}
}
i=minpos;
if(isstarted[i]==0)
{
st[i]=timer;
wt[i]=st[i]-at[i];
isstarted[i]=1;
}
srt[i]=srt[i]-1;
timer=timer+1;
if(srt[i]==0)
{
ft[i]=timer;
wt[i]=wt[i]+(ft[i]-(st[i]+tempsrt[i]));
tt[i]=wt[i]+tempsrt[i];
rr[i]=tt[i]/tempsrt[i];
iscompleted[i]=1;
}
}
printf("\n\t CPU SCHEDULING ALGORITHM\n\t ************************");
printf("\n\t PRIORITY PRE-EMPTIVE\n\t ********************");
printf("\n--------------------------------------------------");
printf("\nPID AT SRT ST FT WT TT RR PRIORITY\n");
printf("--------------------------------------------------\n");
for(i=0;i<n;i++)
{
printf("%2d %2d %2d ",pid[i],at[i],tempsrt[i]);
printf("%2d %2d %2d %2d %2.2f %3d\n",st[i],ft[i],wt[i],tt[i],rr[i],pri[i]);

}
printf("--------------------------------------------------\n");
for(i=0;i<n;i++)
{
awt=awt+wt[i];
atat=atat+tt[i];
}
atat=atat/n;
awt=awt/n;
printf("The average waiting time is: %5.2f\n",awt);
printf("The average turn around time is: %5.2f",atat);
}
```

### OUTPUT:
![5](https://github.com/Divya110205/EX.5-IMPLEMENTATION-OF-CPU-SCHEDULING-ALGORITHMS/assets/119404855/9784ed0f-97a3-4d33-86d9-06548a0d2c11)

### RESULT:

Priority Preemptive scheduling is implemented successfully.

### AIM: 

To implement Priority Non-Preemptive Scheduling

### ALGORITHM:
1. Start the process 
2. Get the number of processes to be inserted 
3. Get the corresponding priority of processes 
4. Sort the processes according to the priority and allocate the one with highest priority to execute first 
5. If two process have same priority then FCFS scheduling algorithm is used 
6. Calculate the total and average waiting time and turnaround time 
7. Display the values 
8. Stop the process
### PROGRAM:
```
#include<stdio.h> 
 
int main() 
{ 
int bt[20],p[20],wt[20],tat[20],pri[20],i,j,k,n,total=0,pos,temp; float 
avg_wt,avg_tat; 
printf("Enter number of process : "); 
scanf("%d",&n); 
 
printf("\nEnter Burst Time:\n"); 
for(i=0;i<n;i++) 
{ 
printf("p%d : ",i+1); 
scanf("%d",&bt[i]); 
p[i]=i+1; //contains process number 
} 
printf(" enter priority of the process \n"); 
for(i=0;i<n;i++) 
{ 
p[i] = i; 
//printf("Priority of Process"); 
printf("p%d : ",i+1); 
scanf("%d",&pri[i]); 
} 
for(i=0;i<n;i++) 
for(k=i+1;k<n;k++) 
if(pri[i] > pri[k]) 
{ 
temp=p[i]; 
p[i]=p[k]; 
p[k]=temp; 
 
temp=bt[i]; 
bt[i]=bt[k]; 
bt[k]=temp; 
temp=pri[i]; 
pri[i]=pri[k]; 
pri[k]=temp; 
 
} 
 
wt[0]=0; //waiting time for first process will be zero 
 
//calculate waiting time 
for(i=1;i<n;i++) 
{ 
wt[i]=0; 
for(j=0;j<i;j++) 
wt[i]+=bt[j]; 
 
total+=wt[i]; 
} 
avg_wt=(float)total/n; //average waiting time 
total=0; 
 
printf("\nProcess\t Burst Time \tPriority \tWaiting Time\tTurnaround Time"); 
for(i=0;i<n;i++) 
{ 
tat[i]=bt[i]+wt[i]; //calculate turnaround time 
total+=tat[i]; 
printf("\n\t p%d\t\t %d\t\t\t %d\t\t\t %d\t\t\t\t%d",p[i],bt[i],pri[i],wt[i],tat[i]); 
} 
 
avg_tat=(float)total/n; //average turnaround time 
printf("\n\nAverage Waiting Time = %f",avg_wt); 
printf("\nAverage Turnaround Time = %f\n",avg_tat); 
}
```
### OUTPUT:
![6](https://github.com/Divya110205/EX.5-IMPLEMENTATION-OF-CPU-SCHEDULING-ALGORITHMS/assets/119404855/049ac8a8-e2e5-4b46-90be-e3fe4af8d406)

### RESULT: 

Priority Non-preemptive scheduling is implemented successfully.

