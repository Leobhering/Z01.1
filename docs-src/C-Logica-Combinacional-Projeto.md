# C - Lógica Combinacional

![](figs/C-LogiComb/sistema-comb.svg)

!!! tip "Scrum Master"
    Você é `Scrum Master` e não sabe por onde começar? De uma olhada nessas dicas: [Vixi! Sou Scrum Master](Vixi!-Sou-Scrum-Master)

Esse projeto tem como objetivo trabalhar com portas lógicas e sistemas digitais combinacionais (sem um clock) em FPGA e VHDL. Os elementos lógicos desenvolvidos nessa etapa serão utilizados como elementos básicos para a construção do computador. 

## Instruções

O desenvolvimento será na linguagem VHDL. Os alunos deverão se organizar para implementar todos os elementos propostos. O facilitador escolhido será responsável pela completude e consistência do branch master do grupo.

Além dos módulos principais, deverá ser entregue um módulo que faz o acionamento de um display de sete segmentos.

### Integrantes

!!! warning 
    Este  projeto é para ser realizado 
    por todos os integrantes do grupo.
    
    Tarefas devem ser criadas no **Issues** e atribuídas aos demais colegas.
    As tarefas devem ser resolvidas individualmente! Utilize a ajuda de seus colegas, mas resolva o que foi atribuído a vocês, essa é sua tarefa/ responsabilidade! 
    
    

## Controle de Tarefas e Repositório

Nas discussões com os outros colegas o scrum master deve definir os módulos que você irá desenvolver. Crie uma rotina para commits e pull-request. Sempre teste os módulos e verifique se está fazendo o esperado.

### Facilitador (Scrum Master)

- Organizar o **github + issues + project**
- Fazer a **atualização** do fork com o upstream
- Gerenciar o grupo (atribuir tarefas)
- **Aceitar os pull-requests**
- Criar relatório da performance de cada um do grupo
- Entregar/Apresentar o projeto no final 

### Desenvolvedores

- Realizar as tarefas atribuidas pelo scrum-master
- Realizar os pull-requests
- Testar os códigos

## Instruções 

A pasta contém dois diretórios distintos : `src/` e `Quartus/`. O diretório `src` contém os arquivos fontes que deverão ser editados para implementar o projeto. O diretório `quartus/` contém o projeto que possibilitará compilar os módulos e testar em hardware.

### Entendendo o projeto

A pasta do projeto C no repositório `Z01.1` possui a seguinte estrutura :

```
/C-Logica-combinacional
    testeLogicaCombinacional.py
    /Quartus
    /src
        /rtl
            *.vhd
    /tests
        /tst
            *.vhd
```

1. `Quartus`: Projeto Quartus que faz uso dos arquivos VHDL localizados em `src/rtl/*.vhd`
1. `testeLogicaCombinacional.py`: Script em python que possibilita a execução dos testes
1. `src/rtl/*.vhd`: Arquivos VHDL que serão implementado pelo grupo
1. `tests/tst/*.vhd`: Arquivos VHDL que realizam teste lógico nos arquivos do rtl

### Executando o script de teste 

Abra o terminal na pasta `C-Logica-Combinacional` e execute o script python localizado nessa pasta:

```bash
$ ./testeLogicaCombinacional.py
```

<script id="asciicast-eolZDZIqCgTe3UQsX5jLrkF3D" src="https://asciinema.org/a/eolZDZIqCgTe3UQsX5jLrkF3D.js" async></script>

!!! note
    No exemplo de teste verificamos que aimplementação da `nand` está errada.

## Módulos

- [ ] Implementar todos os módulos listados
- [ ] Todos os módulos devem passar nos testes
- [ ] Travis deve estar configurado e funcionando
- [ ] Implementar acionamento do diplay de 7 segmentos e demonstrar na FPGA

!!! note 
    Esses arquivos estão localizados em `C-Logica-Combinacional/src/rtl/`

!!! tip
    Utilize o VScode para editar os arquivos vhdl e valide a implementação executando o script de testes.

Deve-se implementar os seguintes circuitos combinacionais: 

- AND 16 bits
    - **Arquivo**   : `And16.vhd`
    - **Descrição** : And bit a bit entre duas palavras de 16 bits.
 
- OR de 16 bits
    - **Arquivo**   : `Or16.vhd`
    - **Descrição** : OR bit a bit entre duas palavras de 16 bits.
 
- NOT de 16 bits
    - **Arquivo**   : `Not16.vhd`
    - **Descrição** : NOT bit a bit entre duas palavras de 16 bits.
    
