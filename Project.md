- 👋 Hi, I’m @Akhil-13111997
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---
Akhil-13111997/Akhil-13111997 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
#include <bits/stdc++.h>
using namespace std;
int pd_op(char ar_op){
	if(ar_op == '+'||ar_op == '-')
	return 1;
	if(ar_op == '*'||ar_op == '/')
	return 2;
	return 0;
}
int taking_ch(int a, int b, char ar_op){
	switch(ar_op){
		case '+': return a + b;
		case '-': return a - b;
		case '*': return a * b;
		case '/': return a / b;
	}
}
int Calculate(string Take){
	int i;
	stack <int> ans;
	stack <char> st_op;
	
	for(i = 0; i < Take.length(); i++){
		if(Take[i] == ' ')
			continue;
		else if(Take[i] == '('){
			st_op.push(Take[i]);
		}
		else if(isdigit(Take[i])){
			int val = 0;
			while(i < Take.length() &&
						isdigit(Take[i]))
			{
				val = (val*10) + (Take[i]-'0');
				i++;
			}
			ans.push(val);
			i--;
		}
		else if(Take[i] == ')')
		{
			while(!st_op.empty() && st_op.top() != '(')
			{
				int val2 = ans.top();
				ans.pop();
				
				int val1 = ans.top();
				ans.pop();
				
				char ar_op = st_op.top();
				st_op.pop();
				
				ans.push(taking_ch(val1, val2, ar_op));
			}
			if(!st_op.empty())
			st_op.pop();
		}
		else
		{
			while(!st_op.empty() && pd_op(st_op.top())>= pd_op(Take[i])){
				int val2 = ans.top();
				ans.pop();
				
				int val1 = ans.top();
				ans.pop();
				
				char ar_op = st_op.top();
				st_op.pop();
				
				ans.push(taking_ch(val1, val2, ar_op));
			}
			st_op.push(Take[i]);
		}
	}
	while(!st_op.empty()){
		int val2 = ans.top();
		ans.pop();
				
		int val1 = ans.top();
		ans.pop();
				
		char ar_op = st_op.top();
		st_op.pop();
				
		ans.push(taking_ch(val1, val2, ar_op));
	}
	return ans.top();
}

int main() {
    char exper[100];
    cin.getline(exper,100);
	cout << Calculate(exper) << "\n";
	return 0;
}

