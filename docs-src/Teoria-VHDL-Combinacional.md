# VHDL - Combinacional

Em sistemas digitais, lógica combinacional é aquela que não depende do estado anterior (não possui memória), podemos classificar portas lógicas (and, or, nand ...), mux, demux, comparadores, full address e outros componentes como sendo do tipo combinacional.

!!! note
    Logic is combinational if outputs at a specified time are a function only of the inputs at that time. Examples of combinational logic functions are decoders, multiplexers, and adders.
    ...
    
    > Trecho extraído do site da [intel](https://www.intel.com/content/www/us/en/programmable/quartushelp/13.0/mergedProjects/hdl/vhdl/vhdl_pro_combinatorial.htm)

## VHDL

Existem duas formas de descrevermos um circuito combinacional em VHDL, uma delas é utilizando o `process`. Não iremos tratar dessa alternativa nesse documento.

!!! note
    O uso de `process` pode confundir vocês nesse primeiro momento, por parecer um função de um programa.

Para transcrevermos uma lógica combinacional em VHDL basta escrever a implementação 

### Equações

Podemos escrever equações em VHDL utilizando os seguintes operadores: `not`, `and`, `or`, `nor`, `xor`, `xnor`. Como no exemplo a seguir:

$X = (\bar{A} . B) + C)$

Transcrevemos para

```vhdl
X <= ((not A) and B) or C
```

!!! tip 
    Abuse dos parenteses () para explicitar o que quer fazer, por exemplo:
    
    ```
    not A and B ... not (A and B) ... (not A) and B
    ```

!!! tip
    Quando desenvolvemos projetos para FPGA não tem a necessidade de simplificarmos a equação lógica, a ferramenta (`Quartus`) faz isso para a gente.

### Concatenate

Em VHDL podemos concatenar bit para formar vetores, isso é feito da seguinte forma:



### with


### when


