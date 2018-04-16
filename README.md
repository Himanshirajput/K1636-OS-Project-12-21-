//# K1636-OS-Project-12-21-
//1.Write a program in C which reads input CPU bursts from a the first line of a text file named as CPU_BURST.txt. Validate the input numbers whether the numbers are positive intergers or not. Consider the numbers as CPU burst.If there are 5 positive integers in the first line of the text file then the program treat those argument as required CPU bust for P1, P2, P3, P4, and P5 process and calculate average waiting time and average turn around time. Consider used scheduling algorithm as SJF and same arrival time for all the processes.
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int main(){
FILE *fp = fopen("cpu_burst.txt", "r");
 int bt[20],p[20],wt[20],tat[20],i=0,j,n=5,total=0,pos,temp;
    float avg_wt,avg_tat;


 printf("\nReading CPU_BURST.txt File\n");
    //for(i=0;i<5;i++)
    while((getc(fp))!=EOF)
    {
        fscanf(fp, "%d", &bt[i]);
          if(bt[i]>0){
        p[i]=i+1;  i++;}         //contains process number
    }
    n=i;
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

    wt[0]=0;            //waiting time for first process will be zero

    //calculate waiting time
    for(i=1;i<n;i++)
    {
        wt[i]=0;
        for(j=0;j<i;j++)
            wt[i]+=bt[j];

        total+=wt[i];
    }

    avg_wt=(float)total/n;      //average waiting time
    total=0;

    printf("\nProcess\t    Burst Time    \tWaiting Time\tTurnaround Time");
    for(i=0;i<n;i++)
    {
        tat[i]=bt[i]+wt[i];     //calculate turnaround time
        total+=tat[i];
        printf("\np%d\t\t  %d\t\t    %d\t\t\t%d",p[i],bt[i],wt[i],tat[i]);
    }

    avg_tat=(float)total/n;     //average turnaround time
    printf("\n\nAverage Waiting Time=%f",avg_wt);
    printf("\nAverage Turnaround Time=%f\n",avg_tat);

    fclose(fp);
    return 0;
}


//2. Design a scheduling program that is capable of scheduling many processes that comes in
at some time interval and are allocated the CPU not more than 10 time units. CPU must
schedule processes having short execution time first. CPU is idle for 3 time units and
does not entertain any process prior this time. Scheduler must maintain a queue that
keeps the order of execution of all the processes. Compute average waiting and
turnaround time.

#include<stdio.h> 
int main() 
{ 
 
  int count,j,n;
  int time,remaining;
  int flag=0,time_quantum=10; 
  int waiting_time=0,turn_around_time=0,arrival_time[10],burst_time[10],rt[10]; 
  printf("\n\nEnter the Total number of Process:\t "); 
  scanf("%d",&n); 
  remaining=n; 
  for(count=0;count<n;count++) 
  { 
    printf("Enter Arrival Time and Burst Time for Process Process Number %d :",count+1); 
    scanf("%d",&arrival_time[count]); 
    scanf("%d",&burst_time[count]); 
    rt[count]=burst_time[count]; 
  } 
  printf("Enter Time Quantum:%d\t",time_quantum); 
 
  printf("\n\nProcess\t|Turnaround Time|Waiting Time\n\n"); 
  for(time=0,count=0;remaining!=0;) 
  { 
    if(rt[count]<=time_quantum && rt[count]>0) 
    { 
      time+=rt[count]; 
      rt[count]=0; 
      flag=1; 
    } 
    else if(rt[count]>0) 
    { 
      rt[count]-=time_quantum; 
      time+=time_quantum; 
    } 
    if(rt[count]==0 && flag==1) 
    { 
      remaining--; 
      printf("P[%d]\t|\t%d\t|\t%d\n",count+1,time-arrival_time[count],time-arrival_time[count]-burst_time[count]); 
      waiting_time+=time-arrival_time[count]-burst_time[count]; 
      turn_around_time+=time-arrival_time[count]; 
      flag=0; 
    } 
    if(count==n-1) 
      count=0; 
    else if(arrival_time[count+1]<=time) 
      count++; 
    else 
      count=0; 
  } 
  printf("\nAverage Waiting Time= %f\n",waiting_time*1.0/n); 
  printf("Avg Turnaround Time = %f",turn_around_time*1.0/n); 
  
  return 0; 
}


   
