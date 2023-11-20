# Quer apostar quanto?
Aplicação de back-end de um sistema de apostas de uma casa de apostas que deseja automatizar os seus processos para não sair em desvantages com os diversos aplicativos de apostas que surgiram. Nesta aplicação, é possível gerenciar o back-end dessa aplicação através de requisições HTTP(s) seguindo a convenção REST.

# Demo
[https://github.com/hp1heloisa/desafio-quer-apostar]()

# Como funciona?
Este projeto é uma API REST para atender a aplicação de apostas. Ela possui três entidades: `participants`, `games` e `bets`. As características destas entidades estão no arquivo `schema.prisma`.

Para as entidades, foram criadas sete rotas:

- GET `/participants`: Retorna todos os participantes e seus respectivos saldos.
- GET `/games`: Retorna todos os jogos cadastrados.
- GET `/games/:id`: Retorna os dados de um jogo junto com as apostas atreladas a ele.
- POST `/participants`: Cria um participante com determinado saldo inicial e body da requisição deve ter a seguinte estrutura: 

```
{
	name: string;
	balance: number; // representado em centavos, ou seja, R$ 10,00 -> 1000
}
```

- POST `/games`: Cria um novo jogo, com placar inicial 0x0 e marcado como não finalizado e o body da requisição deve ter o seguinte formato: 

``` 
{
	homeTeamName: string;
	awayTeamName: string;
}
```

- POST `/bets`: Cadastra uma aposta de um participante em um determinado jogo. O valor da aposta deve ser descontado imediatamente do saldo do participante e o body da requisição deve conter o seguinte formato: 

```
{ 
	homeTeamScore: number;
	awayTeamScore: number; 
	amountBet: number; // representado em centavos, ou seja, R$ 10,00 -> 1000
	gameId: number; 
	participantId: number;
}
```

- POST `/games/:id/finish`: Finaliza um jogo e consequentemente atualiza todas as apostas atreladas a ele, calculando o valor ganho em cada uma e atualizando o saldo dos participantes ganhadores e body da requisição deve ter o seguinte formato: 

```
{
	homeTeamScore: number;
	awayTeamScore: number;
}
```



# Motivação (opcional)
Este projeto foi feito para praticar a construção de uma API REST usando o ecossistema Node e Express junto com as tecnologias TypeScript e Prisma.

# Tecnologias utilizadas
Para este projeto, foram utilizadas:

- Node (versão 18.17.0);
- Express;
- TypeScript;
- Prisma;
- Postgres;
- Jest e Supertest;
- Joi;

# Como rodar em desenvolvimento
Para executar este projeto em desenvolvimento, é necessário seguir os passos abaixo:

- Clonar o repositório;
- Baixar as dependências necessárias com o comando: `npm install`;
- Em seguida, criar o arquivo `.env` com base no `.env.example`;
- Para poder executar os testes, será necessário criar um outro arquivo `.env.test` com base no `.env.example`;
- Este arquivo `.env` é composto pelas seguintes propriedades:
```
  DATABASE_URL="postgresql://postgres..."
```
- A propriedade `DATABASE_URL` é usada para fazer a conexão com o banco de dados.

- Será necessário executar o Prisma para criar o banco de dados e as tabelas necessárias. Para isso, execute o comando: `npx prisma migrate dev`;
- Para rodar o projeto em desenvolvimento, execute o comando `npm run dev`;
- Testes manuais podem ser feitos através do Thunder Client.
