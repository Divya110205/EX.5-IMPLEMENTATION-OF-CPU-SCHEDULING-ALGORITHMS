# EX.5-IMPLEMENTATION-OF-CPU-SCHEDULING-ALGORITHMS

AIM: To implement First-Come-First-Serve (FCFS) Scheduling

ALGORITHM:


PROGRAM:
#include<stdio.h>
int main()
{
int c=0,i,n,bt[10],at[10],wt[10],ft[10];
int st[10],tat[10];
float awt=0,atat=0,rr[10];
printf("Enter the number of process : ");
scanf("%d",&n);
for(i=1;i<=n;i++)
{
printf("Enter the arrival time and burst time for the process %d : ",i);
scanf("%d %d",&at[i],&bt[i]);


}
for(i=1;i<=n;i++)
{
st[i]=c;
c=c+bt[i];
wt[i]=st[i]-at[i];
ft[i]=st[i]+bt[i];
tat[i]=wt[i]+bt[i];
rr[i]=tat[i]/bt[i];
}
for(i=1;i<=n;i++)
{
awt=awt+wt[i];
atat=atat+tat[i];
}
awt=awt/n;
atat=atat/n;
printf("\n\t\t CPU SCHEDULING\n\t\t ***************");
printf("\n\t\t FIRST COME FIRST SERVE\n\t\t **********************");
printf("\n--------------------------------------------------------------\n");
printf("proc\t at\t bt\t st\t ft\t wt\t tat\t rr\t\n");
printf("--------------------------------------------------------------");
for(i=1;i<=n;i++)
{
printf("\n %d\t %d\t %d\t %d\t %d\t %d\t %d\t%5.2f",i,at[i],bt[i],st[i],ft[i],wt[i],tat[i],rr[i]);
}
printf("\n--------------------------------------------------------------");
printf("\n Average waiting time is %5.2f\n average tat is %5.2f",awt,atat); }

OUTPUT:


RESULT: First-Come-First-Serve Scheduling is implemented successfully.


AIM: To implement Shortest Job First (SJF) Preemptive Scheduling

ALGORITHM:


PROGRAM:
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
printf("\nEnter the process,arrival time and burst time : \n");
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

OUTPUT:


RESULT: Shortest Job First (SJF) preemptive scheduling is implemented successfully.


AIM: To implement Shortest Job First (SJF) Non-Preemptive Scheduling

ALGORITHM:


PROGRAM:
#include <stdio.h>

int main() {
    int n;
    printf("Enter the number of processes: ");
    scanf("%d", &n);

    int process_id[10];
    int arrival_time[10];
    int burst_time[10];
    int completion_time[10];
    int waiting_time[10];
    int turnaround_time[10];

    // Input process information
    for (int i = 0; i < n; i++) {
        process_id[i] = i + 1;
        printf("Enter arrival time for process %d: ", process_id[i]);
        scanf("%d", &arrival_time[i]);
        printf("Enter burst time for process %d: ", process_id[i]);
        scanf("%d", &burst_time[i]);
    }

    // Perform SJF Non-Preemptive Scheduling
    for (int i = 0; i < n - 1; i++) {
        for (int j = 0; j < n - i - 1; j++) {
            if (arrival_time[j] > arrival_time[j + 1]) {
                // Swap arrival_time
                int temp = arrival_time[j];
                arrival_time[j] = arrival_time[j + 1];
                arrival_time[j + 1] = temp;

                // Swap burst_time
                temp = burst_time[j];
                burst_time[j] = burst_time[j + 1];
                burst_time[j + 1] = temp;

                // Swap process_id
                temp = process_id[j];
                process_id[j] = process_id[j + 1];
                process_id[j + 1] = temp;
            }
        }
    }

    int time = 0; // Current time

    for (int i = 0; i < n; i++) {
        // Find the process with the smallest burst time that has arrived
        int shortest_job = -1;
        int shortest_time = 10000; // A large initial value

        for (int j = 0; j < n; j++) {
            if (arrival_time[j] <= time && burst_time[j] < shortest_time && burst_time[j] != -1) {
                shortest_job = j;
                shortest_time = burst_time[j];
            }
        }

        if (shortest_job == -1) {
            // No process is available to run at this time
            time++;
        } else {
            // Execute the selected process
            completion_time[shortest_job] = time + burst_time[shortest_job];
            waiting_time[shortest_job] = completion_time[shortest_job] - arrival_time[shortest_job] - burst_time[shortest_job];
            turnaround_time[shortest_job] = waiting_time[shortest_job] + burst_time[shortest_job];
            time = completion_time[shortest_job];
            burst_time[shortest_job] = -1; // Mark the process as completed
        }
    }

    // Display the scheduling information
    printf("\n-----------------------------------\n");
    printf("Process\tAT\tBT\tCT\tWT\tTAT\n");
    printf("-----------------------------------\n");
    for (int i = 0; i < n; i++) {
        printf("P%d\t%d\t%d\t%d\t%d\t%d\n", process_id[i], arrival_time[i],
               burst_time[i], completion_time[i], waiting_time[i],
               turnaround_time[i]);
    }
    printf("-----------------------------------\n");

    return 0;
}

