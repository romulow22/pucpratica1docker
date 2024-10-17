# IEC_DCSE_O3_T1_Online: Conteinerização e Orquestração

## Trabalho Prático Unidade 1 : *Docker*

- Nome: Rômulo Alves
- E-mail: 1545593@sga.pucminas.br
- Matricula: 212457
  
## Sumário
- [IEC\_DCSE\_O3\_T1\_Online: Conteinerização e Orquestração](#iec_dcse_o3_t1_online-conteinerização-e-orquestração)
  - [Trabalho Prático Unidade 1 : *Docker*](#trabalho-prático-unidade-1--docker)
  - [Sumário](#sumário)
  - [Descrição](#descrição)
  - [Arquitetura da Solução](#arquitetura-da-solução)
  - [Detalhes da Implementação](#detalhes-da-implementação)
  - [Requisitos](#requisitos)
  - [Instruções de Instalação e Execução](#instruções-de-instalação-e-execução)
    - [1. Clonar o repositório](#1-clonar-o-repositório)
    - [2. Executar o ambiente](#2-executar-o-ambiente)
  - [Como Jogar](#como-jogar)
  - [Manutenção e Atualização](#manutenção-e-atualização)
  - [Escalabilidade](#escalabilidade)
  - [Remoção do Ambiente](#remoção-do-ambiente)
  - [Considerações de Segurança](#considerações-de-segurança)
  - [Contribuição](#contribuição)
  - [Licença](#licença)

## Descrição

Este projeto implementa uma versão conteinerizada do jogo de adivinhação disponível no [Guess Game](https://github.com/fams/guess_game), utilizando Docker e Docker Compose. A solução demonstra boas práticas de conteinerização, orquestração e arquitetura de microserviços.


## Arquitetura da Solução

A solução é composta por três serviços principais:

1. **backend-app**: Aplicação Python (Flask) que executa a lógica do jogo de adivinhação.
2. **frontend-app**: Servidor Nginx atuando como proxy reverso, balanceando o backend e servindo as páginas do frontend React.
3. **postgresdb**: Banco de dados PostgreSQL para persistência de dados.

## Detalhes da Implementação

1. **Dockerfiles Otimizados**: 
   - Utilização de imagens Alpine para backend e frontend, priorizando eficiência e portabilidade.

2. **Configuração Nginx**:
   - Tratamento diferenciado de requisições entre frontend e backend.
   - Implementação de balanceamento de carga para múltiplas instâncias de backend.

3. **Docker Compose**:
   - Segregação de redes (APP e DB) para isolamento de segurança.
   - Implementação de healthchecks em todos os serviços.
   - Definição de dependências para inicialização correta.
   - Política de restart "unless-stopped" para alta disponibilidade.
   - Volume local para persistência do banco de dados.

## Requisitos

- [Docker](https://docs.docker.com/engine/install/)
- [Docker Compose](https://docs.docker.com/compose/install/)
- [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)

> **Nota**: Este ambiente foi testado no Windows 11 com [Docker Desktop](https://docs.docker.com/desktop/)

## Instruções de Instalação e Execução

### 1. Clonar o repositório

```shell
git clone https://github.com/romulow22/pucpratica1docker.git
```

### 2. Executar o ambiente

```shell
cd pucpratica1docker
docker compose -f docker-compose.yml up -d --build
```  

## Como Jogar

1. Acesse [http://localhost](http://localhost) em seu navegador.
2. Na página 'Maker', crie um novo jogo inserindo uma frase secreta e anote o Game ID gerado.
3. Na página 'Breaker', insira o Game ID e tente adivinhar a frase secreta.


## Manutenção e Atualização

1. Modifique os arquivos **docker-compose.yml**, **Dockerfile** no backend ou frontend conforme necessário.

2. Recrie o ambiente com:

```shell
docker compose -f docker-compose.yml down --rmi all
docker compose -f docker-compose.yml up -d --build
```

## Escalabilidade

Aumente o número de instâncias de backend de duas formas:

1. Adicionando novos serviços no **docker-compose.yml** e atualizando o **nginx.conf**.
2. Usando o comando de escala do Docker Compose:

```shell
docker compose scale backendapp1=3 backendapp2=2
```

## Remoção do Ambiente

Para remover completamente o ambiente:

```shell
docker compose -f docker-compose.yml down --rmi all --volumes
cd ..
rm pucpratica1docker -r -force
```  

## Considerações de Segurança

1. As redes estão segregadas para limitar o acesso direto ao banco de dados.
2. Considere implementar HTTPS para produção.
3. Revise regularmente as imagens Docker e dependências para atualizações de segurança.

## Contribuição

Contribuições são bem-vindas! Por favor, abra uma issue ou pull request para sugestões ou melhorias.

## Licença

Este projeto está licenciado sob a MIT License.