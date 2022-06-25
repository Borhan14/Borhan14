Comment:
#include<stdio.h>
#include<conio.h>
int main()
{ 
char com[30];
int i=2,a=0;
printf("\n Enter comment:");
gets(com);
if(com[0]=='/') 
{ 
 if(com[1]=='/') printf("\n It is a comment");
 else if(com[1]=='*') 
  { 
   for(i=2;i<=30;i++) 
    { 
     if(com[i]=='*'&& com[i+1]=='/') 
      { 
       printf("\n It is a comment");
       a=1;
       break;
      } 
    else continue;
    } 
    if(a==0) printf("\n It is not a comment");
  } 
 else printf("\n It is not a comment");
} 
else printf("\n It is not a comment");
getch();
}

Follow calculation:
#include<stdio.h> 
#include<string.h>
#include<ctype.h>
int n,m=0,p,i=0,j=0;
char a[10][10],followResult[10];
void follow(char c);
void first(char c);
void addToResult(char);
int main()
{
 int i;
 int choice;
 char c,ch;
 printf("Enter the no.of productions: ");
 scanf("%d", &n);
 printf(" Enter %d productions\nProduction with multiple terms should be give as separate productions \n", n);
 for(i=0;i<n;i++)
  scanf("%s%c",a[i],&ch);
    // gets(a[i]);
 do
 {
  m=0;
  printf("Find FOLLOW of -->");
  scanf(" %c",&c);
  follow(c);
  printf("FOLLOW(%c) = { ",c);
  for(i=0; i<m; i++)
   printf("%c ",followResult[i]);
  printf(" }\n");
  printf("Do you want to continue(Press 1 to continue....)?");
  scanf("%d%c", &choice, &ch);
 }
 while(choice==1);
}
void follow(char c)
{
    if(a[0][0]==c) addToResult('$');
 for(i=0; i<n; i++)
 {
  for(j=2; j<strlen(a[i]); j++)
  {
   if(a[i][j]==c)
   {
    if(a[i][j+1]!='\0') first(a[i][j+1]);
    if(a[i][j+1]=='\0'&& c!=a[i][0])
     follow(a[i][0]);
   }
  }
 }
}
void first(char c)
{
      int k;
                 if(!(isupper(c)))
                     //f[m++]=c;
                     addToResult(c);
                 for(k=0; k<n; k++)
                 {
                 if(a[k][0]==c)
                 {
                 if(a[k][2]=='$') follow(a[i][0]);
                 else if(islower(a[k][2]))
                     //f[m++]=a[k][2];
                     addToResult(a[k][2]);
                 else first(a[k][2]);
                 }
                 }
}
void  addToResult(char c)
{
    int i;
    for( i=0; i<=m; i++)
        if(followResult[i]==c)
            return;
   followResult[m++]=c;
}

Regular expression:
// to accept languages using rules 'a*b+'

#include<stdio.h>
#include<string.h>

int main()
{
	int state=0, i, len;
	char s[20];
	printf("\nEnter a String:");
	gets(s);
	len= strlen(s);
	for(i=0; i<len; i++)
	{
		if (state==0 && s[i]=='a')
		state=0;
		else if (state==0||state==1 && s[i]=='b')
		state=1;
		else if (state==1 && s[i]=='a')
		{
			state=2;
			break;
		}
		else if (s[i] != 'a' || s[i] != 'b')
		{
			state=2;
			break;
		}
	}
	if (state==1) printf("\n %s is accepted under rule 'a*b+'", s);
	else printf("\n %s is not accepted under rule 'a*b+'", s);
}
Regular expression2:
// to accept languages using rules 'a*'

#include<stdio.h>
#include<string.h>

int main()
{
	int state=0, i, len;
	char s[20];
	printf("\nEnter a String:");
	gets(s);
	len= strlen(s);
	for(i=0; i<len; i++)
	{
		if (state==0 && s[i]=='a')
		state=0;
		else if (state==0 && s[i]!='a')
			{
			state=1;
			break;
		}
	
	}
	if (state==0) printf("\n %s is accepted under rule 'a*'", s);
	else printf("\n %s is not accepted under rule 'a*'", s);
}

Token:
#include <stdbool.h>
#include <stdio.h>
#include <string.h>
#include <stdlib.h>

// Returns 'true' if the character is a DELIMITER.
bool isDelimiter(char ch)
{
	if (ch == ' ' || ch == '+' || ch == '-' || ch == '*' ||
		ch == '/' || ch == ',' || ch == ';' || ch == '>' ||
		ch == '<' || ch == '=' || ch == '(' || ch == ')' ||
		ch == '[' || ch == ']' || ch == '{' || ch == '}')
		return (true);
	return (false);
}

