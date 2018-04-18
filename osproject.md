#include<stdio.h>
#include<stdlib.h>

int cmp_inc(const void * a, const void * b) {
   return ( *(int*)a - *(int*)b );
}
int cmp_dec(const void * a, const void * b) {
   return ( *(int*)b - *(int*)a );
}

int main(){
    int n;
    printf("Enter no.of cylinders: ");
    scanf("%d",&n);
    int prev,curr,no_of_elements;
    printf("\nEnter current position: ");
    scanf("%d",&curr);
    printf("\nEnter previous position: ");
    scanf("%d",&prev);
    printf("\nEnter no of queries left: ");
    scanf("%d",&no_of_elements);
    int element[no_of_elements],j=0,k=0,pre[no_of_elements],next[no_of_elements];
    next[j]=curr;j++;
    for(int i=0;i<no_of_elements;i++){
        scanf("%d",&element[i]);
        if(element[i]>=curr){
            next[j]=element[i];
            j++;
        }
        if(element[i]<curr){
            pre[k]=element[i];
            k++;
        }
    }
    int sum=0;
    if(curr>=prev){
        qsort(next,j,sizeof(int),cmp_inc);
        qsort(pre,k,sizeof(int),cmp_dec);
        for(int m=1;m<j;m++){
            sum+=next[m]-next[m-1];
        }
        sum+=(n-1)-next[j-1];
        sum+=(n-1)-pre[0];
        for(int m=1;m<k;m++){
            sum+=pre[m-1]-pre[m];
        }
        printf("Total distance that needs to be travelled %d",sum);
    }

}
