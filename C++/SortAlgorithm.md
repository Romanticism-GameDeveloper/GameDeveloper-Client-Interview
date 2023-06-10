뭔가 즉석으로 구현해보라고 할 수도 있지 않을까 싶어서 쓴 Sorting 알고리즘 코드

``` C++
#include<iostream>
#include<vector>
#include<algorithm>
using namespace std;
void SelectionSort(vector<int> v){
    for(int i = 0; i<v.size()-1; ++i){ //맨 마지막은 알아서 정렬 될 거니까
        int Index = i;
        for(int j = i+1; j<v.size(); ++j){
            if(v[Index]>v[j]){
                Index = j;
            }
        }
        swap(v[i], v[Index]);
    }
}


void InsertionSort(vector<int> v){
    for(int i = 1; i<v.size(); ++i){
        //i의 원래 자리를 찾아나가자
        int key = v[i];
        int j = i-1;
        while(j>=0 && key<v[j]){
            v[j+1] = v[j];
            --j;
        }
        v[j+1] = key;
    }
}

void qsort(vector<int> v, int s, int e){
    int pivot = v[s];
    int bs = s, be = e;
    while(s<e){
        while(pivot<=v[e] && s<e) --e;
        if(s>e) break;
        while(pivot>=v[s] && s<e) ++s;
        if(s>e) break;
        swap(v[s], v[e]);
    }
    //pivot 자리도 만들어주기
    swap(v[bs], v[s]);
    
    if(bs<s) qsort(v, bs, s-1);
    if(be>e) qsort(v, s+1, be);

}

void BubbleSort(vector<int> v){
    //버블 횟수
    for(int i = 0; i<v.size()-1; ++i){
        //실제 비교
        for(int j = 1; j<v.size()-i; ++j){
            if(v[j-1]>v[j]) swap(v[i], v[j]);
        }
    }
}
```
