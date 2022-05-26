## Experiment 6

### Aim: 
Implementation of Selected Repeat Protocol algorithm.

### Source Code: 

```cpp
#include <iostream>

using namespace std;

int main()
{
    int frame, windowSize, nack = 0, i, sent;
    cout<<"Enter window size\n";
    cin>>windowSize;

    while (1)
    {
        for (i = 0; i < windowSize; i++)
        {
            cout<<"Frame"<<++sent<<" has been transmission\n";
            
            if (sent == windowsize)
                break;
        }

        cout<<"Negative acknowledge recieved (0/1)\n";
        cin>>nack;
        
        if (nack == 1)
        {
            cout<<"Negative acknowledge recieved (1/1)\n";
            cout<<"Number of frame not recieved: ";
            cin>frame;

            int frames[frame];
            cout<<"Frames number not recieved: ";
        
            for (i = 0; i < frame; i++)
            {
                cin>>frames[i];
                cout<<"Frame "<`<frames[i]<<"has been transmitted\n";
            }
        }
    }
    cout<<"All frames have been transmitted.\n";
    return 0;
}
```

### Output:

![](https://raw.githubusercontent.com/rajatgupta24/DCN/master/exp-6.png)