// Algorithms
void stock_span(int *day,int n){
	int *ans = new int[n];
	memset(ans,0,n);
	ans[0] = 1;
	for(int i = 1;i<n;i++){
		//i is the current day
		int j = i-1; //starting from just left of current index
		//to find the NGL index
		while(j>=-1){
			if(day[j] > day[i])
				break;
			j--;
		}
		//j will contain the NGL if j!=-1
		if(j!=-1)ans[i] = (i - j);

		// NGL - curr_idx will give the current span for the stock
		else ans[i] = i+1;
	}
	for(int i= 0 ;i<n;i++)cout<<ans[i]<<" ";
}

// But this was the NAIVE approch, we could use stack either

void stock_span_n(int *day,int n){
		int *ans = new int[n];
	memset(ans,0,n);
	stack<int> s;
	s.push(0); //pushing the 0th index into the stack
	ans[0] = 1; //span of first element is 1
	for(int i = 1;i<n;i++){
		while (!s.empty() && day[s.top()] <= day[i]) 
		//pop the stack until all the elements in the stack has smaller values than current
		//when this loop breaks and we are at some index that index will refer to our NGL
            s.pop();
        if(s.empty())
        	ans[i] = i+1;
        else
        	ans[i] = i - s.top(); //s.top() acts as the NGL
        s.push(i);
	}
	for(int i= 0 ;i<n;i++)cout<<ans[i]<<" ";
}
