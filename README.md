//# K1636-OS-Project-12-21-
//1.Write a program in C which reads input CPU bursts from a the first line of a text file named as CPU_BURST.txt. Validate the input numbers whether the numbers are positive intergers or not. Consider the numbers as CPU burst.If there are 5 positive integers in the first line of the text file then the program treat those argument as required CPU bust for P1, P2, P3, P4, and P5 process and calculate average waiting time and average turn around time. Consider used scheduling algorithm as SJF and same arrival time for all the processes.


//2. Design a scheduling program that is capable of scheduling many processes that comes in
at some time interval and are allocated the CPU not more than 10 time units. CPU must
schedule processes having short execution time first. CPU is idle for 3 time units and
does not entertain any process prior this time. Scheduler must maintain a queue that
keeps the order of execution of all the processes. Compute average waiting and
turnaround time.

#include<stdio.h>
 
void main()
{
    int burst_time,p[20],waiting_time[20],turnaroundtime[20],i,j,n,total=0,pos,temp;
    float avg_wt,avg_tat;
    printf("Enter number of process:");
    scanf("%d",&n);
 
    printf("\nEnter Burst Time:\n");
    for(i=0;i<n;i++)
    {
        printf("p%d:",i+1);
        scanf("%d",&burst_time[i]);
        p[i]=i+1;           //contains process number
    }
 
    //sorting burst time in ascending order using selection sort
    for(i=0;i<n;i++)
    {
        pos=i;
        for(j=i+1;j<n;j++)
        {
            if(burst_timt[j]<burst_time[pos])
                pos=j;
        }
 
        temp=bt[i];
        burst_time[i]=burst_time[pos];
        burst_time[pos]=temp;
 
        temp=p[i];
        p[i]=p[pos];
        p[pos]=temp;
    }
 
    waiting_time[0]=3;            //waiting time for first process will be 3time units
 
    //calculate waiting time
    for(i=1;i<n;i++)
    {
        Waiting_time[i]=0;
        for(j=0;j<i;j++)
            waiting_time[i]+=burst_time[j];
 
        total+=waiting_time[i];
    }
 
    avg_wt=(float)total/n;      //average waiting time
    total=0;
 
    printf("\nProcess\t    Burst Time    \tWaiting Time\tTurnaround Time");
    for(i=0;i<n;i++)
    {
        turnaroundtime[i]=burst_time[i]+waiting_time[i];     //calculate turnaround time
        total+=turnaroundtime[i];
        printf("\np%d\t\t  %d\t\t    %d\t\t\t%d",p[i],burst_time[i],waiting_time[i],turnaroundtime[i]);
    }
 
    avg_tat=(float)total/n;     //average turnaround time
    printf("\n\nAverage Waiting Time=%f",avg_wt);
    printf("\nAverage Turnaround Time=%f\n",avg_tat);
}
