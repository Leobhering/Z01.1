# B - Circuitos Integrados

Esse projeto tem como objetivo trabalhar com os conceitos básicos de portas lógicas feitas em circuitos integrados. Cada grupo receberá uma equação lógica que deverá implementar e caberá ao grupo decidir a melhor forma de separação de trabalho que privilegie a distribuição de tarefas.

## Instruções

Deve-se implementar a mesma equação **lógica recebida em sala** (individual por grupo) via os circuitos integrados da família 40xx lógicos, disponível no Laboratório de Informática.

O circuito deve ser realizado na protoboard, deve-se gravar um vídeo do mesmo funcionando.

### Entradas

Pode-se utilizar como entrada do sistema (A,B,C,...) *jumpers* que estarão hora conectados em `GND (0)` ou `VCC (1)`. 

!!! tip
    A cada entrada um LED de cor diferente pode ser utilizado para de forma fácil saber quais são as entradas do sistema.

### Saída

A saída final do sistema deve ser representada com um LED, sendo aceso indicando lógica `1` e apagado lógica `0`.

### Documentação

Um documento descrevendo a solução empregada deve ser apresentando. O documento deve conter: A equação lógica original, diagrama de blocos lógico (contendo as portas lógicas), o diagrama elétrico (quais pinos de quais componentes foram utilizados) e o link para o vídeo do circuito funcionando.

!!! note
    O documento não precisa ser grande, de uma a duas páginas.

### Validação

Uma tabela verdade do circuito deve ser apresentada e em aula e uma demonstração que o circuito representa a tabela deve ser feita.

### Entrega 

A entrega da documentação deve ser realizada via github no repositório do grupo.

O documento deve ser colocado na pasta do repositório do grupo: `Z01.1/Projetos/B-CircuitosIntegrados/`


## Rubricas

As rubricas são progressivas A(B(C())).

| Nota         | Descritivo                                                                                                         |
| ------------ | ------------------------------------------------------------------------------------------------------------------ |
| **A**        | - Adicionar um sensor ao robô e usar para aprimorar sua lógica                                                     |
|              |                                                                                                                    |
| **B**        | - Trabalhando com o robô: Implementando equação lógica para controle dos motores e usando bumpers como entradas.   |
|              |                                                                                                                    |
| **C**        | - Circuito funcionado                                                                                              |
|              | - Documentação certa                                                                                               |
|              | - Vídeo demonstrando funcionamento                                                                                 |
|              |                                                                                                                    |
| **D**        | - Entregue fora do prazo máximo                                                                                    |
|              | - Circuito não funcionando                                                                                         |
|              | - Documentação com mais um itens errados/faltando                                                                  |
|              |                                                                                                                    |
| **I**        | - Não entregue                                                                                                     |

### Trabalhando com o robô 

O robô possui dois sensores de fim de curso (bumpers), um em cada lado da frente do robô que fornecem lógica `1` quando acionados e `0` quando não tem contato. O controle do robô é feito pelo controle de dois motores, esquerda e direita, cada motor possui dois sinais de controle: `Direção` e `Ligado`, conforme tabela a seguir:

| Direção M1 | Ligado M1 | Direção M2 | Ligado M2 | Comportamento |
| ---------- | --------- | ---------- | --------- | ------------- |
| `1`        |           |            |           |               |


A entrega deve ser um vídeo com o robô sendo controlado pelo seu circuito, e uma documentação com a tabela verdade e as equações encontradas para cada sinal do motor.

!!! note
    Estamos trabalhando com circuitos que não possuem memória, portanto não vai dar para fazer coisas muito complexas
    
!!! tip
    Faça uma tabela verdade com os sensores sendo entradas e os sinais dos motores saídas. Para cada saída encontre um equação lógica.
