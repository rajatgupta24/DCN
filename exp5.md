# Experiment 5

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
        for (i = ack+1; i <= windowSize; i++, sent++)
          cout<<"\nFrame"<<i<<" has been transmission\n";
        
        cout<<"Last acknowledge recieved: ";
        cin>>ack;
        if (ack == windowSize)
            break;
    }
    cout<<"All frames have been transmitted.\n";
    return 0;
}
```
