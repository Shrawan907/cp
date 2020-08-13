##  only comptitive programming Q&A ##




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
5


Merge Intervals

    Asked in:  
    Google

Given a set of non-overlapping intervals, insert a new interval into the intervals (merge if necessary).

You may assume that the intervals were initially sorted according to their start times.

Example 1:

Given intervals [1,3],[6,9] insert and merge [2,5] would result in [1,5],[6,9].

Example 2:

Given [1,2],[3,5],[6,7],[8,10],[12,16], insert and merge [4,9] would result in [1,2],[3,10],[12,16].

This is because the new interval [4,9] overlaps with [3,5],[6,7],[8,10].

Make sure the returned intervals are also sorted.

{
	Hint for a question not given with a question-------------
	
	

	Have you covered the following corner cases :

	1) Size of interval array as 0.

	2) newInterval being an interval preceding all intervals in the array.

	    Given interval (3,6),(8,10), insert and merge (1,2)

	3) newInterval being an interval succeeding all intervals in the array.

	    Given interval (1,2), (3,6), insert and merge (8,10)

	4) newInterval not overlapping with any interval and falling in between 2 intervals in the array.

	    Given interval (1,2), (8,10) insert and merge (3,6) 

	5) newInterval covering all given intervals.

	    Given interval (3, 5), (7, 9) insert and merge (1, 10)


}

solution (c++ 17):

/*
 * Definition for an interval.		// these comments are added to know how Interval struct look like used in solution
 * struct Interval {
 *     int start;
 *     int end;
 *     Interval() : start(0), end(0) {}
 *     Interval(int s, int e) : start(s), end(e) {}
 * };
 */	
 void swap(int * a,int *b) {
     *a ^= *b ^= *a ^= *b; 
 }
 
vector<Interval> Solution::insert(vector<Interval> &intervals, Interval newInterval) {
	int k = -1,j=-1;
   if(intervals.size() == 0){			// if vector is empty	
      intervals.push_back(newInterval);
      return intervals;
    } 
    if(newInterval.end < newInterval.start)	// if interval given in oposite order
        swap(&newInterval.start,&newInterval.end);
    if(intervals[0].start > newInterval.end) {
        reverse(intervals.begin(),intervals.end());
        intervals.push_back(newInterval);
        reverse(intervals.begin(),intervals.end());
    }
    if(intervals.back().end < newInterval.start){
        intervals.push_back(newInterval);
        return intervals;
    }
	/*
						 how i think for finding the value of k and j
						 vector index 	0	1	2	3	4	5
						 possible k,j   0   1   2   3   4   5   6   7   8   9   10   11
	*/
    for(int i=0;i<intervals.size();i++) {
        if(intervals[i].start <= newInterval.start) {
            k++;
            if(intervals[i].end < newInterval.start)
                k++;
        }
        if(intervals[i].start <= newInterval.end) {
            j++;
            if(intervals[i].end < newInterval.end)
                j++;
            else
                break;
        } 
        else
            break;
    }
    int m = k/2,n=j/2;
    if(k < 0)
        m = 0;
    else if(k%2 != 0)
        m++;
    else
        newInterval.start = intervals[m].start;
    newInterval.end = max(newInterval.end,intervals[n].end);
    vector<Interval> I;
	
    for(int i=0;i<m;i++)
        I.push_back(intervals[i]);
	
    I.push_back(newInterval);
    
    for(int i=n+1;i<intervals.size();i++)
        I.push_back(intervals[i]);
    return I;
}

========================================================================================
6

You are given n intervals, each from  to 

. You need to merge overlapping intervals to form a new interval. After all possible merging is done, you have a new set of mutually exclusive intervals.
Print the size of this new set of mutually exclusive intervals.

Input Format

    First line contains 

, denoting number of intervals.
Each of next
lines will contain two integers, denoting and .

n = int(input())
c = []
for i in range(0,n):
    a,b = map(int,input().split())
    c.append([a,b])
c.sort()
t=1
for i in range(0,n-1):
    if(c[i][1] < c[i+1][0]):
        t+=1
    else:
        c[i+1][1] = max(c[i][1],c[i+1][1])
print(t) 

======================================================================================
7



Given a collection of intervals, merge all overlapping intervals.

For example:

Given [1,3],[2,6],[8,10],[15,18],

return [1,6],[8,10],[15,18].

Make sure the returned intervals are sorted.




