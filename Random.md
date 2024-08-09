# Random
* **Event:** n00bz 2024
* **Problem Type:** Crypto
* **Point Value / Difficulty:** 451

## Description
I hid my password behind an impressive sorting machine. The machine is very luck based, or is it?!?!?!?

## Steps
1.  **Understanding Challenge**: The challenge involves a C++ file that acts as a black box. It takes an input string of more than 10 unique characters and randomly shuffles them multiple times. If the string becomes sorted at any point, you receive the flag.
    
2.  **Identifying the Vulnerability**: The vulnerability is that `random_shuffle` uses a default seed, causing it to shuffle the input string in the same way every time we connect to the server.
    
3.  **Initial Input Submission**: To exploit this, first submit the string `0123456789` and observe how it is shuffled by the server.
    
4.  **Crafting the Pre-shuffled Input**: Reverse the observed shuffle to create a pre-shuffled input. Submit this pre-shuffled input, which will result in a sorted string after the server's shuffle, thereby obtaining the flag.



## Code 
```cpp
#include<chrono>
#include<cstdlib>
#include<iostream>
#include<algorithm>
#include<string>
#include<fstream>
#include<thread>
#include<map>
using namespace std;

bool amazingcustomsortingalgorithm(string s) {
    int n = s.size();
    for (int i = 0; i < 69; i++) {
        cout << s << endl;
        bool good = true;
        for (int i = 0; i < n - 1; i++)
            good &= s[i] <= s[i + 1];
        
        if (good)
            return true;

        random_shuffle(s.begin(), s.end());

        this_thread::sleep_for(chrono::milliseconds(500));
    }

    return false;
}

int main() {
    string s;
    getline(cin, s);

    map<char, int> counts;
    for (char c : s) {
        if (counts[c]) {
            cout << "no repeating letters allowed passed this machine" << endl;
            return 1;
        }
        counts[c]++;
    }

    if (s.size() < 10) {
        cout << "this machine will only process worthy strings" << endl;
        return 1;
    }

    if (s.size() == 69) {
        cout << "a very worthy string" << endl;
        cout << "i'll give you a clue'" << endl;
        cout << "just because something says it's random mean it actually is" << endl;
        return 69;
    }

    random_shuffle(s.begin(), s.end());
    
    if (amazingcustomsortingalgorithm(s)) {
        ifstream fin("flag.txt");
        string flag;
        fin >> flag;
        cout << flag << endl;
    }
    else {
        cout << "UNWORTHY USER DETECTED" << endl;
    }
}

```

## Output
```bash
$ nc challs.n00bzunit3d.xyz 10588
0123456789
4378052169
0578439216
^C
$ nc challs.n00bzunit3d.xyz 10588
0123456789
4378052169
0578439216
^C
$ nc challs.n00bzunit3d.xyz 10588
4761058239
0123456789
n00bz{5up3r_dup3r_ultr4_54f3_p455w0rd_7bffc2b26246}
```

#### FLAG
```
n00bz{5up3r_dup3r_ultr4_54f3_p455w0rd_7bffc2b26246}
```