---
title: 用 C++ 模擬簡單的 8-bit cpu
date: 2022-11-05 23:13:30
cover:
top_img:
categories:
    - 計算機科學
tags:
    - C++
    - 'Computer Architecture'
    - Assembly Language
---
最近在看 beneater 的 8-bit cpu 想說用 C++ 寫看看練練手，所以就寫出來啦~
由於還沒對 CPU 理解得很徹底，只有把ALU做出來而已，以後再看看會不會在重寫一個哈哈。

# 架構
- accumulator register
- b register
- instruction register
- program counter

# 程式碼
```cpp
#include<bits/stdc++.h>
#include<stdio.h>

using byte=uint8_t;

byte accumulator; // accumulator register
byte b; // register b
byte instruction; // instruction register
byte counter; // program counter

bool negitive; // negitive flag
bool sign; // sign flag

bool HLT=0;

byte memory[256]={0b11110000};

bool isDebug=0;

void reset(){
    accumulator=0;
    b=0;
    counter=0;
    instruction=0;
    for(int i=0;i<256;i++) memory[i]=0b11110000;
}

void fetch(){
    if(HLT) return;
    instruction=memory[counter];
    counter+=1;
}

void STA(){
    if(isDebug) printf("%#4x STA: %#x\n",counter,memory[counter]);
    accumulator=memory[counter];
    counter+=1;
}

void STB(){
    if(isDebug) printf("%#4x STB: %#x\n",counter,memory[counter]);
    b=memory[counter];
    counter+=1;
}

void ADD(){
    if(isDebug) printf("%#4x ADD: %#x\n",counter,memory[counter]);
    b=memory[counter];
    accumulator+=b;
    counter+=1;
}

void OUT(){
    if(isDebug) printf("%#4x OUT\n",counter);
    printf("%#4x\n",accumulator);
}

void decode(){
    instruction/=16;
    if(isDebug) printf("%#4x instruction: %#x\n",counter-1,instruction);
    switch(instruction){
        case 0x0001:    // STA
            STA();            
            break;

        case 0b0010:    // LDA
            break;

        case 0b0011:    // STB
            STB();
            break;

        case 0b0100:    // LDB
            break;

        case 0b0101:    // ADD
            ADD();
            break;

        case 0b1101:    // OUT
            OUT();
            break;

        case 0b1110:    // HLT
            if(isDebug) printf("%#4x HLT\n",counter);
            HLT=1;
            break;

        case 0b1111:    // NOP
            if(isDebug) printf("%#4x NOP\n",counter);
            break;
    }
}


void print_register(byte reg){
    for(int i=0;i<8;i++){
        printf("%u",reg/128);
        reg*=2;
    }
}

void print_memory(byte address){
    for(int i=0;i<8;i++){
        printf("%u",memory[address]/128);
        memory[address]*=2;
    }
}

void debug(){
    if(!isDebug) return; 
    printf("\n%4#x  ",counter);
    printf("%4#x\n",memory[counter]);
    printf("register:\n");
    printf("%14s %4#x\n","accumulator",accumulator); 
    printf("%14s %4#x\n","b",b);
    printf("%14s %4#x\n","instruction",instruction);
}

int main(){
    reset();
    memory[0]=0b00010000;   // LDA   
    memory[1]=0b00000001;
    memory[2]=0b01010000;   // ADD
    memory[3]=0b00000001;
    memory[4]=0b11010000;   // HLT
    memory[5]=0b11100000;

    while(!HLT){
        // fetch
        //debug();
        fetch();
        decode();
    }
    return 0;
}

```