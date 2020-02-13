# Lab 2: Travis CI

Travis é um sistema de integração contínua que vai executar de forma automática alguns testes (criado por nós) no projeto e em caso de alguma falha irá notificar no github e por e-mail todos os integrantes.

Como ele funciona ? Ele fica verificando o repositório por alterações (você deve além de dar commit, dar push) e para cada novo commit ele faz o seguinte

1. Inicializa uma nova máquina virtual na nuvem (ubuntu, windows, mac)
2. Instala todo a infra necessária do projeto (no caso do Z01.1 : python, java, Quartus, ...)
3. Executa os scripts de teste localizados em cada projeto.
4. Desliga e "deleta" a máquina virtual recém criada.

O arquivo de configuração do travis está localizado na raiz do repositório: [`Z01.1/.travis.yml`](https://github.com/Insper/Z01.1/blob/master/.travis.yml). Nele que estão feitas todas as definições de execução.

Na pagina do seu repositório em commits deve aparecer uma pequena bolinha em cada um dos commits novos que serão feitos no projeto, esse indicador será atualizado pelo travis sendo:

- Amarelo: O teste está em execução
- Verde: O teste passou
- Vermelho: O teste falhou

!!! note
    Cada teste leva em torno de alguns minutos já que toda a infraestrutura é instalada sempre do zero, não utilize o sistema de Integração Contínua para validar as suas novas implementações, esse sistema deve ser utilizado para encontrar problemas mais amplos ou para o scrum master aceitar ou não um pull-request, já que o resultado do sucesso ou não dessa requisição é visível facilmente.

## Ativando o Travis

!!! warning "Somente o `owner` do repositório"
    Daqui até o próximo aviso só uma pessoa do grupo deve fazer! Os demais devem acompanhar.

Será necessário acessar o site do travis:

- [https://travis-ci.org/](https://travis-ci.org/) e adicione o projeto forkado ao travis :

![Travis](figs/C-LogiComb/C-config-travis.gif)

