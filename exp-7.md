## Experiment 7

### Aim: 

Go Back N sliding window protocol algorithm.

### Source Code: 

```cpp
#include <iostream>

using namespace std;

int main()
{
    int sent = 0, windowSize, ack = 0, i;
    cout<<"Enter window size\n";
    cin>>windowSize;

    while (1)
    {
        for (i = ack+1; i <= windowSize; i++)
        {
            cout<<"\nFrame"<<sent+1<<" has been transmission\n";
            sent++;
            if (sent == windowsize)
                break;
        }
        
        cout<<"Last acknowledgement recieved: ";
        cin>>ack;

        if (ack == windowSize)
            break;
        else 
            sent = ack;
    }
    cout<<"All frames have been transmitted.\n";
    return 0;
}
```
### Output:

![](https://raw.githubusercontent.com/rajatgupta24/DCN/master/exp-7.png)
