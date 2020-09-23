<div align="center">

## Make a Continous Clock in Turbo C\+\+


</div>

### Description

This code uses the Video Display Unit (VDU) Concept.

this program can compiled and executed on DOS mode (I used Turbo c++ 2.0 compiler) On execution It gives a continue clock at Right-Below corner. After execution It gives promp again to you but clock continues untill you terminate the Dos screen.
 
### More Info
 
Nothing is required as input

Nothing Just How to execute the code on Dos screen.

Show the clock in 00:00:00 mode

Hours 0->23

I am not encountered any Side effects. But it uses interrupt services so it may cause some side effects.


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[Shyam Sunder Verma](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/shyam-sunder-verma.md)
**Level**          |Intermediate
**User Rating**    |5.0 (30 globes from 6 users)
**Compatibility**  |C\+\+ \(general\), Borland C\+\+
**Category**       |[Miscellaneous](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/miscellaneous__3-1.md)
**World**          |[C / C\+\+](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/c-c.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/shyam-sunder-verma-make-a-continous-clock-in-turbo-c__3-8584/archive/master.zip)





### Source Code

```
// Author : Shyam Sunder Verma
// MLVT Institute Bhilwara
// Rajasthan University Jaipur
// " http://www.geocities.com/ssv445 "
// ssv445@rediffmail.com
//ssv445@yahoo.com
// The source code is copyright of author. it can be modified and used. but it should not be provided on web links.
//you can have the link of this page on your web page.
// This is the program by which you can have a paralle clock in Turbo C++2.0 editor
// Follow the below guidelines to run programs
// 	1. Compile and Make this program under Turbo C++
//	2. Now go to dos shell and run Exe file of the same Program.
//	3. Now type exit.(exit only from dos Shell)
//Notes-- You have to each time run it manually.
// for any comment or query mail me -- shyam
#include <stdio.h>
#include <dos.h>
#include <conio.h>
#include<string.h>
#include<stdlib.h>
char far *v;
char far *vidmem=(char far*)0xB8000000;
char str1[50]="Shyam Sunder Verma-->>",strt[10]="shyam";
//-----------------------------------------------------------------
void putChar(int r,int c,char ch);
void putString(int r,int c,char *ch);
//-----------------------------------------------------------------
#define INTR 0X1C /* The clock tick interrupt */
#ifdef __cplusplus
 #define __CPPARGS ...
#else
 #define __CPPARGS
#endif
void interrupt ( *oldhandler)(__CPPARGS);
struct time t;
void interrupt handler(__CPPARGS);
class Clock
{
  public:
	unsigned int h,m,s;
	float hd;
	Clock()
	{
		gettime(&t);
		h= t.ti_hour;
		m=t.ti_min;
		s=t.ti_sec;
		hd=t.ti_hund;
		putString(24,1,"Shyam Sunder Verma");
		oldhandler = getvect(INTR);
		setvect(INTR, handler);
		//Print();
	}
	void Start()
	{
	}
	~Clock()
	{
	  //	setvect(INTR, oldhandler);
	}
	void Next()
	{
	  hd+=(100/19.2);
	  if(hd>99)
	  {
		 hd=0;
		 s++;
		 if(s>59)
		 {
			s=0;
			m++;
			 if(m>59)
			 {
				h++;
				m=0;
				 if(h>23)
				 {
					h=0;
				 }
			 }
		 }
		 Print();
	  }
	}
	void Print()
	{
	 putString(24,60,"________________");
	 strcpy(str1,"SSV : [");
	 strcat(str1,itoa(h,strt,10));
	 strcat(str1,":");
	 strcat(str1,itoa(m,strt,10));
	 strcat(str1,":");
	 strcat(str1,itoa(s,strt,10));
	 strcat(str1,"]");
	 putString(24,60,str1);
	}
};
Clock clk;
void interrupt handler(__CPPARGS)
{
/* call the old routine */
 clk.Next();
 oldhandler();
}
void main()
{
	clrscr();
	printf("Starting Continue Clock... ");
	delay(2000);
	clrscr();
	delay(2000);
}
//---------------------------------------------------------------
inline void putChar(int r,int c,char ch)
{
	r%=25;
	c%=80;
	v=vidmem+r*160+c*2;
	*v=ch;
	v++;
	*v=(char)78;
}
void putString(int r,int c,char *ch)
{
	for(;*ch;ch++)
		putChar(r,c++,*ch);
}
```

