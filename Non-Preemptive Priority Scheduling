#include <iostream>
#include <algorithm> 
#include <iomanip>
#include <string.h> 
using namespace std;

int minimumArrivalTime;

struct process {
    int pid;
    int arrival_time;
    int burst_time;
    int priority;
    int start_time;
    int completion_time;
    int turnaround_time;
    int waiting_time;

};

int main() {

    int n;
    struct process p[100];
    struct process arr[100];
    float avg_turnaround_time = 0;
    float avg_waiting_time = 0;
    int total_turnaround_time = 0;
    int total_waiting_time = 0;
    int total_response_time = 0;
    int total_idle_time = 0;
    int is_completed[100];
    int totalCPUBurstTime = 0;
    memset(is_completed, 0, sizeof(is_completed));

    cout << setprecision(2) << fixed;

    cout << "Enter the number of processes: ";
    cin >> n;
    if (n <= 0) {
        cout << "error: enter one or more processes" << endl;
        return -1;
    }
    cout << endl;

    minimumArrivalTime = 2147483647;

    for (int i = 0; i < n; i++) {
        cout << "Enter arrival time of process " << i + 1 << ": ";
        cin >> p[i].arrival_time;
        cout << "Enter burst time of process " << i + 1 << ": ";
        cin >> p[i].burst_time;
        cout << "Enter priority of the process " << i + 1 << ": ";
        cin >> p[i].priority;
        p[i].pid = i + 1;
        cout << endl;
        totalCPUBurstTime += p[i].burst_time;
        if (minimumArrivalTime > p[i].arrival_time)
            minimumArrivalTime = p[i].arrival_time;
    }

    int current_time = 0;
    int completed = 0;
    int prev = 0;

    while (completed != n) {
        int idx = -1;
        int min = 99999999999999;
        for (int i = 0; i < n; i++) {
            if (p[i].arrival_time <= current_time && is_completed[i] == 0) {
                if (p[i].priority < min) {
                    min = p[i].priority;
                    idx = i;
                }
                if (p[i].priority == min) {
                    if (p[i].arrival_time < p[idx].arrival_time) {
                        min = p[i].priority;
                        idx = i;
                    }
                }
            }
        }
        if (idx != -1) {
            p[idx].start_time = current_time;
            p[idx].completion_time = p[idx].start_time + p[idx].burst_time;
            p[idx].turnaround_time = p[idx].completion_time - p[idx].arrival_time;
            p[idx].waiting_time = p[idx].turnaround_time - p[idx].burst_time;


            total_turnaround_time += p[idx].turnaround_time;
            total_waiting_time += p[idx].waiting_time;
            total_idle_time += p[idx].start_time - prev;

            is_completed[idx] = 1;
            completed++;
            current_time = p[idx].completion_time;
            prev = current_time;
        }
        else {
            current_time++;
        }

    }

    int min_arrival_time = 10000000;
    int max_completion_time = -1;
    for (int i = 0; i < n; i++) {
        min_arrival_time = min(min_arrival_time, p[i].arrival_time);
        max_completion_time = max(max_completion_time, p[i].completion_time);
    }

    avg_turnaround_time = (float)total_turnaround_time / n;
    avg_waiting_time = (float)total_waiting_time / n;

    for (int m = 0; m < n; m++) {
        arr[m] = p[m];
    }
    int min, i = 0 , j = 0;
    for (i = 0; i < n - 1; i++) {
        min = i;
        for ( j = i + 1; j < n; j++) {
            if (arr[j].start_time < arr[min].start_time) {
                min = j;
            }
        }
        swap(arr[i], arr[min]);
    }

    const int maxWidth = 100;
    int scalingFactor, counter, tempi, currentTime;
    printf("The gantt chart for the given processes is : \n\n");

    scalingFactor = maxWidth / totalCPUBurstTime;
    for (i = 0; i < scalingFactor * totalCPUBurstTime + 2 + n; i++)
    {
        printf("-");
    }
    printf("\n|");
    counter = 0, tempi = 0;
    for (i = 0; i < scalingFactor * totalCPUBurstTime; i++)
    {
        if (i == p[counter].burst_time * scalingFactor + tempi)
        {
            counter++;
            tempi = i;
            printf("|");
        }
        else if (i == (p[counter].burst_time * scalingFactor) / 2 + tempi)
        {
            printf("P%d", arr[counter].pid);
        }
        else
        {
            printf(" ");
        }

    }
    printf("|");
    printf("\n");

    for (i = 0; i < scalingFactor * totalCPUBurstTime + 2 + n; i++)
    {
        printf("-");
    }
    printf("\n");

    /* printing the time labels of the gantt chart */
    counter = 0;
    tempi = 0;
    currentTime = minimumArrivalTime;
    printf("%d", currentTime);
    for (i = 0; i < scalingFactor * totalCPUBurstTime; i++)
    {
        if (i == p[counter].burst_time * scalingFactor + tempi)
        {

            tempi = i;
            currentTime += p[counter].burst_time;
            avg_waiting_time += currentTime;
            counter++;
            printf("%2d", currentTime);
        }
        else
        {
            printf(" ");
        }
    }


    currentTime += p[counter].burst_time;

    printf("%2d\n\n", currentTime);


    cout << endl;

    /*
    AT - Arrival Time of the process
    BT - Burst time of the process
    ST - Start time of the process
    CT - Completion time of the process
    TAT - Turnaround time of the process
    WT - Waiting time of the process
    RT - Response time of the process
    */

    cout << "#P\t" << "AT\t" << "BT\t" << "PRI\t" << "ST\t" << "CT\t" << "TAT\t" << "WT\t" << "\n" << endl;

    for (int i = 0; i < n; i++) {
        cout << p[i].pid << "\t" << p[i].arrival_time << "\t" << p[i].burst_time << "\t" << p[i].priority << "\t" << p[i].start_time << "\t" << p[i].completion_time << "\t" << p[i].turnaround_time << "\t" << p[i].waiting_time << "\t" << "\n" << endl;
    }
    cout << "Average Turnaround Time = " << avg_turnaround_time << endl;
    cout << "Average Waiting Time = " << avg_waiting_time << endl;

}
