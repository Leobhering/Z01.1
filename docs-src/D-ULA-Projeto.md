# D - ULA

![ULA](figs/D-ULA/D-sistema-ula.png)

Neste projeto seu grupo terá que desenvolver os componentes para a implementação de uma unidade lógica e aritmética (ULA) de 16 bit (proposta pelo livro texto) que será capaz de realizar operações binárias muito simples porém que possibilitará realizarmos muitas coisas!

!!! note 
    Nas discussões com o grupo, o scrum master deverá definir 
    os módulos que cada integrante irá desenvolver. 
    Crie uma rotina para commits e pull-requests.
  
!!! tip
    Você é `Scrum Master` e não sabe por onde começar? 
    De uma olhada nessas dicas:
    [Vixi! Sou Scrum Master](Vixi!-Sou-Scrum-Master)
    
!!! tip
    Sempre teste os módulos e verifique se está funcionando como o esperado.

## Instruções 

A pasta do projeto D, no repositório Z01, possui a seguinte estrutura:

```bash
/D-ULA
    testeULA.py
    programFPGA.py
    /Quartus
    /src
        /rtl
            *.vhd
    /tests
        /tst
            *.vhd
```

1. Quartus: Projeto Quartus que faz uso dos arquivos VHDL localizados em src/rtl/*.vhd;
1. testeULA.py: Scripts em python que automatizam a execução dos testes;
1. src/rtl/*.vhd: Arquivos VHDL que serão implementados pelo grupo;
1. tests/tst/*.vhd: Arquivos VHDL que realizam o teste lógico nos arquivos do rtl.

### Executando o Script de Teste 

Abra o terminal na pasta `D-UnidadeLogicaAritmetica/`  e execute o script python localizado nessa pasta:

```bash
$ ./testeULA.py
```

O mesmo irá compilar os arquivos `src/rtl/*.vhd` e executar os testes unitários em cada um deles. Nesse momento do teste, como os módulos não estão implementados, o resultado deverá ser falho.

Esse comando executa um teste unitário em cada um dos módulos, verificando se sua implementação está correta. O resultado é exibido na tela como : **pass** ou **fail**.

# O que deve ser feito: 

Além de implementar os módulos, deve-se gerar uma imagem com a forma de onda desse módulo. Para cada nova implementação deve-se criar um novo branch e remover o comentário do arquivo: `tests/config.txt` somente o módulo que está sendo implementado. 

Note que é possível reaproveitar, via **port map**, os módulos do projeto anterior (C). Esses módulos anteriores, já são incluídos, automaticamente (pelo script), na compilação dos módulos do projeto D.

## Módulos 

!!! note
    Esses arquivos estão localizados em `D-UnidadeLogicaAritmetica/src/rtl/`

Deve-se implementar os seguintes circuitos combinacionais:

- HalfAdder
    - **Arquivo**   : `HalfAdder.vhd`
    - **Descrição** : Adiciona dois bits que resulta em um bit de soma e outro de carry out.
    - **Dependência**: Não tem.
 
- FullAdder
    - **Arquivo**   : `FullAdder.vhd`
    - **Descrição** : Adiciona três bits, dois referentes às entradas e o outro referente ao carry in. O resultado é um bit com a soma e outro com o carry out.
     - **Dependência**: Não tem.

- Add16
    - **Arquivo**   : `Add16.vhd`
    - **Descrição** : Adiciona dois vetores de 16 bits resultando em um vetor de 16 bits (sem carry out do bit mais significativo - MSB).
    - **Dependência**: `FullAdder`
  
- Inc16 
    - **Arquivo**   : `Inc16.vhd`
    - **Descrição** : Adiciona '1' a um vetor de 16 bits resultando em um vetor de 16 bits (sem carry out do MSB).
    - **Dependência**: `Add16`
    
- Inversor16 
    - **Arquivo**   : `Inversor16.vhd`
    - **Descrição** : Inverte um vetor de entrada quando o bit de controle **n** (nx ou ny) for igual a '1', e não modifica o vetor de entrada caso contrário. O resultado é um novo vetor de 16 bits.
    - **Dependência**: Não tem.
    
- Zerador16
    - **Arquivo**   : `Zerador16.vhd`
    - **Descrição** : Zera um vetor de entrada quando o bit de controle **z** (zx ou zy) for igual a '1'. Não modifica o vetor de entrada se o bit for '0'. O resultado é um novo vetor de 16 bits.
    - **Dependência**: Não tem.
    
- Comparador16
    - **Arquivo**   : `Comparador16.vhd`
    - **Descrição** : Verifica se o vetor de saída (16 bits) é igual a zero (**zr**) e se menor que Zero (**ng**). Caso igual a zero, faz com que o sinal **zr** seja igual a '1' e caso contrário '0'. Se o sinal de entrada for negativo faz com que **ng** receba '1' e '0' caso contrário.
    - **Dependência**: Não tem.
    
Pseudo código :

```python
if(a == 0):
  zr = 1
else:
  zr = 0
  
if (a < 0):
  ng = 1
else:
  ng = 0
```
    
- ALU
    - **Arquivo**   : `ALU.vhd`
    - **Descrição** : A entidade que faz o mapeamento de todas as demais, interligando os blocos (zerador, comparador, inversor, Add ....) em um único bloco.
    - **Dependência**: `Comparador16`, `Zerador16`, `Inversor16`, `Add16`, 

Para implementar a ALU será necessário usar os blocos desenvolvidos neste projeto e os blocos desenvolvidos no projeto anterior: And16, Mux16. O script de compilação e teste já faz a inclusão deles. A arquitetura da ULA pode ser vista abaixo:

![ULA](figs/D-ULA/D-ula.png)

## Forma de onda

Para cada teste realizado, deve-se carregar a interface gráfica e tirar um print da forma de onda do módulo com os testes aplicados a ele ([lab 8](D-ULA-Lab-1)). Essa imagem deve ser salva na mesma pasta dos arquivos VHDL (src/rtl/) e com o mesmo nome dos módulos. A pasta no final do projeto deve possuir os seguintes arquivos:

``` bash
/src/rtl/
         Add16.vhd
         Add16.png
         ALU.vhd
         ALU.png
         Comparador16.vhd
         Comparador16.png
         FullAdder.vhd
         FullAdder.png
         HalfAdder.vhd
         HalfAdder.png
         Inc16.vhd
         Inc16.png
         Inversor16.vhd
         Inversor16.png
         Zerador16.vhd
         Zerador16.png
```

## Testando em HW

Para testar os módulos em hardware, deve-se abrir o projeto (D-UnidadeLogicaAritmetica/Quartus). Ele já inclui todos os módulos desta entrega e também os módulos da entrega passada. O arquivo localizado em /rtl/toplevel.vhd já faz o mapeamento dos pinos da FPGA para os pinos da ULA (como no [lab 9](D-ULA-Lab-2)). Para testar no hardware basta compilar e programar a FPGA.

# Rubricas para avaliação de projetos

Cada integrante do grupo irá receber duas notas: uma referente ao desenvolvimento total do projeto (Projeto) e outra referente a sua participação individual no grupo (que depende do seu papel).

## Projeto

| Conceito |                                                                                                      |
|----------|------------------------------------------------------------------------------------------------------|
| I        | - Não implementou os módulos Add16, ULA, Comparador, FullAdder, HalfAdder, Inc16, Inversosr, Zerador.|
|          |                                                                                                      |
| D        | - Implementou todos os módulos menos a ULA.                                                          |
|          |                                                                                                      |
| C        | - Configurou o travis e funcionou.                                                                   |
|          | - Todos os testes passaram (ok).                                                                     |
|          | - ULA funcionando.                                                                                   |
|          | - Todos os módulos sendo testados no Travis.                                                         |
|          | - Possui a forma de onda de todos os módulos (.png).                                                 |
|          |                                                                                                      |
| B        | - Compila no Quartus a ULA do grupo e fez um vídeo demonstrando o seu funcionamento (FPGA). |      
|          |   O vídeo pode estar no git (se for pequeno) ou hospedado em algum site    |
| | |
| A        | - Modifica a ULA incluindo uma instrução a mais (exe: shift left/right)            |

## Desenvolvedor e Scrum Master

As rubricas a serem seguidas serão comuns a todos os projeto e está descrito no link :

 - [Rubricas Scrum e Desenvolvedor](/Sobre-Rubricas/)

