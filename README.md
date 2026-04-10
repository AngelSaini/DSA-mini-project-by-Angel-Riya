# DSA-mini-project-by-Angel-Riya
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define MAX_HISTORY 100
#define MAX_URL_LEN 256

typedef struct {
    char urls[MAX_HISTORY][MAX_URL_LEN];
    int count;
    int current;
} BrowserHistory;

// Initialize
BrowserHistory* init() {
    BrowserHistory* h = (BrowserHistory*)malloc(sizeof(BrowserHistory));
    h->count = 0;
    h->current = -1;
    return h;
}

// Visit URL
void visit(BrowserHistory* h, char url[]) {
    if (h->count < MAX_HISTORY) {
        strcpy(h->urls[h->count], url);
        h->current = h->count;
        h->count++;
        printf("Visited: %s\n", url);
    } else {
        printf("History Full!\n");
    }
}

// Show history
void show_history(BrowserHistory* h) {
    if (h->count == 0) {
        printf("No history available!\n");
        return;
    }

    printf("\n--- History ---\n");
    for (int i = 0; i < h->count; i++) {
        printf("%d. %s", i + 1, h->urls[i]);
        if (i == h->current)
            printf("  <-- Current");
        printf("\n");
    }
}

// Go Back (select any URL)
void go_back(BrowserHistory* h) {
    int choice;

    if (h->count == 0) {
        printf("No history available!\n");
        return;
    }

    show_history(h);
    printf("Enter which URL you want to open: ");
    scanf("%d", &choice);

    if (choice >= 1 && choice <= h->count) {
        h->current = choice - 1;
        printf("Now Opening: %s\n", h->urls[h->current]);
    } else {
        printf("Invalid choice!\n");
    }
}

int main() {
    BrowserHistory* h = init();
    int choice;
    char url[MAX_URL_LEN];

    while (1) {
        printf("\n1. Visit URL\n");
        printf("2. Show History\n");
        printf("3. Go Back (Select URL)\n");
        printf("4. Exit\n");

        printf("Enter choice: ");
        scanf("%d", &choice);

        switch (choice) {

            case 1:
                printf("Enter URL: ");
                scanf("%s", url);
                visit(h, url);
                break;

            case 2:
                show_history(h);
                break;

            case 3:
                go_back(h);
                break;

            case 4:
                free(h);
                printf("Exit\n");
                return 0;

            default:
                printf("Invalid choice!\n");
        }
    }
}