// Returns 'true' if the character is an OPERATOR.
bool isOperator(char ch)
{
	if (ch == '+' || ch == '-' || ch == '*' ||
		ch == '/' || ch == '>' || ch == '<' ||
		ch == '=')
		return (true);
	return (false);
}

// Returns 'true' if the string is a VALID IDENTIFIER.
bool validIdentifier(char* str)
{
	if (str[0] == '0' || str[0] == '1' || str[0] == '2' ||
		str[0] == '3' || str[0] == '4' || str[0] == '5' ||
		str[0] == '6' || str[0] == '7' || str[0] == '8' ||
		str[0] == '9' || isDelimiter(str[0]) == true)
		return (false);
	return (true);
}

// Returns 'true' if the string is a KEYWORD.
bool isKeyword(char* str)
{
	if (!strcmp(str, "if") || !strcmp(str, "else") ||
		!strcmp(str, "while") || !strcmp(str, "do") ||
		!strcmp(str, "break") ||
		!strcmp(str, "continue") || !strcmp(str, "int")
		|| !strcmp(str, "double") || !strcmp(str, "float")
		|| !strcmp(str, "return") || !strcmp(str, "char")
		|| !strcmp(str, "case") || !strcmp(str, "char")
		|| !strcmp(str, "sizeof") || !strcmp(str, "long")
		|| !strcmp(str, "short") || !strcmp(str, "typedef")
		|| !strcmp(str, "switch") || !strcmp(str, "unsigned")
		|| !strcmp(str, "void") || !strcmp(str, "static")
		|| !strcmp(str, "struct") || !strcmp(str, "goto"))
		return (true);
	return (false);
}

// Returns 'true' if the string is an INTEGER.
bool isInteger(char* str)
{
	int i, len = strlen(str);

	if (len == 0)
		return (false);
	for (i = 0; i < len; i++) {
		if (str[i] != '0' && str[i] != '1' && str[i] != '2'
			&& str[i] != '3' && str[i] != '4' && str[i] != '5'
			&& str[i] != '6' && str[i] != '7' && str[i] != '8'
			&& str[i] != '9' || (str[i] == '-' && i > 0))
			return (false);
	}
	return (true);
}

// Returns 'true' if the string is a REAL NUMBER.
bool isRealNumber(char* str)
{
	int i, len = strlen(str);
	bool hasDecimal = false;

	if (len == 0)
		return (false);
	for (i = 0; i < len; i++) {
		if (str[i] != '0' && str[i] != '1' && str[i] != '2'
			&& str[i] != '3' && str[i] != '4' && str[i] != '5'
			&& str[i] != '6' && str[i] != '7' && str[i] != '8'
			&& str[i] != '9' && str[i] != '.' ||
			(str[i] == '-' && i > 0))
			return (false);
		if (str[i] == '.')
			hasDecimal = true;
	}
	return (hasDecimal);
}

// Extracts the SUBSTRING.
char* subString(char* str, int left, int right)
{
	int i;
	char* subStr = (char*)malloc(
				sizeof(char) * (right - left + 2));

	for (i = left; i <= right; i++)
		subStr[i - left] = str[i];
	subStr[right - left + 1] = '\0';
	return (subStr);
}

// Parsing the input STRING.
void parse(char* str)
{
	int left = 0, right = 0;
	int len = strlen(str);

	while (right <= len && left <= right) {
		if (isDelimiter(str[right]) == false)
			right++;

		if (isDelimiter(str[right]) == true && left == right) {
			if (isOperator(str[right]) == true)
				printf("'%c' IS AN OPERATOR\n", str[right]);

			right++;
			left = right;
		} else if (isDelimiter(str[right]) == true && left != right
				|| (right == len && left != right)) {
			char* subStr = subString(str, left, right - 1);

			if (isKeyword(subStr) == true)
				printf("'%s' IS A KEYWORD\n", subStr);

			else if (isInteger(subStr) == true)
				printf("'%s' IS AN INTEGER\n", subStr);

			else if (isRealNumber(subStr) == true)
				printf("'%s' IS A REAL NUMBER\n", subStr);

			else if (validIdentifier(subStr) == true
					&& isDelimiter(str[right - 1]) == false)
				printf("'%s' IS A VALID IDENTIFIER\n", subStr);

			else if (validIdentifier(subStr) == false
					&& isDelimiter(str[right - 1]) == false)
				printf("'%s' IS NOT A VALID IDENTIFIER\n", subStr);
			left = right;
		}
	}
	return;
}

// DRIVER FUNCTION
int main()
{
	// maximum length of string is 100 here
	char str[100] = "int a = b + c * 1; ";

	parse(str); // calling the parse function

	return (0);
}

