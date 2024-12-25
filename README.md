# HASHTABLE


#include <stdio.h>
#include <stdlib.h>
#define MAX_EMPLOYEES 5
#define HT_SIZE 10
// Employee details need to add to Hash table
struct Employee
{
 int key;
 char name[30];
};
// Create an employee hash table..
struct EmployeeHashTable
{
 struct Employee *employees[MAX_EMPLOYEES];
};
// Using hash function division method
int hash(int key, int m)
{
 return key % m;
}
// insert employee into hash table
void insert(struct EmployeeHashTable *ht, struct Employee *emp, int m)
{
 int index = hash(emp->key, m); // Find index to insert empin hash table
 while (ht->employees[index] != NULL)
 {
 index = (index + 1) % m; //Linear probing finding next position to insert
 }
 ht->employees[index] = emp;
}
// Display the hash table of employees...
void display(struct EmployeeHashTable *ht, int m)
{
 int i;
 printf("Hash Table:\n");
 for (i = 0; i < m; i++)
 {
 if (ht->employees[i] != NULL)
 {
 printf("Index %d: Key=%d, Name=%s\n", i, ht->employees[i]->key,
ht->employees[i]->name);
 }
 else
 {
 printf("Index %d: Empty\n", i);
 }
 }
}
int main()
{
 int i,m;
 struct EmployeeHashTable ht;

 // Make all employee pointers NULL
 for ( i = 0; i < MAX_EMPLOYEES; i++)
 {
 ht.employees[i] = NULL;
 }
 m = HT_SIZE;
 // Create 4 emps key,values to insert into hash table
 struct Employee e1 = {1000, "Ram"};
 struct Employee e2 = {1001, "Naga"};
 struct Employee e3 = {1002, "Lakshmi"};
 struct Employee e4 = {2002, "Sontosh"};
 insert(&ht, &e1, m);
 insert(&ht, &e2, m);
 insert(&ht, &e3, m);
 insert(&ht, &e4, m);
 display(&ht, m);
 return 0;
} 
