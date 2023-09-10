#include<stdio.h>
int main()
{
 int c,first,last,middle,n,search,array[100];
 printf("enter no.of elements\n");
 scanf("%d",&n);
 printf("enter %d elements \n",n);
 for(c=0;c<n;c++)
  {
   scanf("%d",array[c]);
  }
 printf("enter value to find \n");
 scanf("%d",&search);
 first=0;
 last=0;
 middle=(first+last)/2;
 while(first<=last)
 {
   if(array[middle]<search)
   {
    first=middle+1;
   }
  else if(array[middle]==search)
  {
   printf("%d found as location %d\n",search,middle);
   break;
  }
 else
 {
 last=middle-1;
 }
 middle=(first+last)/2;
}
 if(first>last)
 {
   printf("elements %d is not found\n",search);
 }
 return 0;
} 


