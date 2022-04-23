# Win or Tail Decision Machine
# 邏設實驗_HW3_資二(2)_鄭宇傑

### 實驗目的 :

>### 先用if else設計四人投票機，後使用case改寫

### 實驗材料 :

>### EDAplayground及相關環境

### 實驗步驟 :

>### 1.先用if else設計投票機
```verilog=
module voter_if (I, O);
input [3:0] I; 
output [3:1] O; 
reg [3:1] O;

always@ (I)
begin
    if (I == 4'b0000)
        O[3] = 1;
    else if (I == 4'b0001)
        O[3] = 1;
    else if (I == 4'b0010)
        O[3] = 1;
    else if (I == 4'b0100)
        O[3] = 1;
    else if (I == 4'b1000)
        O[3] = 1;
    else
        O[3] = 0;

    if (I == 4'b0011)
        O[2] = 1;
    else if (I == 4'b0101)
        O[2] = 1;
    else if (I == 4'b0110)
        O[2] = 1;
    else if (I == 4'b1001)
        O[2] = 1;
    else if (I == 4'b1010)
        O[2] = 1;
    else if (I == 4'b1100)
        O[2] = 1;
    else
        O[2] = 0;

    if (I == 4'b1110 || I == 4'b1101 || I ==4'b1011 || I == 4'b0111 || I == 4'b1111)
        O[1] = 1;
    else
        O[1] = 0;

end
endmodule
```
>### testbench
```verilog=
module voter_if_tb;
reg [3:0] I_tb;
wire  [3:1] O_tb;
voter_if voter_1(.I(I_tb),.O(O_tb));
initial
begin
    #160 $finish;
end
initial
begin
    #0   I_tb = 4'b0000;
    #10  I_tb = 4'b0001;
    #10  I_tb = 4'b0010;
    #10  I_tb = 4'b0011;
    #10  I_tb = 4'b0100;
    #10  I_tb = 4'b0101;
    #10  I_tb = 4'b0110;
    #10  I_tb = 4'b0111;
    #10  I_tb = 4'b1000;
    #10  I_tb = 4'b1001;
    #10  I_tb = 4'b1010;
    #10  I_tb = 4'b1011;
    #10  I_tb = 4'b1100;
    #10  I_tb = 4'b1101;
    #10  I_tb = 4'b1110;
    #10  I_tb = 4'b1111;
end
initial
begin
    $dumpfile("0408.vcd");
    $dumpvars(0, voter_1);
end
endmodule
```
>### Makefile
```verilog=
VERILOG = iverilog
TARGET = test0408.vcd
TEMP = test0408.vpp

$(TARGET) : $(TEMP)
	vvp $(TEMP)

$(TEMP): 0408_tb.v 0408.v
	$(VERILOG) -o $(TEMP) 0408_tb.v 0408.v

clean:
	rm $(TARGET)
```
>### 2.使用case改寫
```verilog=
module voter_if (I, O);
input [3:0] I; 
output [3:1] O; 
reg [3:1] O;

always@ (I)
case (I)    
    4'b0000 :
        O[3] = 1;
    4'b0001 :
        O[3] = 1;
    4'b0010 :
        O[3] = 1;
    4'b0100 :
        O[3] = 1;
    4'b1000 :
        O[3] = 1;
    default :
        O[3] = 0;
endcase

always@ (I)
case (I)   
    4'b0011 :
        O[2] = 1;
    4'b0110 :
        O[2] = 1;
    4'b1100 :
        O[2] = 1;
    4'b1001 :
        O[2] = 1;
    4'b1010 :
        O[2] = 1;
    4'b0101 :
        O[2] = 1;
    default :
        O[2] = 0;
endcase

always@ (I)
case (I)   
    4'b1110 :
        O[1] = 1;
    4'b1101 :
        O[1] = 1;
    4'b1011 :
        O[1] = 1;
    4'b0111 :
        O[1] = 1;
    4'b1111 :
        O[1] = 1;
    default :
        O[1] = 0;
endcase
    
endmodule
```
### 實驗結果 : 
![](https://i.imgur.com/KYurluo.png)
### 實驗討論 : 
寫testbench不是這麼的順利，但查了一下資料與同學的幫助成功完成。
### 實驗心得 : 
>一開始改寫會一直卡住且失敗，但在不斷嘗試跟理解下，慢慢進入狀況，最後成功寫出來，也對verilog的語法更熟悉了。
### 參考文獻 : 
>數位邏輯實習智慧大師之Lecture_5
### Github連結 : 
[1410932066_hw3](https://github.com/s1410932066/HW3.git)
