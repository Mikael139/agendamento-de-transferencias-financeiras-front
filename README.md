# Agendamento de Transferências - Front-end
Este projeto é a interface de usuário (front-end) para o sistema de agendamento de transferências financeiras. Desenvolvido com Vue.js, ele permite que você interaja com a API REST de forma intuitiva, agendando novas transferências e visualizando o extrato de todas as operações.

O projeto foi criado para ser leve e eficiente, consumindo os endpoints da API de back-end e fornecendo uma experiência de usuário simples.

# Tecnologias Utilizadas
- Vue.js: Framework JavaScript progressivo para a construção de interfaces de usuário. A arquitetura baseada em componentes permite uma organização clara e modular do código.
- Axios: Um cliente HTTP leve e robusto, utilizado para fazer as requisições POST e GET para a API.
- CSS Puro: Para a estilização dos componentes, garantindo um visual limpo e moderno.

# Como Rodar o Projeto?
Siga os passos abaixo para ter a aplicação rodando em sua máquina.

Pré-requisitos
Certifique-se de que você tem o Node.js e o npm (Node Package Manager) instalados em seu sistema.

1. Clonar o Repositório
Primeiro, clone este repositório para o seu ambiente local e navegue até a pasta do projeto.
```
git clone [https://github.com/Mikael139/agendamento-de-transferencias-financeiras-front](https://github.com/Mikael139/agendamento-de-transferencias-financeiras-front)
```
```
cd agendamento-de-transferencias-financeiras-front
```

2. Instalar as Dependências
Com o terminal dentro da pasta do projeto, execute o comando para instalar todas as dependências necessárias.
```
npm install
```

3. Iniciar o Servidor de Desenvolvimento
Após a instalação, você pode iniciar a aplicação com o seguinte comando. Ela será executada em http://localhost:8081.
```
npm run serve
```

# Dependência da API
É essencial que a API do back-end esteja rodando na porta 8080 antes de iniciar esta aplicação front-end. O front-end se comunica com a API nos seguintes endpoints:
```
POST: http://localhost:8080/api/transferencias/agendar
```
```
GET: http://localhost:8080/api/transferencias/extrato
```

# Back-End (Java)
O desafio principal é criar um sistema que permite aos usuários agendar transferências financeiras, aplicando regras de negócio específicas para o cálculo de taxas. O sistema também oferece um endpoint para visualizar o extrato de todos os agendamentos realizados.

[Link do repositório](https://github.com/Mikael139/agendamento-de-transferencias-financeiras)
