# FSJS2.0

This folder contains all the projects build under the supervision of iNeuron FSJS 2.0 instructors.

#include <stdio.h>
#include <stdlib.h>

//Structure for a node of the linked list
struct Node
{
    int coefficient;
    int exponent;
    struct Node* next;
};

//Function to create a new node
struct Node* createNode(int coefficient, int exponent)
{
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    newNode->coefficient = coefficient;
    newNode->exponent = exponent;
    newNode->next = NULL;
    return newNode;
}

//Function to insert a node into a linked list
struct Node* insert(struct Node* head, int coefficient, int exponent)
{
    struct Node* newNode = createNode(coefficient, exponent);
    if(head == NULL)
        return newNode;
    else
    {
        newNode->next = head;
        return newNode;
    }
}

//Function to add two polynomials represented by linked lists
struct Node* addPolynomials(struct Node* first, struct Node* second)
{
    struct Node* result = NULL;
    struct Node *temp1, *temp2;
    temp1 = first;
    temp2 = second;
    while(temp1 != NULL && temp2 != NULL)
    {
        if(temp1->exponent > temp2->exponent)
        {
            result = insert(result, temp1->coefficient, temp1->exponent);
            temp1 = temp1->next;
        }
        else if(temp1->exponent < temp2->exponent)
        {
            result = insert(result, temp2->coefficient, temp2->exponent);
            temp2 = temp2->next;
        }
        else
        {
            result = insert(result, temp1->coefficient + temp2->coefficient, temp1->exponent);
            temp1 = temp1->next;
            temp2 = temp2->next;
        }
    }
    while(temp1 != NULL)
    {
        result = insert(result, temp1->coefficient, temp1->exponent);
        temp1 = temp1->next;
    }
    while(temp2 != NULL)
    {
        result = insert(result, temp2->coefficient, temp2->exponent);
        temp2 = temp2->next;
    }
    return result;
}

//Function to display the polynomial
void display(struct Node* head)
{
    if(head == NULL)
        printf("\nPolynomial does not exist!!");
    else
    {
        printf("\nThe polynomial is:\n");
        while(head != NULL)
        {
            printf("%dx^%d", head->coefficient, head->exponent);
            head = head->next;
            if(head != NULL)
                printf(" + ");
        }
    }
}

int main()
{
    struct Node* first = NULL;
    struct Node* second = NULL;
    struct Node* result = NULL;
    int coefficient, exponent;

    //
