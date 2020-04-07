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

