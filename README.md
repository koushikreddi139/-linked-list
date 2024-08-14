#include <stdio.h> 
#include <stdlib.h>
typedef struct Node { 
int data; struct Node* next;
} Node;
Node* createNode(int data) { 
Node* newNode = (Node*)malloc(sizeof(Node));
newNode->data = data; 
newNode->next = NULL; 
return newNode;
}
void printList(Node* head) { 
Node* temp = head;
while (temp != NULL) {
printf("%d -> ", temp->data);
temp = temp->next;
}
printf("NULL\n");
}
void insertMiddle(Node** head, int data)
{
if (*head == NULL)
{
// If list is empty, just add the node *head = createNode(data); return;
}
Node* slow = *head;
Node* fast = *head;
Node* prev = NULL;
while (fast != NULL && fast->next != NULL)
{
    prev = slow;
    slow = slow->next;
    fast = fast->next->next;
}
Node* newNode = createNode(data);
if (prev != NULL)
{
    prev->next = newNode;
}
newNode->next = slow;
}
void deleteMiddle(Node** head) 
{ 
if (*head == NULL) return;
// Empty list if ((*head)->next == NULL)
{
// Only one node free(*head);
*head = NULL;
return;
}
Node* slow = *head;
Node* fast = *head;
Node* prev = NULL;
while (fast != NULL && fast->next != NULL)
{
    prev = slow;
    slow = slow->next;
    fast = fast->next->next;
}
if (prev != NULL)
{
    prev->next = slow->next;
}
free(slow);
} 
int main()
{
Node* head = NULL;
insertMiddle(&head, 1);
insertMiddle(&head, 2);
insertMiddle(&head, 3);
insertMiddle(&head, 4);
insertMiddle(&head, 5);
printf("Original List:\n");
printList(head);
insertMiddle(&head, 99);
printf("After Inserting 99 in the middle:\n");
printList(head);
deleteMiddle(&head);
printf("After Deleting the middle node:\n");
printList(head);
return 0;
}