# Definition for an interval.
# class Interval:
#     def __init__(self, s=0, e=0):
#         self.start = s
#         self.end = e
(Python )
class Solution:
    # @param intervals, a list of Intervals
    # @return a list of Interval
    def merge(self, intervals):
        t = []
        for i in intervals:
            a = i.start
            b = i.end
            if a>b:
                c = a
                a = b
                b = c
            t.append([a,b])
        s = len(intervals)
        t.sort()
        for i in range(0,s):
            intervals[i].start = t[i][0]
            intervals[i].end = t[i][1]
        t = []   
        i=0
        while(i<len(intervals)-1):
            if(intervals[i].end >= intervals[i+1].start):
                if intervals[i].end >= intervals[i+1].end:
                    intervals.remove(intervals[i+1])
                else:
                    intervals[i].end = intervals[i+1].end
                    intervals.remove(intervals[i+1])
            else:
                i+=1
        return intervals
	
============================================================================================
8

A=1 Z=26 AA=27 AB=28 AAA=703
now find string back from number

solution( c++17 ):

string Solution::convertToTitle(int A) {
    int x;
    string C = "";
    while(A>0) {
        x = A%26;
        if(x==0){
            x = 26;
            A-=26; 
	    // we subtract 26 because for x > 0 it means that number x more then actual dividend no. but x = 0  means 26 more so generaly we forgot to subtract due to which wrong ans printed. this can be easily chek for A = 943566 whose right output: "BAQTZ"
        }
        A = A/26;
        C += (char)(x+64);
    }
    reverse(C.begin(),C.end());
    return C;
}


======================< mast concept >============================
9

Rearrange a given array so that Arr[i] becomes Arr[Arr[i]] with O(1) extra space.

