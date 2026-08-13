#include <stdio.h>
#include <string.h>

#define MAX 20

struct Customer
{
    int id;
    char name[30];
    char service[20];
    int price;
    char time[15];
};

int main()
{
    struct Customer queue[MAX];

    int front = -1, rear = -1;
    int mainChoice, customerChoice, managementChoice;
    int serviceChoice;
    int searchID;
    int i, found;
    int totalIncome = 0;
    int servedCustomers = 0;

    while (1)
    {
        printf("\n========================================\n");
        printf("       SMART BEAUTY SALON SYSTEM\n");
        printf("========================================\n");
        printf("1. Customer Panel\n");
        printf("2. Management Panel\n");
        printf("3. Exit\n");
        printf("========================================\n");

        printf("Enter Choice: ");
        scanf("%d", &mainChoice);

        /* ================= CUSTOMER PANEL ================= */

        if (mainChoice == 1)
        {
            while (1)
            {
                printf("\n============= CUSTOMER PANEL =============\n");
                printf("1. Book Appointment\n");
                printf("2. View My Appointment\n");
                printf("3. Back\n");
                printf("===========================================\n");

                printf("Enter Choice: ");
                scanf("%d", &customerChoice);

                /* BOOK APPOINTMENT */

                if (customerChoice == 1)
                {
                    if (rear == MAX - 1)
                    {
                        printf("\nSorry! Appointment Queue is Full.\n");
                    }
                    else
                    {
                        if (front == -1)
                        {
                            front = 0;
                        }

                        rear++;

                        printf("\nEnter Customer ID: ");
                        scanf("%d", &queue[rear].id);

                        printf("Enter Customer Name: ");
                        scanf(" %[^\n]", queue[rear].name);

                        printf("\n--------- SELECT SERVICE ---------\n");
                        printf("1. Haircut     - 300 Tk\n");
                        printf("2. Facial      - 800 Tk\n");
                        printf("3. Hair Spa    - 1000 Tk\n");
                        printf("4. Manicure    - 500 Tk\n");
                        printf("5. Pedicure    - 600 Tk\n");
                        printf("----------------------------------\n");

                        printf("Enter Service: ");
                        scanf("%d", &serviceChoice);

                        if (serviceChoice == 1)
                        {
                            strcpy(queue[rear].service, "Haircut");
                            queue[rear].price = 300;
                        }
                        else if (serviceChoice == 2)
                        {
                            strcpy(queue[rear].service, "Facial");
                            queue[rear].price = 800;
                        }
                        else if (serviceChoice == 3)
                        {
                            strcpy(queue[rear].service, "Hair Spa");
                            queue[rear].price = 1000;
                        }
                        else if (serviceChoice == 4)
                        {
                            strcpy(queue[rear].service, "Manicure");
                            queue[rear].price = 500;
                        }
                        else if (serviceChoice == 5)
                        {
                            strcpy(queue[rear].service, "Pedicure");
                            queue[rear].price = 600;
                        }
                        else
                        {
                            printf("\nInvalid Service!\n");

                            rear--;

                            if (rear < front)
                            {
                                front = -1;
                                rear = -1;
                            }

                            continue;
                        }

                        printf("Enter Appointment Time: ");
                        scanf(" %[^\n]", queue[rear].time);

                        printf("\n========================================\n");
                        printf("       APPOINTMENT CONFIRMED!\n");
                        printf("========================================\n");
                        printf("Queue Number : %d\n", rear - front + 1);
                        printf("Customer ID  : %d\n", queue[rear].id);
                        printf("Customer     : %s\n", queue[rear].name);
                        printf("Service      : %s\n", queue[rear].service);
                        printf("Price        : %d Tk\n", queue[rear].price);
                        printf("Time         : %s\n", queue[rear].time);
                        printf("========================================\n");
                    }
                }

                /* VIEW MY APPOINTMENT */

                else if (customerChoice == 2)
                {
                    if (front == -1)
                    {
                        printf("\nNo Appointment Available.\n");
                    }
                    else
                    {
                        printf("\nEnter Customer ID: ");
                        scanf("%d", &searchID);

                        found = 0;

                        for (i = front; i <= rear; i++)
                        {
                            if (queue[i].id == searchID)
                            {
                                printf("\n========================================\n");
                                printf("        MY APPOINTMENT DETAILS\n");
                                printf("========================================\n");
                                printf("Customer ID  : %d\n", queue[i].id);
                                printf("Customer     : %s\n", queue[i].name);
                                printf("Service      : %s\n", queue[i].service);
                                printf("Price        : %d Tk\n", queue[i].price);
                                printf("Time         : %s\n", queue[i].time);
                                printf("Queue Number : %d\n", i - front + 1);
                                printf("========================================\n");

                                found = 1;
                                break;
                            }
                        }

                        if (found == 0)
                        {
                            printf("\nAppointment Not Found!\n");
                        }
                    }
                }

                /* BACK */

                else if (customerChoice == 3)
                {
                    break;
                }

                else
                {
                    printf("\nInvalid Choice!\n");
                }
            }
        }

        /* ================= MANAGEMENT PANEL ================= */

        else if (mainChoice == 2)
        {
            while (1)
            {
                printf("\n============ MANAGEMENT PANEL ============\n");
                printf("1. View All Appointments\n");
                printf("2. Serve Next Customer\n");
                printf("3. View Waiting Queue\n");
                printf("4. View Daily Income\n");
                printf("5. Back\n");
                printf("==========================================\n");

                printf("Enter Choice: ");
                scanf("%d", &managementChoice);

                /* VIEW ALL APPOINTMENTS */

                if (managementChoice == 1)
                {
                    if (front == -1)
                    {
                        printf("\nNo Appointment Available.\n");
                    }
                    else
                    {
                        printf("\n==============================================\n");
                        printf("          ALL APPOINTMENTS\n");
                        printf("==============================================\n");

                        for (i = front; i <= rear; i++)
                        {
                            printf("\nQueue Number : %d\n", i - front + 1);
                            printf("Customer ID  : %d\n", queue[i].id);
                            printf("Customer     : %s\n", queue[i].name);
                            printf("Service      : %s\n", queue[i].service);
                            printf("Price        : %d Tk\n", queue[i].price);
                            printf("Time         : %s\n", queue[i].time);
                            printf("----------------------------------------------\n");
                        }
                    }
                }

                /* SERVE NEXT CUSTOMER */

                else if (managementChoice == 2)
                {
                    if (front == -1)
                    {
                        printf("\nNo Customer is Waiting.\n");
                    }
                    else
                    {
                        printf("\n========================================\n");
                        printf("             NOW SERVING\n");
                        printf("========================================\n");
                        printf("Queue Number : 1\n");
                        printf("Customer ID  : %d\n", queue[front].id);
                        printf("Customer     : %s\n", queue[front].name);
                        printf("Service      : %s\n", queue[front].service);
                        printf("Time         : %s\n", queue[front].time);
                        printf("Bill         : %d Tk\n", queue[front].price);
                        printf("========================================\n");

                        totalIncome =
                            totalIncome + queue[front].price;

                        servedCustomers++;

                        front++;

                        if (front > rear)
                        {
                            front = -1;
                            rear = -1;
                        }

                        printf("Customer Served Successfully!\n");
                    }
                }

                /* VIEW WAITING QUEUE */

                else if (managementChoice == 3)
                {
                    if (front == -1)
                    {
                        printf("\nNo Customer is Waiting.\n");
                    }
                    else
                    {
                        printf("\n========================================\n");
                        printf("           WAITING QUEUE\n");
                        printf("========================================\n");

                        for (i = front; i <= rear; i++)
                        {
                            printf("Queue %d : %d - %s - %s - %s\n",
                                   i - front + 1,
                                   queue[i].id,
                                   queue[i].name,
                                   queue[i].service,
                                   queue[i].time);
                        }

                        printf("========================================\n");
                    }
                }

                /* DAILY INCOME */

                else if (managementChoice == 4)
                {
                    printf("\n========================================\n");
                    printf("             DAILY INCOME\n");
                    printf("========================================\n");
                    printf("Customers Served : %d\n", servedCustomers);
                    printf("Total Income     : %d Tk\n", totalIncome);
                    printf("========================================\n");
                }

                /* BACK */

                else if (managementChoice == 5)
                {
                    break;
                }

                else
                {
                    printf("\nInvalid Choice!\n");
                }
            }
        }

        /* EXIT */

        else if (mainChoice == 3)
        {
            printf("\nThank You for Using Smart Beauty Salon System!\n");
            break;
        }

        else
        {
            printf("\nInvalid Choice! Please Try Again.\n");
        }
    }

    return 0;
}
