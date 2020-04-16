1

/*
  Test Cases  input || output
        1. CHEFCHEFF || 2   as [CHEF][CHEF]F
        2. CCHHEEEFFFFCC || 1 as [CCHHEEEFFFF]CC
        3. CHCHEEFFCC || 2  as [CHCHEEF]FCC CH[CHEEFF]CC
        
  it added bcoz we forget to count number of c before h and h before e and so on
*/


#include <iostream>
using namespace std;
int main() {
	int c,h,e,f;
	    string s;
	    c=0;h=0;e=0;f=0;
	    cin>>s;
	    for(int i=0;i<s.length();i++) {
	        if (s[i] == 'C')
	            c++;
	        else if (s[i] == 'H') { 
	            if (c>h)
	                h++;
	        } 
	        else if (s[i] == 'E' ) {
	            if(h>e)
	                e++;
	        }
	        else if(s[i] == 'F') {
	            if(e>f)
	                f++;
	        }
	    }
	    cout<<f<<endl;
	return 0;
}
=====================================================================================================
2

/* FIND DAY OF ANY GREGORIAN CALLENDER  SEE CENTUARY CODE , AND FORMULA */

#include <iostream>
using namespace std;

int main() {
	// your code goes here
	int t,y,m = 0,d=1,l,c,cc[4]={6,4,2,0}; // m month code of january
	string w[7] = {"sunday","monday","tuesday","wednesday","thursday","friday","saturday"};
	cin>>t;     // w[] week aranged according to their day code
	while(t--) {
	    l = 0;
	    cin>>y;
	    int yy = y%100;
	    int yc = (yy + yy/4)%7; // last two digit of year
	    c = cc[ (y/100)%4 ];    // c for century code
	   if(y%400 == 0 || (y%100 != 0 && y%4 == 0))
	        l = 1;  // for leap year
	   int dd = (yc + c + m + d - l)%7;
	   cout<<w[dd]<<endl;
	}   
	return 0;
}

=========================================================================================
3


If the vector has [1, 2, 3]

the returned vector should be [1, 2, 4]		// just like adding 1 to a number

as 123 + 1 = 124.

    NOTE: Certain things are intentionally left unclear in this question which you should practice asking the interviewer.
    For example, for this problem, following are some good questions to ask :

        Q : Can the input have 0’s before the most significant digit. Or in other words, is 0 1 2 3 a valid input?

        A : For the purpose of this question, YES
        Q : Can the output have 0’s before the most significant digit? Or in other words, is 0 1 2 4 a valid output?
        A : For the purpose of this question, NO. Even if the input has zeroes before the most significant digit.

code (c++ 17):

vector<int> Solution::plusOne(vector<int> &A) {
    int t = A.size();
    reverse(A.begin(),A.end());
    while(A.back() == 0 && t>1) {
        A.pop_back();
        --t;
    }
    
    bool loop = true;
    t=0;
    while (loop) {

        A[t] += 1;
        if(A[t] < 10)
            loop = false;
        else {
            A[t] = 0;
            if (t == A.size()-1) {
                A.push_back(1);
                loop = false;
            }
        }
        t++;
    }
    reverse(A.begin(),A.end());
    return A;
}

================================================================================
4

to find the max possible sum of sub-array of an array

int subarray_with_max_possible_sum(int a[],int n) {
	sum = 0;
	best = 0;
	for(int i=0;i<n;i++) {
		sum = max(a[i],sum + a[i]);
		if (i>0)
			best = max(sum,best);
		else
			best = sum;
	}
}

===================================================================================
