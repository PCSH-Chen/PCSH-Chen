## `Ciallo, World～(∠・ω< )⌒☆`
窩不知道要寫什麼，那就來快讀快寫吧（
```Cpp
void fastRead(int &x){
    int i = 0;
    char c;
    int d = 1;
    while(true){
        c = getchar();
        if(c<'0'||c>'9') break;
        i += (c-'0')*d;
        d*=10;
    }
    x = i;
    return;
}

void fastOut(int x){
    if(x<0) putchar('-'),x*=-1;
    if(x>9) fastOut(x/10);
    putchar(((x%10)+'0'));
}
```