# digital-clock-and-stopwatch
This is the project of the subject Computer programming . On this project we are making digital clock and stopwatch using C program . 
#include <stdio.h> 
#include <time.h> 
#include <windows.h> 
#include <conio.h>

int main() { 
int choice; int hour, min, sec; time_t start, current; double elapsed_time;

while (1) {
    system("cls");
    printf("Choose Mode:\n");
    printf("1. Digital Clock\n");
    printf("2. Stopwatch\n");
    printf("3. Exit\n");
    printf("Enter your choice: ");
    scanf("%d", &choice);
    getchar(); // Consume newline character

    if (choice == 1) {
        time_t s;
        struct tm *current_time;
        s = time(NULL);
        current_time = localtime(&s);
        hour = current_time->tm_hour;
        min = current_time->tm_min;
        sec = current_time->tm_sec;

        while (1) {
            system("cls");
            printf("%02d:%02d:%02d\n\t\t", hour, min, sec);
            Sleep(1000);
            sec++;
            if (sec == 60) { sec = 0; min++; }
            if (min == 60) { min = 0; hour++; }
            if (hour == 24) { hour = 0; }

            if (_kbhit()) { // Allow exit with key press
                getchar();
                break;
            }
        }
    } 
    else if (choice == 2) {
        printf("Press Enter to start the stopwatch...");
        while (getchar() != '\n');

        start = time(NULL);
        printf("Stopwatch started. Press any key to stop...\n");
        
        while (!_kbhit()) { // Keep updating time until a key is pressed
            current = time(NULL);
            elapsed_time = difftime(current, start);
            system("cls");
            printf("Stopwatch Running...\n");
            printf("Elapsed time: %.2f seconds\n", elapsed_time);
            Sleep(500); // Update every 0.5 seconds
        }
        getchar(); // Consume key press
    } 
    else if (choice == 3) {
        printf("Exiting...\n");
        break;
    } 
    else {
        printf("Invalid choice! Try again.\n");
        Sleep(1000);
    }
}
return 0;

}
