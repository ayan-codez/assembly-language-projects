# Palestine Flag – Assembly Language

This project draws the Palestinian flag using Assembly Language.

## Features
- Demonstrates CPU flags and graphics
- Draws colored flag blocks
- Uses loops and memory handling

## Tools
- EMU8086 / DOSBox
- Assembly Language (x86)

## How to Run
1. Open `palestine_flag.asm` in EMU8086
2. Compile and run the program
3. Observe the Palestinian flag output

## Author
Muhammad Ayan Tahir
##Code
    .model small
.stack 100h

.data
   
    tri_widths db 2, 4, 6, 8, 10, 12, 12, 10, 8, 6, 4, 2

.code
    mov ax, @data
    mov ds, ax
    
  
    mov ax, 0003h
    int 10h

    mov ax, 0xb800      
    mov es, ax 

    mov ax, 1020h       
    xor di, di          
    mov cx, 2000        
    cld
    rep stosw

 
    mov di, 350       
    mov cx, 22       
    call drawPole       

    

  
    mov di, 352        
    mov ax, 0020h    
    call drawStripeBlock

   
    mov ax, 7020h      
    call drawStripeBlock

   
    mov ax, 2020h      
    call drawStripeBlock

   
    
    mov di, 352         
    lea si, tri_widths  
    mov cx, 12          

drawTriangleLoop:
    push cx           
    push di             

 
    xor ax, ax          
    lodsb              
    mov cx, ax         

 
    mov ax, 4020h     
    rep stosw           

    pop di              
    add di, 160         
    
    pop cx             
    loop drawTriangleLoop

    mov ah, 07h    
    int 21h        

    MOV AH, 4Ch                     
    INT 21H

drawStripeBlock proc
    mov cx, 4           
stripe_loop:
    push cx             
    push di             
    
    mov cx, 26          
    rep stosw           
    
    pop di              
    add di, 160       
    pop cx              
    loop stripe_loop    
    ret
drawStripeBlock endp

drawPole proc
    mov ax, 6020h       
poleLoop:
    stosw               
    add di, 158         
    loop poleLoop
    ret
drawPole endp

end
