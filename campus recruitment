#include<stdio.h>
struct stud
{
       char name[50];
       int usn,apt;
    float cgpa;
};
struct stud;
void main()
{
struct stud a[100];
int i,n,p;
float o;
printf(“enter the nuber of students:”)’
scanf(“%d”,&n);
printf(“enter the name,usn and cgpa of  %d students\n”);
for(i=0;i<n;i++)
{
scanf(“%s%d%f”,a[i].name,&a[i].usn,&a[i].cgpa);
}
printf(“enter the cgpa limit for the campus recruitments of  the year 2016-17\n”);
scanf(“%f”,&o);
printf(“the following students are not selected to next level”);
for(i=0;i<n;i++)
{
if(a[i].cgpa<=o)
{

                                                 
                                                                    8
printf(“the students name=%s,usn=%d,cgpa=%f  is not eligible for aptitude test\n”,a[i].name,a[i].usn,a[i].cgpa);
}
}
printf(“the following students are selected to next round of campus recruitment”);
for(i=0;i<n;i++)
{
if(a[i].cgpa>=o)
{
printf(“the student name=%s,usn=%d,cgpa=%f  is selected, enter their aptitude marks\n”,a[i].name,a[i].usn,a[i].cgpa);
scanf(“%d”,&a[i].apt);
}
}
printf(“enter the aptitude test limit for campus recruitment of year 2016-17”);
scanf(“%d”,&p);
printf(“the following students are not selected to the final round of campus recruitment\n”);
for(i=0;i<n;i++)
{
if(a[i].cgpa<=o)
{
if(a[i].apt<=p)
{
printf(“the student name=%s,usn=%d,cgpa=%f is not selected for campus interview\n”,a[i].name,a[i].usn,a[i].cgpa);
}
}
}
for(i=0;i<n;i++)
                                                     9
{
if(a[i].cgpa>=o)
{
if(a[i].apt<=p)
{
printf(“the student name=%s,usn=%d,cgpa=%f,aptitude marks=%d is not selected for campus interview\n”,a[i].name,a[i].usn,a[i].cgpa,a[i].apt);
}
}
}
printf(“the following student are selected for final round of campus recruitment\n”);
for(i=0;i<n;i++)
{
if(a[i].apt>=p)
{
printf(“the student name =%s,usn=%d,cgpa=%f,aptitude marks=%d,is selected to the interview of campus recruitment\n”,a[i].name,a[i].usn,a[i].cgpa,a[i].apt);
}
}
printf(“all the best for those who selected for final round of campus recruitment”);
}
