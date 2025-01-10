# cpt.data.linked_list

A dynamic data structure that uses pointers

## Synopsis

```c
typedef struct node {
  int val;
  node *next;
} node_t;
```

## Overview

A linked list functions as an array that can grow and
shrink as needed, from any point in the array

There are some advantages over simple [arrays](./xp8m.md):

- Items can be added or removed from any point in the list
- There is no need to define an initial size

However there are some other disadvantages:

- There is no "random" constant access, to reach any element
  on the list you have to iterate over the whole list
- It requires [dynamic memory](./77ao.md) allocation and [pointers](./xl2p.md) 
- They have a large overhead in memory space and speed of
  access due to not be stored contiguously on memory

### What is a linked list

It's a set of dynamically allocated `nodes`, arranged in such a
way that each `node` contains one value and one pointer. The
pointer always points to either the next node or tu `NULL`

> If it points to `NULL` then it means it's the last node in the
> list

A linked list is held using a local `pointer` variable which
points to the first item of the list, if that `pointer` is
also `NULL` then the list is considered empty

## Cookbook

### Simple implementation of linked list in `c`

For a simple implementation we will

- Create the `node_t` structure
- Define the `head` that we will point to `NULL`
- Allocate the first `node` and make the `head` point to it
- Set the node value and make it's `next` pointer point to `NULL`

```c
typedef struct node {
  int value;
  node *next;
} node_t;

int main() {
  node_t *head = NULL;

  head = (node_t *)malloc(sizeof(node_t));
  if (head == NULL) {
    return 1;
  }

  head->val = 1;
  head->next = NULL;

  // We add another node

  head->next = (node_t *)malloc(sizeof(node_t));

  head->next->value = 2;
  head->next->next = NULL;
}
```

### Iterating over a linked list

A common way to iterate over a linked list is to loop
to the next `node` until we find the `node` that points
to `NULL`

Thoe not extriclty necessary, it's a good practice to
use a `current` variable to hold the currently accessed
node in order to keep the reference to the `head`

```c
void print_list(head *node_t) {
  node_t *current = head;

  while (node_t->next != NULL) {
    printf("%c ", node_t->val);

    current = node->next
  }

  // We are at the last node since it's
  // `next` pointer is `NULL`
  printf("%c\n", node_t->val);
}
```

### Adding an item to the end of a linked list

To add to the end of a list we will:

- Iterate through the list until we reach it's end
- Create a new `node` item
- Make the last `node` in the list point to the new `node`
- Make the new `node` point to `NULL`

```c
void push(node_t *head, int value) {
  node_t *current = head;

  while (current->next != NULL) {
    current = current->next;
  }

  node_t *new_node = NULL;
  new_node = (node_t *)malloc(sizeof(node_t));

  new_node->value = value;
  new_node->next = NULL;

  current->next = new_node;
}
```

### Adding an item to the beging of the linked list

To add to the beging of a list we will:

- Create a new `node` item
- Point it's `next` pointer to the value of `head`
- Point `head` to the value of the new node
  - Or more easilly make `head` be the pointer 
    of the new `node`

> For this case we will use a double `pointer` to
> be able to replace the actual pointer that it's
> passed to function

```c
void stack(node_t **head, int value) {
  node_t *new_node = NULL;
  new_node = (node_t *)malloc(sizeof(node_t));

  new_node->value = value;
  new_node->next = *head;

  // Make head the pointer of the new node
  *head = new_node;
}
```

### Removing the first item of a linke list (popping)

To remove from the beging of the list (pop the `node`)
we wil perform the reversed action

- Take the next item that the `head` points at and save it
- Free the `head` item
- Set the head to be the next item that we've stored on the side

```c
int pop(node_t **head) {
  int poped_value = -1;
  node_t *next_node = NULL;

  if (*head == NULL) {
    // This should also set an error (like errno)
    return -1;
  }

  next_node = (*head)->next;
  poped_value = (*head)->val;

  free(*head);
  *head = next_node;

  return poped_value;
}
```

### Removing the last item of the linked list

This a very similar operation as **adding** to the end of the
list, with the exception that - since we have to change one
item before the last item, we actually have to look **two** 
items ahead and see if the **next** item is the last one

```c
int remove_last(node_t *head) {
  int returned_item = -1;
  node_t *current = head;

  if (current == NULL) {
    // This should also set an error (like errno)
    return -1;
  }

  if (current->next == NULL) {
    returned_item = current->value;
    free(current);

    return returned_item
  }

  while (current->next->next !== NULL) {
    current = current->next;
  }

  returned_item = current->next->value;

  // Free the memory block of the pointer
  free(current->next);

  // Set the next value pointer to NULL
  current->next = NULL;

  return returned_item;
}
```

### Remove an especific item from a linked list

To remove an item from any point of the linked list,
either by it's index or value, we will need to go over
all the items, continuously looking ahead to find out
if we've reached the node before the item we wish to
remove

This is beacuse we need to change the location to where
the previousnode points to  as well

- Iterate to the `node` before the `node` we wish to delete
- Save the `node` we wish to delete in a temporary `pointer`
- Set the previous `node` next `ponter` to point to the `node` after
  the `node` we wish to delete
- Delete the `node` using the temporary `pointer`

```c
int slice(node_t **head, int index) {
  int value = -1;

  node_t *current = *head;
  node_t *temp = NULL;

  if (index == 0) {
    // From the implementation seen above
    return pop(head);
  }

  // Assuming that they have to pass 0 index values
  // We don't want for current to be the target node 
  // to extract and thus we do `index-1`
  for (int i = 0; i < index-1; i++) {
    // Check that there is next node to go to
    if (current->next == NULL) {
      // Set an out of index error
      return -1;
    }

    current = current->next;
  }

  // Check that the target value to extract exist
  if (current->next == NULL) {
    // Set an out of index error
    return -1;
  }

  temp = current->next;

  value = temp->value;
  current->next = temp->nex;
  free(temp);

  return value
}
```