OUTPUT:


RESULT: Shortest Job First (SJF) Non-preemptive scheduling is implemented successfully.

AIM: To implement Round Robin (RR) Scheduling

ALGORITHM:


PROGRAM:

#include<stdio.h>
int main()
{
int n,i,pro[10],at[10],srt[10],st[10],ft[10],wt[10],tt[10];
static int iscompleted[10],isstarted[10],isentered[10];
int queue[10],f,r,count,tq,j,timer,totalsrt,tempsrt[10];
float rr[10],awt=0,atat=0;
printf("\n\t ROUND ROBIN");
printf("\nEnter the no. of process : ");
scanf("%d",&n);

printf("\nEnter the value for Time Quantum : ");
scanf("%d",&tq);
printf("\nEnter the process id for n process : \n");
for(i=0;i<n;i++)
{
scanf("%d",&pro[i]);
}
printf("\nEnter the arrival time for n process : \n");
for(i=0;i<n;i++)
{
scanf("%d",&at[i]);
}
printf("\nEnter the Burst time for n process : \n");
for(i=0;i<n;i++)
{
scanf("%d",&srt[i]);
}
totalsrt=0;
for(i=0;i<n;i++)
{
totalsrt=totalsrt+srt[i];
tempsrt[i]=srt[i];
}
f=0;
r=-1;
count=0;
timer=0;
for(i=0;i<n;i++)
{
if(at[i]==0)
{
r=(r+1)%n;
queue[r]=i;
isentered[i]=1;
count=count+1;
}
}
while(timer<totalsrt)
{
j=queue[f];
f=(f+1)%n;
if(isstarted[j]==0)
{
st[j]=timer;
wt[j]=st[j]-at[j];
isstarted[j]=1;
}
if(srt[j]>=tq)

{
timer=timer+tq;
srt[j]=srt[j]-tq;
}
else
{
timer=timer+srt[j];
srt[j]=srt[j]-srt[j];
}
if(srt[j]==0)
{
ft[j]=timer;
wt[j]=wt[j]+(ft[j]-(st[j]+tempsrt[j]));
tt[j]=wt[j]+tempsrt[j];
rr[j]=(float)tt[j]/tempsrt[j];
iscompleted[j]=1;
}
for(i=0;i<n&&count<n;i++)
{
if(at[i]<=timer&&isentered[i]==0)
{
r=(r+1)%n;
queue[r]=i;
isentered[i]=1;
count=count+1;
}
}
if(iscompleted[j]==0)
{
r=(r+1)%n;
queue[r]=j;
}
}
printf("\n\t CPU SCHEDULING\n\t **************");
printf("\n\t ROUND ROBIN\n\t ***********\n");
printf("------------------------------------------- \n");
printf("PRO AT BUT ST FT WT TT RR");
printf("\n------------------------------------------- \n");
for(i=0;i<n;i++)
{
printf("%3d %2d %2d",pro[i],at[i],tempsrt[i]);
printf(" %3d %3d %2d",st[i],ft[i],wt[i]);
printf(" %3d %4.2f\n",tt[i],rr[i]);
}
printf("------------------------------------------ ");

for(i=0;i<n;i++)
{
awt=awt+wt[i];
atat=atat+tt[i];
}
awt=awt/n;
atat=atat/n;
printf("\nAvg waiting time is %5.2f ",awt );
printf("\nAvg turn around time is %5.2f",atat);
}
OUTPUT:


RESULT: Round Robin (RR) Scheduling is implemented successfully.


AIM: To implement Priority Preemptive Scheduling

ALGORITHM:


PROGRAM:


OUTPUT:


RESULT: Priority Preemptive scheduling is implemented successfully.


AIM: To implement Priority Non-Preemptive Scheduling

ALGORITHM:


PROGRAM:


OUTPUT:


RESULT: Priority Non-preemptive scheduling is implemented successfully.

