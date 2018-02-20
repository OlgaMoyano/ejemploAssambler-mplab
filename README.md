# ejemploAssambler-mplab
list p=16f877a
#include<P16f877a.inc>
errorlevel -302
__CONFIG _WDT_OFF&_PWRTE_ON&_XT_OSC&_LVP_OFF&_CP_OFF
ORG 0x0000
;Variables de retardo, nos permitirán apreciar el conteo evitando que se realice a intervalos de tiempo muy rapidos.
valor1 equ h'21'
valor2 equ h'22'
valor3 equ h'23'
contador equ h'24'
;Hay que definir la asignación de segmentos apagados o encendidos, estas variables serán cargadas posteriormente.
;        HEXADECIMAL      BINARIO
CERO     EQU h'3F'   ;   01111110B
UNO      EQU h'06'   ;   01001000B
DOS      EQU h'5B'   ;   00111101B
TRES     EQU h'4F'   ;   01101101B
CUATRO   EQU h'66'   ;   01001011B
CINCO    EQU h'6D'   ;   01100111B
SEIS     EQU h'7D'   ;   01110111B
SIETE    EQU h'07'   ;   01001110B
OCHO     EQU h'7F'   ;   01111111B
NUEVE    EQU h'6F'   ;   01101111B
org 0h ;Reset
goto salidas

salidas:
       clrf PORTB
       clrf PORTC      ;Limpia puertos B y C para determinar que son salidas
       bsf STATUS,RP0 
       bcf STATUS,RP1 
       movlw h'0'
       movwf TRISB   
       movwf TRISC    
       bcf STATUS,RP0  ;ir al Banco 0
INICIO:     
       clrf contador   ;Inicia las decenas
       clrf PORTC      
LOOP:  
     movlw CERO        ;carga a w el valor de cero
       movwf PORTB
    call RETARDO
     movlw UNO
       movwf PORTB
       call RETARDO
     movlw DOS
       movwf PORTB
       call RETARDO
     movlw TRES
       movwf PORTB
       call RETARDO
     movlw CUATRO
       movwf PORTB
       call RETARDO
     movlw CINCO
       movwf PORTB
       call RETARDO
     movlw SEIS
       movwf PORTB
       call RETARDO
     movlw SIETE
       movwf PORTB
       call RETARDO
     movlw OCHO
       movwf PORTB
       call RETARDO
     movlw NUEVE
       movwf PORTB
       call RETARDO

       incf contador,1 ;Incrementa contador de decenas
       movlw h'A'
       xorwf contador,w
       btfsc STATUS,Z 
       goto  INICIO                                      
      
Decenas     
       movlw h'1'
       xorwf contador,w
       btfsc STATUS,Z  
       goto PRINT1
      
       movlw h'2'
       xorwf contador,w
       btfsc STATUS,Z 
       goto PRINT2

       movlw h'3'
       xorwf contador,w
       btfsc STATUS,Z  
       goto PRINT3

       movlw h'4'
       xorwf contador,w
       btfsc STATUS,Z  
       goto PRINT4

       movlw h'5'
       xorwf contador,w
       btfsc STATUS,Z  
       goto PRINT5
      
       movlw h'6'
       xorwf contador,w
       btfsc STATUS,Z   
       goto PRINT6

       movlw h'7'
       xorwf contador,w
       btfsc STATUS,Z   
       goto PRINT7

       movlw h'8'
       xorwf contador,w
       btfsc STATUS,Z   
       goto PRINT8

       movlw h'9'
       xorwf contador,w
       btfsc STATUS,Z  
       goto PRINT9
      

;Decenas en el display
PRINT1:
       movlw UNO       
       movwf PORTC
       goto LOOP
PRINT2:
       movlw DOS       
       movwf PORTC
       goto LOOP
PRINT3:
       movlw TRES       
       movwf PORTC
       goto LOOP
PRINT4:
       movlw CUATRO       
       movwf PORTC
       goto LOOP
PRINT5:
       movlw CINCO       
       movwf PORTC
       goto LOOP
PRINT6:
       movlw SEIS       
       movwf PORTC
       goto LOOP
PRINT7:
       movlw SIETE       
       movwf PORTC
       goto LOOP
PRINT8:
       movlw OCHO       
       movwf PORTC
       goto LOOP
PRINT9:
       movlw NUEVE       
       movwf PORTC
       goto LOOP

RETARDO
     movlw h'40'  ;Valor que  genera un retardo
     movwf valor1
tres movlw h'40'
     movwf valor2
dos  movlw h'40'
     movwf valor3
uno  decfsz valor3
     goto uno
     decfsz valor2
     goto dos
     decfsz valor1  
     goto tres
     return
  end
