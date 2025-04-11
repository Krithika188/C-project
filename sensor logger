# C-project
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

// Log file name
#define LOG_FILE "sensor_log.csv"

// Function to get current timestamp
void getCurrentTimestamp(char *buffer, int size) {
    time_t now = time(NULL);
    struct tm *t = localtime(&now);
    strftime(buffer, size, "%Y-%m-%d %H:%M:%S", t);
}

// Function to simulate sensor data
void getSensorData(float *temperature, float *humidity) {
    *temperature = (rand() % 400) / 10.0 + 20;  // Simulated temp: 20-60°C
    *humidity = (rand() % 1000) / 10.0;         // Simulated humidity: 0-100%
}

// Function to log sensor data
void logSensorData() {
    FILE *file = fopen(LOG_FILE, "a+"); // Open in append+read mode
    if (file == NULL) {
        printf("❌ Error: Could not open log file!\n");
        return;
    }

    // Check if file is empty to write header
    fseek(file, 0, SEEK_END);
    long size = ftell(file);
    if (size == 0) {
        fprintf(file, "Timestamp,Temperature,Humidity\n");
    }

    float temperature, humidity;
    char timestamp[30];
    
    getCurrentTimestamp(timestamp, sizeof(timestamp));
    getSensorData(&temperature, &humidity);

    fprintf(file, "%s,%.2f,%.2f\n", timestamp, temperature, humidity);
    fclose(file);
    
    printf("✅ Logged Data -> Time: %s | Temp: %.2f°C | Humidity: %.2f%%\n", 
            timestamp, temperature, humidity);
}

// Function to view logs
void viewLogs() {
    FILE *file = fopen(LOG_FILE, "r");
    if (file == NULL) {
        printf("⚠️ No logs found. Start logging data first.\n");
        return;
    }

    char line[100];
    printf("\n--- Sensor Data Logs ---\n");
    while (fgets(line, sizeof(line), file)) {
        printf("%s", line);
    }
    printf("------------------------\n");

    fclose(file);
}

int main() {
    int choice;
    srand(time(0)); // Seed for random values

    while (1) {
        printf("\n🔘 Menu:\n1. Log Sensor Data\n2. View Logs\n3. Exit\nChoose an option: ");
        if (scanf("%d", &choice) != 1) {
            printf("Invalid input. Exiting...\n");
            break;
        }

        switch (choice) {
            case 1: logSensorData(); break;
            case 2: viewLogs(); break;
            case 3: printf("👋 Exiting...\n"); return 0;
            default: printf("❌ Invalid option! Try again.\n");
        }
    }
}
