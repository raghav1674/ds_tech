#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

vector<vector<int>> target_triplet(vector<int> &arr, int target_sum)
{

    vector<vector<int>> matches;

    sort(arr.begin(), arr.end()); // need to sort the array before we do anything (if not sorted.)
    

    for (int i = 0; i < arr.size() - 3; i++)
    {
        int start=i;
        int right = arr.size() - 1; // the right index point to last element
        int left = start + 1; // the left will be +1 the start value
        while (left < right) // till the left don't overtake right
        {
            
            vector<int> match; // create an array of matches.
            int sum = (arr[start] + arr[left] + arr[right]); //calculate sum 

            if (sum == target_sum) // if match found push this pairs of matches in an array and increment left and decrement right 
            {
                match.push_back(arr[start]);
                match.push_back(arr[left]);
                match.push_back(arr[right]);


                left++;
                right--;


                matches.push_back(match);
            }
            else if(sum< target_sum)//if sum < target sum it means we need to increase it ans as the array is sorted we can increase the left value.
                    left++;
            else//if sum > target sum it means we need to decrease it and  as the array is sorted we can decrease the right value.
                    right--;
            
        }


       
    }

  return matches;
}

int main(){


    vector<int> arr={1,2,3,4,5,6,7,8,9,10};
    vector<vector<int>>answer=target_triplet(arr,12);
    for(int i=0;i<answer.size();i++){
        for(int j=0;j<answer[i].size();j++){
                cout<<answer[i][j]<<" ";
        }

        cout<<" , ";
    }
    return 0;
}