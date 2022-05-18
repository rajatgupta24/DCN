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
# Experiment 6

### Aim: 
Selected repeat sliding window protocol algorithm.

### Source Code: 

```cpp

#include <iostream>
using namespace std;
int main()
{
    int frame, windowSize, nack = 0, i;
    cout<<"Enter window size\n";
    cin>>windowSize;
    while (1)
    {
        for (i = ack+1; i <= windowSize; i++, sent++)
            cout<<"\nFrame"<<i<<" has been transmission\n";
        
        cout<<"Negative acknowledge recieved (0/1): ";
        cin>>nack;
        
        if (nack == 1)
        {
            cout<<"Number of frame not recieved: ";
            cin>frame;
            int frames[frame];
            cout<<"Frames number not recieved: ";
        
            for (i = 0; i < frame; i++)
            {
                cin>>frames[i];
                cout<<"Frame "<<frme[i]<<"has been transmitted\n";
            }
        }
        cout<<"ALL frames have been transmitted";
        return 0;
    }
    cout<<"All frames have been transmitted.\n";
    return 0;
}
```
