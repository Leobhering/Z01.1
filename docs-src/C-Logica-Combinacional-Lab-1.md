# C - Lógica Combinacional - parte 1

!!! note
    Por favor, realizar em trio ou dupla

!!! linux
    Usar o Linux fornecido!

!!! warning "Scrum Master"
    Atualize o repositório com o upstream antes de começar!

!!! tip 
    Você é `Scrum Master` e não sabe por onde começar? De uma olhada nessas dicas: [Vixi! Sou Scrum Master](Vixi!-Sou-Scrum-Master)

!!! tip "Antes de começar!"
    Após clonar o repositório devemos baixar e atualizar a infra necessária para o curso, ainda no terminal, vá para a pasta do repositório:

    ```bash
    $ cd Z01.1-NomeDoGrupo/
    $ ./updateZ01tools.sh
    ```

    Isso irá baixar as dependências phython (via pip) e também clonar um repositório chamado `Z01-Tools` na raiz do usuário: `$HOME/Z01-Tools/`.


Nesse lab iremos pela primeira vez programar uma FPGA e começar a trabalhar com uma linguagem de descrição de hardware (HDL), o VHDL.

## VHDL

Esse laboratório é introdutório para o desenvolvimento do projeto ([`C Lógica Combinacional`](C-Logica-Combinacional-Projeto)), vamos criar o nosso primeiro código em VHDL e em seguida, programar a FPGA para executar o hardware recém descrito.

Após essa etapa, iremos começar o desenvolvimento do projeto, programando os módulos que virão a ser utilizados no computador Z01.

### Entendendo a estrutura de pastas

A pasta do projeto C (`C-LogicaCombinacional`) no repositório Z01 possui a seguinte estrutura:

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

