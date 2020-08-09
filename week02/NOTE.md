学习笔记
有限状态机同一时刻只能处于一个状态。
mealy状态机根据不同的输入有不同的输出，moore状态机下一个状态是固定的。
function match(str){
    state = findA;
    for (let c of str){
        state = state(c)
    }
    return state === end;
}


function findA(val){
    if(val==='a'){
        return findB
    }else {
        return findA
    } 
}

function findB(val){
    if(val==='b'){
        return end
    } else {
        return findA
    }
}

function end(){
    return end;
}

第一步
HTTP请求总结：
设计一个HTTP请求的类
conten type是一个必要的字段，要有默认值
body是KV格式（key-value）
不同的content-type影响body的格式

第二步
send函数总结：
在Request的构造器中收集必要的信息
设计一个send函数，把请求真实发送到服务器
send函数应该是异步的，所以返回Promise

第三步
发送请求：
设计支持已有的connection或者自己新建的connection
收到数据传给parser
根据parser的状态resolve Promise

第四步
responseParser:
response必须分段构造，所有我们要用一个responseParser来装配
responseParser分段处理ResponseText，我们用状态机来分析文本的结构

第五步
BodyParser
reponse的body可能根据content-type有不同的结构，因此我们会采用子parser的结构来解决问题
以TrunkedBodyParser为例，我们同样采用状态机来处理body的格式；