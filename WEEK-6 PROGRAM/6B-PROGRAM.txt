#include <stdio.h>
#include <stdlib.h>

struct Node {
    int data;
    struct Node* next;
};


struct Node* createNode(int data) {
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    newNode->data = data;
    newNode->next = NULL;
    return newNode;
}


void push(struct Node** top, int data) {
    struct Node* newNode = createNode(data);
    newNode->next = *top;
    *top = newNode;
    printf("Pushed %d to stack\n", data);
}

void pop(struct Node** top) {
    if (*top == NULL) {
        printf("Stack is empty\n");
        return;
    }
    struct Node* temp = *top;
    *top = (*top)->next;
    printf("Popped %d from stack\n", temp->data);
    free(temp);
}


void enqueue(struct Node** front, struct Node** rear, int data) {
    struct Node* newNode = createNode(data);
    if (*rear == NULL) {
        *front = *rear = newNode;
        printf("Enqueued %d to queue\n", data);
        return;
    }
    (*rear)->next = newNode;
    *rear = newNode;
    printf("Enqueued %d to queue\n", data);
}

void dequeue(struct Node** front) {
    if (*front == NULL) {
        printf("Queue Underflow\n");
        return;
    }
    struct Node* temp = *front;
    int n=temp->data;
    *front = (*front)->next;
    free(temp);
    printf("Dequeued %d from queue\n", n);
}

void display(struct Node* head) {
    if (head == NULL) {
        printf("List is empty\n");
        return;
    }
    struct Node* temp = head;
    while (temp != NULL) {
        printf("\n%d", temp->data);
        temp = temp->next;
    }
}

int main() {
    struct Node* stack = NULL;
    struct Node* front = NULL;
    struct Node* rear = NULL;
    int choice, data;

    while (1) {
        printf("\n1. Push to stack \n2. Pop from stack \n3. Display stack \n4. Enqueue to queue \n5. Dequeue from queue \n6. Display queue \n7. Exit\nEnter choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                printf("Enter the data to push: ");
                scanf("%d", &data);
                push(&stack, data);
                break;
            case 2:
                pop(&stack);
                break;
            case 3:
                printf("Stack: ");
                display(stack);
                break;
            case 4:
                printf("Enter the data to enqueue: ");
                scanf("%d", &data);
                enqueue(&front, &rear, data);
                break;
            case 5:
                dequeue(&front);
                if (front == NULL) {
                    rear = NULL;
                }
                break;
            case 6:
                printf("Queue: ");
                display(front);
                break;
            case 7:
                exit(0);
            default:
                printf("Invalid choice\n");
        }
    }
}