1. `Quartus`: Projeto Quartus que faz uso dos arquivos VHDL localizados em src/rtl/*.vhd 
     - Serve para programar a **FPGA**
1. `*.py`: Scripts em python automatiza a execução dos testes
1. `src/rtl/*.vhd`: Arquivos VHDL que serão implementado pelo grupo
1. `tests/tst/*.vhd`: Arquivos VHDL que realizam teste lógico nos arquivos do rtl
1. `tests/config.txt`: Configuração dos testes

### Abrindo o Quartus

!!! linux
    Se não encontrar o software abra o terminal e escreva `quartus` :arrow_right: `enter`.

Abra o software do  `Quartus` ![](figs/C-LogiComb/quartusIcon.png){ width=30px} e clique em `File` :arrow_right: `Open Project` :arrow_right: escolha o projeto localizado na pasta `C-Logica-Combinacional/Quartus`.

O arquivo que o Quartus irá reconhecer é o: `DE0_CV_Default.qpf` como no gif a seguir:

![Abrindo o Quartus](figs/C-LogiComb/Quartus1.gif)

Abra o arquivo `TopLevel.vhd` como demonstrado no gif anterior, este arquivo é o que chamamos de [top level](https://www.xilinx.com/support/documentation/sw_manuals/xilinx10/isehelp/pfp_p_toplevelhdl.htm) (pode-se fazer uma analogia com o `main` de um código), ele será o primeiro a ser executado na compilação e utilizará os demais módulos do sistema.

Um código em VHDL possui basicamente três partes:

1. Declaração de bibliotecas utilizadas

```vhdl
library ieee;
use ieee.std_logic_1164.all;
use ieee.numeric_std.all;
use work.all;
```

2. Declaração das entradas e saídas desse bloco (entidade)

```vhdl
entity TopLevel is
  port(
        SW   : in  std_logic_vector(9 downto 0);
        LEDR : out std_logic_vector(9 downto 0)
  );
end entity;
```

3. Implementação da lógica que relaciona as entradas e saídas do módulo (arquitetura)

```vhdl
architecture rtl of TopLevel is

begin


end rtl;
```

![](figs/C-LogiComb/entity.png)

O código original disponível não realiza nenhuma lógica. Note que sua arquitetura está vazia!

### Compilando o código

Para compilarmos esse código VHDL basta irmos em: `Processing` :arrow_right: `Start Compilation`. A ferramenta irá "realizar" o código, ou seja, interpretar e torna-lo um hardware.

![Compilando](figs/C-LogiComb/Quartus2.gif)

### RTL View

Podemos gerar a visão rtl do código em vhdl, esse diagrama é a interpretação do código em VHDL pelo compilador e como ele seria supostamente implementando em hardware. Para isso: 

`Tools` :arrow_right: `Netlist Viewers` :arrow_right: `RTL viewer`

Ele irá gerar o seguinte diagrama:

![Compilando](figs/C-LogiComb/Quartus3.png)

Onde podemos analisar que não existe nenhuma lógica que relaciona entrada com saída.

### Modificando o projeto

Vamos modificar o arquivo `toplevel.vhd` do projeto para ficar como:

```vhdl
---------------
-- implementacao
---------------
begin
 
  LEDR(0) <= SW(0);

end rtl;
```

``` diff
+ 1. Compile
+ 2. Gere o RTL Viewer novamente
```

O resultado deve ser o seguinte:

![Compilando](figs/C-LogiComb/Quartus-rtl2.png)

Onde o valor do `LEDR0` será o próprio valor de entrada chave `SW0`.

### Programando a FPGA

Para programar na FPGA conecte-a ao seu computador via cabo USB e vá em: `Tools` :arrow_right: `Programmer`. Ele deve abrir uma nova interface:

![Programando](figs/C-LogiComb/quartus-pgr.gif)

!!! tip "Testando"
    Brinque com as chaves e note que os LEDs irão acender conforme as chaves são colocadas na posição on.

## Exercício

Para cada desafio proposto a seguir, verifique se o RTL corresponde a lógica que deseja implementar. Após a verificação teste na programe e teste na FPGA:

1. Compile
1. Verifique o RTL
1. Programe a FPGA
    
!!! question "Exercício 1"
    1. Faça a saída LEDR(0) ser o inverso da entrada SW(0)

!!! question "Exercício 2" 
    Faça a saída LEDR(0) ser a entrada SW(0) ou SW(1)

!!! question "Exercício 3"
    Faça a saída LEDR(0) ser a entrada SW(0) ou SW(1) e o LEDR(1) ser a chave SW(1)

!!! question "Exercício 4"

    Note que na nossa FPGA possuímos seis [displays de sete segmentos](https://en.wikipedia.org/wiki/Seven-segment_display). 

    ![](figs/C-LogiComb/7seg.png)

    Para termos acesso a esses displays, basta modificar a entidade do projeto para:

    ```vhdl
    entity TopLevel is
        port(
            SW      : in  std_logic_vector(9 downto 0);
            HEX0    : out std_logic_vector(6 downto 0); -- 7seg0
            HEX1    : out std_logic_vector(6 downto 0); -- 7seg1
            HEX2    : out std_logic_vector(6 downto 0); -- 7seg2
            HEX3    : out std_logic_vector(6 downto 0); -- 7seg3
            LEDR    : out std_logic_vector(9 downto 0)
        );
    end entity;
    ```

    Agora com os 7segs mapeados como saída (`out`) na nossa `entity` podemos acionar cada led do display, como descrito no manual da placa (isso só é possível pois o projeto já foi configurado corretamente antes pelo seu professor):

    ![](figs/C-LogiComb/7seg-manual.png)

    - Faça aparecer o número `5` no `HEX0`.

## Adicionando um novo componente ao projeto

O desenvolvimento de projetos de hardware assim como os de softwares devem ser feitos de forma modular, onde especifica-se e implementa-se pequenos módulos (entidades) que são combinadas em sistemas cada vez mais complexos até chegar ao `TopLevel`.

Esse projeto define uma série de pequenos módulos, um com sua especificidade (localizados em `C-LogicaCombinacional/src/rtl/`) :

- And16.vhd
- DMux2Way.vhd
- DMux4Way.vhd
- DMux8Way.vhd
- Mux16.vhd
- Mux2Way.vhd
- Mux4Way16.vhd
- Mux4Way.vhd
- Mux8Way16.vhd
- Mux8Way.vhd
- [`Nand.vhd`](https://github.com/Insper/Z01.1/blob/master/Projetos/C-LogicaCombinacional/src/rtl/Nand.vhd)
- Nor8Way.vhd
- Not16.vhd
- Or16.vhd
- Or8Way.vhd
- TopLevel.vhd

O módulo [`Nand.vhd`](https://github.com/Insper/Z01.1/blob/master/Projetos/C-LogicaCombinacional/src/rtl/Nand.vhd) que já está implementando para vocês, possui o seguinte conteúdo:

```vhdl
Library ieee;
use ieee.std_logic_1164.all;

entity nand_z01 is
   port(
      A : in  std_logic;
      B : in  std_logic;
      Q : out std_logic
   );
end nand_z01;

architecture rtl of nand_z01 is
begin
   q <= not (a and b);
end rtl;
```

!!! tip
    Note que o VHDL não é case sensitive (nand = NAND = nAnD = ...)

Esse módulo é uma entidade que possui duas entrada (a,b) e uma saída (q) e implementa um `nand` entre as entradas.

### Inserindo no `toplevel` 

Podemos inserir essa `nand` no `toplevel` da seguinte maneira:

``` vhdl
begin
 
  u1 : work.nand_z01 port map(A => SW(0), 
                              B => SW(1), 
                              Q=> LEDR(0)
                              );

end rtl;
```

Essa linha de código pode ser lida como:

> Cria um componente chamada de **u1**, mapeando (roteando) a entrada `SW(0)` na porta **A** da `NAND` e a entrada `SW(1)` na entrada **B** da `NAND` e a saída **Q** mapeada para o LEDR(0)

Compilando o projeto podemos analisar o RTL gerado:

![RTL NAND TopLevel](figs/C-LogiComb/quartus-nand.png)

![RTL NAND Expandido](figs/C-LogiComb/quartus-nand2.png)

## Desafios extras

Realize os seguintes desafios junto com o seu grupo, siga os passos anteriores para conseguir rodar na FPGA.

!!! question "Exercício 5"
    Faça TODOs os LEDs acenderem quando a seguinte combinação de entrada for:
  
    ```
    SW9               SW0
      1 0 0 1 1 0 1 0 1 0
    ```

!!! question "Exercício 6"
    Faça um código VHDL para implementar o circuito a seguir:

    ![Circuito](figs/C-LogiComb/circuito.png)

    Sendo:

    - X: chave 0 (SW(0))
    - y: chave 1 (SW(1))
    - z: chave 2 (SW(2))