- NOR 8 Way 
    - **Arquivo**   : `Nor8Way.vhd`
    - **Descrição** : NOR entre 8 bits, resulta em uma única saída
    
- OR 8 Way  
    - **Arquivo**   : `Or8Way.vhd`
    - **Descrição** : OR entre 8 bits, resulta em uma única saída
 
- Demultiplexiador de 2 saídas 
    - **Arquivo**   : `DMux2Way.vhd`
    - **Descrição** : Demultiplexa uma entrada binária em duas saídas.
    
- Demultiplexiador de 4 saídas
    - **Arquivo**   : `DMux4Way.vhd`
    - **Descrição** : Demultiplexa uma entrada binária em quatro saídas.
    
- Demultiplexiador de 8 saídas
    - **Arquivo**   : `DMux8Way.vhd`
    - **Descrição** : Demultiplexa uma entrada binária em oito saídas.
    
- Multiplexador de duas entradas de 16 bits 
    - **Arquivo**   : `Mux16.vhd`
    - **Descrição** : Multiplexa duas entradas de 16 bits para uma de 16 bits.
    
-  Multiplexador 2 entradas de um bit cada
    - **Arquivo**   : `Mux2Way.vhd`
    - **Descrição** : Multiplexa 2 entradas binárias em uma saída binária
    
-  Multiplexador 4 entradas de um bit cada
    - **Arquivo**   : `Mux4Way.vhd`
    - **Descrição** : Multiplexa 4 entradas binárias em uma saída binária
    
-  Multiplexador 8 entradas de um bit cada
    - **Arquivo**   : `Mux8Way.vhd`
    - **Descrição** : Multiplexa 8 entradas binárias em uma saída binária
    
-  Multiplexador 4 entradas de 16 bits cada
    - **Arquivo**   : `Mux4Way16.vhd`
    - **Descrição** : Multiplexa 4 entradas de 16 bits cada em uma saída de 16 bits.
    
-  Multiplexador 8 entradas de 16 bits cada
    - **Arquivo**   : `Mux8Way16.vhd`
    - **Descrição** : Multiplexa 8 entradas de 16 bits cada em uma saída de 16 bits.

- Display de 7s
    - **Arquivo**: `/src/toplevel.vhd'
    - **Descrição**: Deve ler as chaves da FPGA SW e exibir seu valor no display de 7s (Hexa, Decimal).

!!! warning "Display 7s"
    Esse módulo não possui teste unitário, deve-se utilizar a FPGA para validar.

!!! tip "Display 7s"
    Esse item é uma continuação do que foi realizado no [laboratório 5](/C-Logica-Combinacional-Lab-1/), onde vocês tiveram
    que exibir um valor constante no display de 7s. 
    
    Para cada segmento do display, vocês devem encontrar uma equação booleana que o represente, e então implementar em VHDL e 
    testar na FPGA.

!!! note "Dicas VHDL"
    Existem diversos locais onde podem tirar dúvida de `VHDL`, por exemplo : 

    - :+1: http://esd.cs.ucr.edu/labs/tutorial/
    - https://courseware.ee.calpoly.edu/cpe-169/Misc_stuff/cheat_sheet.pdf
    - https://www.ics.uci.edu/~jmoorkan/vhdlref/vhdl_golden_reference_guide.pdf


## Rubricas para avaliação do projeto

Cada integrante do grupo irá receber duas notas: Uma referente ao desenvolvimento total do projeto (Projeto) e outra referente a sua participação individual no grupo.

### Grupo

Para atingir os objetivos A e B, deve-se antes atingir o C.

| Conceito | Descritivo                                                             |
|----------|------------------------------------------------------------------------|
| **A**    | Exibe três dígitos em Decimal                                          |
| **B**    | Exibe três dígitos em Hexadecimal                                      |
|          | (exibir até o valor 0x3FF = 2^10 - 1)                                  |
| **C**    | Ter criado o project no github                                         |
|          | O travis configurado e funcionando                                     |
|          | Todos os módulos implementados e funcionado (teste ok)                 |
|          | **Implementando um único display de 7s (conta até 16 em hexadecimal)** |
| **D**    | Até três Módulos com falha                                             |
| **I**    | Mais de três módulos com falha                                         |

### Individual

As rubricas a serem seguidas serão comuns a todos os projeto e está descrito no link:

- [Rubricas Scrum e Desenvolvedor](/Sobre-Rubricas/)
