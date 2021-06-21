---
layout: post
title:  "Helping Daenerys Targaryen using C"
date:   2019-08-18 18:21:56 -0300
categories: presentation
---

{% include image.html url="/blog/assets/daenerys.jpg" description="Daenerys of the House Targaryen, the First of Her Name, Breaker of Chains and Mother of Dragons :dragon_face:" %}

<br>At the beginning of 2018, I took a class at UFBA, MATA40 - Algorithms and Data Structures, that made me solve a lot of programming exercises using a programming language called C.

One of those exercises was really fun to solve. I've highlighted the most important sentences to solve this problem below:

***

<br> **General of the Immaculate** 

> Daenerys Targaryen is the leader of the mighty army of the Immaculate. As part of a deal, <mark>she promised to raffle a soldier to be proclaimed general of her army</mark>. For the draw, <mark>she placed S pieces of parchment numbered 1 through S in a bag and drew a certain number I; The winner was the Ith soldier on her list</mark>. But Daenerys lost the list of soldiers in her last fight, so she doesn't know which number corresponds to each soldier. As a good queen, <mark> she knows the names of all her soldiers, and also that their numbers are assigned according to the alphabetical order. </mark> But her soldiers are very anxious and soon want to know who was the chosen to be the general. Given the names of Daenerys's soldiers and the number drawn, determine the name of the soldiers who must be the new Immaculate general.

**Input:**

> The first line contains two integers S and I separated by a blank space, 1≤ I≤ S≤100. The next S lines contain the names of Daenerys soldiers between 1 and 20 characters long. Names are composed of lowercase letters 'a' through 'z' only.

**Output:**

> <mark>Your program should print, on a single line, the name of the new Immaculate General. </mark>

**Examples:**

Input: 5 3  
Input: vilan, malganor, tristam, tylian, anduin  
Output: tristam  

***

<br> First, let's understand what the exercise is asking. From the text, we assume that given a bag with pieces of parchment that contain a number corresponding to one of the soldiers, Daenerys will randomly pick a number from that bag and the soldier correspondig to that number will be the general. The soldiers are numbered according to the alphabetical order.   

To achieve that, create a file called `immacculate.c` and write the following, correspondig to the first part of our input (Two integers corresponding to the number of soldiers that will be inserted and the number drawn from the bag):

```c
#include <stdio.h>
#include <stdlib.h>

int main(){
    int soldiers, numberDrawn;
    scanf("%d %d", &soldiers, &numberDrawn);

    return 0;
}

```
After that, we have to verify the condition that says 1 ≤ I ≤ S ≤ 100 and receive our list of soldiers. For standard, C returns 0 for success, so we're going to assume 1 as our failing scenario.

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int soldiers, numberDrawn, i;
    scanf("%d %d", &soldiers, &numberDrawn);

    if (1 <= numberDrawn && numberDrawn <= soldiers && soldiers <= 100) {
        char arrSoldiers[soldiers][200];

        for (i = 0; i < soldiers; i++) {
            scanf("%s", arrSoldiers[i]);
        }

        return 0;
    } else {
        return 1; // Exit status
    }
}

```

Our exercise also says that the names of Daenerys soldiers must be between 1 and 20 characters long. And the names are composed of lowercase letters 'a' through 'z' only. So, let's add that to our code: 

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int main() {
    int soldiers, numberDrawn, i, j;
    scanf("%d %d", &soldiers, &numberDrawn);

    if (1 <= numberDrawn && numberDrawn <= soldiers && soldiers <= 100) {
        char arrSoldiers[soldiers][200];

        for (i = 0; i < soldiers; i++) {
            scanf("%s", arrSoldiers[i]);

            // Check string lenght
            if (strlen(arrSoldiers[i]) > 20) return 1;
            for (j = 0; j < strlen(arrSoldiers[i]); j++) {
                // Check olny ASCII lowercase letters
                if ((int) arrSoldiers[i][j] < 97 ||
                    (int) arrSoldiers[i][j] > 122) return 1;
            }
        }

        return 0;
    } else {
        return 1; // Exit status
    }
}
```

Now here comes the most important part of the exercise, we're going to receive an unsorted list of soldiers and to verify who's the winner we have to order them by alphabetical order and simply print the position of the soldier based on the number drawn, adding that we have our final code: 

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int main() {
    int soldiers, numberDrawn, i, j;
    scanf("%d %d", & soldiers, & numberDrawn);

    if (1 <= numberDrawn && numberDrawn <= soldiers && soldiers <= 100) {
        char arrSoldiers[soldiers][200];
        char aux[20];

        for (i = 0; i < soldiers; i++) {
            scanf("%s", arrSoldiers[i]);

            // Check string lenght
            if (strlen(arrSoldiers[i]) > 20) return 1;
            for (j = 0; j < strlen(arrSoldiers[i]); j++) {
                // Check olny ASCII lowercase letters
                if ((int) arrSoldiers[i][j] < 97 ||
                    (int) arrSoldiers[i][j] > 122) return 1;
            }
        }

        // Order the array 
        for (i = 1; i < soldiers; i++) {
            for (j = 0; j < soldiers - 1; j++) {
                if (strcmp(arrSoldiers[j], arrSoldiers[j + 1]) > 0) {
                    strcpy(aux, arrSoldiers[j]);
                    strcpy(arrSoldiers[j], arrSoldiers[j + 1]);
                    strcpy(arrSoldiers[j + 1], aux);
                }
            }
        }

        // Prints the winner
        printf("%s\n", arrSoldiers[numberDrawn - 1]);
        return 0;
    } else {
        return 1; // Exit status
    }
}
```
Thank you for your time, I hope you have liked this post!
