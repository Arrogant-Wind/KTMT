I. Cú pháp các lệnh logic** 

+ `and    Rd, Rs, Rt`     
_rd<- rs AND rt_
+ `andi   Rd, Rs, imm`    
_rd<- rs AND imm_
+ `or     Rd, Rs, Rt`      
_rd<- rs OR rt_
+ `ori    Rd, Rs, imm`     
_rd<- rs OR imm_
+ `nor    Rd, Rs, $0`     
_rd<-  NOT(rs)_
+ `nor    Rd, Rs, Rt`      
_rd<- rs NOR rt_
+ `xor    Rd, Rs, Rt`      
_rd<- rs XOR rt_
+ `xori   Rd, Rs, immed`    
_rd<- rs XOR imm_

>Ví dụ:  
$s1= 0100 0110 1010 0001 1100 0000 1011 0111  
$s2= 1111 1111 1111 1111 0000 0000 0000 0000  

>Sau khi thực hiện:  
and $s3, $s1, $s2  
or $s4, $s1, $s2  
xor $s5, $s1, $s2  
nor $s6, $s1, $s2  

>thu được kết quả:  
$s3= 0100 0110 1010 0001 0000 0000 0000 0000  
$s4= 1111 1111 1111 1111 1100 0000 1011 0111  
$s5= 1011 1001 0101 1110 1100 0000 1011 0111  
$s6= 0000 0000 0000 0000 0011 1111 0100 1000  


II. Một vài ứng dụng** 
1. Đặt lại 1 bit
+ nếu vị trí bit cần đặt là 1, ta lấy chuỗi đó AND với 1 chuỗi bit có '0' ở vị trí tương ứng cần đặt và các vị trí khác bằng '1'
++ ví dụ  
chuỗi 11011010 cần đặt lại vị trí 1:  
> ta có 1101 1010 . 1111 1101 = 1101 1000

+ nếu vị trí bit cần đặt là 0, ta lấy chuỗi đó OR với 1 chuỗi bit có '1' ở vị trí tương ứng cần đặt và các vị trí khác bằng '0'
++ ví dụ  
chuỗi 1101 1010 cần đặt lại vị trí 1:  
> ta có 1101 1000 + 0000 0100 = 1101 1100

2. Kiểm tra 1 bit
+ Muốn kiểm tra 1 bit ở vị trí bất kì, ta AND nó với chuỗi có '1' ở vị trí tương ứng, các vị trí còn lại bằng '0'
++ ví dụ
>1110 0110 · 0010 0000 = 0010 0000  
>1100 0110 · 0010 0000 = 0000 0000
3. 
