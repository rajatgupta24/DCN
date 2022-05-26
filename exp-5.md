## Experiment 5

### Aim: 

Write a program to implement & study Stop and Wait Protocol.

### Source Code: 

```cpp
#include <iostream>
#include <stdio.h>

using namespace std;

int main()
{
    int windowSize, i, send, ack;
    cout<<"Enter number of frames: \n";
    cin>>windowSize;

    for(i = 0; i < windowsize; i++)
    {
        sent = i;
        cout<<"Frame "<<sent<<"is sent\n";
        cin>>ack;

        if (ack != send){
            i--;
            continue;
        }
    }

    return 0;
}
```

### Output:

![](https://raw.githubusercontent.com/rajatgupta24/DCN/master/exp-5.png)