Input : [1, 0]
Return : [0, 1


    Lets say N = size of the array. Then, following holds true :

      1.  All elements in the array are in the range [0, N-1]
      2.  N * N does not overflow for a signed integer

solution: (c++)
-----concept------
 if it is possible that every index store two values old and new
    let old val. a  and  new val b
       if we sore values as a + bn
       then val/n give new value and val%n give old val
    1. increment every element by ( (A[A[i]]%n)*n )
    2. divide every element by n
----------------
void Solution::arrange(vector<int> &A) {
    int n = A.size();
    for(int i=0;i<n;i++) {
        A[i] += (A[A[i]]%n)*n;
    }
    for(int i=0;i<n;i++) {
        A[i] /= n;
    }
}

========================================================================
10

Q. Find the way we can make total in different ways using different number of each coins,
	example: n = 10 c = {2,5,3,6} (coins)
	So we can make total as:
	 2 2 2 2 2	= 10
	 2 2 3 3 	= 10
	 2 2 6		= 10
	 2 3 5		= 10
	 5 5 		= 10
	 So there are 5 ways we can make total 10 from coins {2,5,3,6}.
	 
Sol (C++) :
		(  Dynamic Programming  )

map< pair<int,int>,long > m;	// declaring pair map
long search(int n,int j,vector<long> c,int l) {
    if(n < 0)
        return 0;
    if (n == 0) {
        return 1;
    }
    if(m.count({n,j}))  // use of memorization 
        return m[{n,j}];
    else {
        long t = 0;
        long result = 0;
        for(int i = j; i < l; i++) {
            if(n-c[i] >= 0) {
                result = search(n-c[i],i,c,l);
                if (result > 0)
                    t += result;
            }
            else    
                break;	// we' break ' the loop here bcoz 'c' is sorted but if it was not we should use " continue ".
        }
        m[{n,j}] = t;	// assign value in paired map, it is used as memorization ( Dynamic programing )
        return t;
    }
}

long getWays(int n, vector<long> c) {
    sort(c.begin(),c.end());		// sorting is not neccesory, we can skip this by making change in line 437
    int l = (int) c.size();
    return search(n,0,c,l);

}

int main() {
  cout<< getWays( total amount to be made , set of coins ) << endl;
 }

================================================================
11.

Q
Larry has been given a permutation of a sequence of natural numbers incrementing from 1 as an array. He must determine whether the array can be sorted using the following operation any number of times: 

A		rotate 
[1,6,5,2,4,3]	[6,5,2]
[1,5,2,6,4,3]	[5,2,6]
[1,2,6,5,4,3]	[5,4,3]
[1,2,6,3,5,4]	[6,3,5]
[1,2,3,5,6,4]	[5,6,4]
[1,2,3,4,5,6]

YES

/*
Yes, it seems very clear that it very hard to solve these question by doing rotation and check as the question said. Well the hint is given in previous comments is so helpful (thank to them), so the hidden approch for this question is same as to determine the solvability of n-puzzle game (i.e. checking the solution is exist or not). Spoiler alert! you have to check for each element that how many elements after its postion are smaller then it, and sum all these count you get for each element. now if the sum is even => solution possible ("YES")
*/
string larrysArray(vector<int> A) {
    int n = A.size();
    int sum = 0;
    for(int i=0;i<n-1;i++)
        for(int j = i+1;j<n;j++)
            if(A[i] > A[j])
                sum += 1;
    if(sum%2 == 0)
        return "YES";
    else
        return "NO";
}
====================================================================
12
	
Q
Given an array of integers, determine whether the array can be sorted in ascending order using only one of the following operations one time.

    Swap two elements.
    Reverse one sub-segment.

Determine whether one, both or neither of the operations will complete the task. If both work, choose swap. For instance, given an array [2,3,5,4] either swap the 4 and 5, or reverse them to sort the array. Choose swap. The Output Format section below details requirements. 
 
< https://www.hackerrank.com/challenges/almost-sorted/problem >
soln: 
void almostSorted(vector<int> arr) {
    int n=arr.size();
    int r=0,j=0,k=0;
    for(int i=1;i<n;i++) {
        if(arr[i] < arr[i-1] ) {
            if(r == 0) {		// for problem in neighbours
                j = i-1;
                k = i;
                r = 1;
            }
            else if(r == 1 && k == i-1) {	// if this condition is gona true than surely "yes recursive" or "no" 
                r = 2;
                k = i;
            } else if(r == 2 && k == i-1) {	// update value k for recursive
                k = i;
            } else if(r == 1) {			//  i.e update k for swap 
                k = i;
                r = 3;
            } else {				// for not possible
                r = 4;
            }
        }
    }
    if(r == 0)
        cout<<"yes"<<endl;
    else if( r == 4)
        cout<<"no"<<endl;
    else {
        if (j == k-1) {					// we also compare with neigbours if we perform that changes
            if(j == 0 || arr[k] > arr[j-1]) {
                if( k == n-1 || arr[j] < arr[k+1])
                    cout<<"yes\nswap "<<j+1<<" "<<k+1;
                else    
                    cout<<"no";
            } else  
                cout<<"no";
        }
        else if(r == 2) {				// we also compare with neigbours if we perform that changes
            if(j == 0 || arr[k] >= arr[j-1]) {
                if(k == n-1 || arr[j] <= arr[k+1])
                    cout<<"yes\nreverse "<<j+1<<" "<<k+1;
                else    
                    cout<<"no";
            } else
                cout<<"no";
        }
        else {						// we also compare with neigbours if we perform that changes
            if(arr[k] <= arr[j+1]) {
                if(j == 0 || arr[k] >= arr[j-1]) {
                    if(arr[j] >= arr[k-1]) {
                        if(k == n-1 || arr[j] <= arr[k+1])
                            cout<<"yes\nswap "<<j+1<<" "<<k+1;
                        else    
                            cout<<"no";
                    } else    
                        cout<<"no";
                } else 
                    cout<<"no";
            } else
                cout<<"no";
        }
        cout<<endl;
    }
}
		   
		   
========================================================================================

14
 move matrix to 90 degree in anticlock wise dir without in O(1) space
 // transepose than swaping
 ans:
 
 #include<bits/stdc++.h>
using namespace std;

int main() {
    int n;
    cin>>n;
    int a[n][n];
    for(int i=0;i<n;i++){
        for(int j=0;j<n;j++)
            cin>>a[i][j];
    }
    int t,k,r,temp;
    
    for(int j=0;j<n;j++) {
        t = (int)((j+1) / 2);
        k=0;r=j;
        while(t-- && k < n && r >= 0) {
            temp = a[k][r];
            a[k][r] = a[r][k];
            a[r][k] = temp;
            k++;
            r--;
        }
    }
    for(int i=1;i<n;i++) {
        t = (n-i) / 2;
        k = i;r=n-1;
        while (t-- && k < n && r >= 0)
        {
            temp = a[k][r];
            a[k][r] = a[r][k];
            a[r][k] = temp;
            k++;
            r--;
        }
    }

    for(k=0,r=n-1; k < r; k++,r--) {
        for(int j=0;j<n;j++){
            temp = a[r][j];
            a[r][j] = a[k][j];
            a[k][j] = temp;
        }
    }
        cout<<"\n";
        for(int i=0;i<n;i++){
        for(int j=0;j<n;j++)
            cout<<a[i][j]<<" ";
        cout<<"\n";
    }

}

=========================================================================
