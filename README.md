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



