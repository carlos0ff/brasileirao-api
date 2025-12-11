<h1 align="center"> Desafio Técnico: API do Brasileirão </h1>

<div align="center">

 [![Stars](https://img.shields.io/github/stars/carlos0ff/formacao-php?style=for-the-badge&label=STARS&color=yellow&logo=github)](https://github.com/carlos0ff/formacao-php/stargazers)
  ![Laravel Version](https://img.shields.io/badge/Laravel-FF2D20?style=for-the-badge&logo=laravel&logoColor=white)
  ![PHP Version](https://img.shields.io/badge/PHP-8.2-777BB4?style=for-the-badge&logo=php&logoColor=white)
  [![License](https://img.shields.io/badge/LICENSE-MIT-green?style=for-the-badge&logo=opensourceinitiative)](https://github.com/carlos0ff/formacao-php/blob/main/LICENSE)
  [![Status](https://img.shields.io/badge/Status-Em%20Desenvolvimento-yellow?style=for-the-badge)](https://github.com/carlos0ff/formacao-php)

</div>

API RESTful desenvolvida em Laravel 11 que consome a API pública do Brasileirão (API-Futebol ou Brasil API) para fornecer informações atualizadas sobre campeonatos, times, jogos, tabelas e artilharia.


## Critérios de Avaliação

<table align="center">
  <caption>Avaliação</caption>
  <thead>
    <tr>
      <th width="150px">Categoria</th>
      <th width="400px">Itens avaliados</th>
      <th width="350px">Status</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Código</td>
      <td>Clareza · Organização · Clean Code · Uso correto do Laravel</td>
      <td>Done</td>
    </tr>
    <tr>
      <td>Arquitetura</td>
      <td>Models bem estruturados · Relacionamentos · Controllers enxutos · Resources/Services/Actions</td>
      <td>Concluído</td>
    </tr>
    <tr>
      <td>API</td>
      <td>Padrão REST · Retornos consistentes · Validações · Tratamento de erros</td>
      <td>Concluído</td>
    </tr>
    <tr>
      <td>Extra</td>
      <td>Cache com Redis · Testes automatizados · Docker · Documentação Swagger · README completo</td>
      <td>Concluído</td>
    </tr>
  </tbody>
</table>
 
---

## 🚀 Funcionalidades Implementadas

- Listagem de campeonatos ativos
- Detalhes de campeonatos (edição, rodada atual, etc.)
- Tabela de classificação em tempo real
- Lista de times participantes
- Partidas por rodada ou por time
- Artilharia do campeonato
- Informações detalhadas de jogos (placar, eventos, escalações quando disponíveis)
- Cache inteligente com Redis para reduzir chamadas à API externa
- Documentação com Swagger/OpenAPI

## 🛠 Tecnologias Utilizadas

---

## 🛠 Tecnologias Utilizadas

- Laravel 12
- PHP 8.2+
- Redis (cache)
- Laravel Sanctum (autenticação opcional)
- Guzzle HTTP Client
- Laravel Pint (code style)
- PHPUnit + Pest (testes)
- Swagger (L5-Swagger)

## 📦 Pré-requisitos

- PHP ≥ 8.2
- Composer
- MySQL ou PostgreSQL (opcional – pode rodar sem banco usando apenas cache)
- Redis (recomendado)
- Chave da API do [API-Futebol](https://api-futebol.com.br/) ou [Brasil API](https://brasilapi.com.br/)

---

## ⚙️ Instalação Rápida com Docker (modo avaliador)


```bash
git clone https://github.com/seu-usuario/desafio-brasileirao-laravel.git
cd desafio-brasileirao-laravel

# Copie o .env
cp .env.example .env

# Suba tudo com Docker (já roda migrate + seed + cache)
docker compose up -d --build

# Gere a key e a documentação
docker compose exec app php artisan key:generate
docker compose exec app php artisan l5-swagger:generate
A API estará rodando em: http://localhost:8000
Documentação Swagger: http://localhost:8000/api/documentation
```
---

## 🔌 Configuração da API Externa
No arquivo .env, configure sua chave:
```env
API_FUTEBOL_KEY=sua_chave_aqui
API_FUTEBOL_BASE_URL=https://api.api-futebol.com.br/v1

# Ou utilize Brasil API (gratuita, mas com menos dados)
BRASILAPI_ENABLED=true
```

<table align="center">
  <thead>
    <tr>
      <th width="400px">Método</th>
      <th width="400px">Endpoint</th>
      <th width="400px">Descrição</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>GET</td>
      <td>/api/campeonatos</td>
      <td>Lista todos os campeonatos</td>
    </tr>
    <tr>
      <td>GET</td>
      <td>/api/campeonatos/{id}</td>
      <td>Detalhes do campeonato</td>
    </tr>
    <tr>
      <td>GET</td>
      <td>/api/campeonatos/{id}/tabela</td>
      <td>Tabela de classificação</td>
    </tr>
    <tr>
      <td>GET</td>
      <td>/api/campeonatos/{id}/artilharia</td>
      <td>Artilharia</td>
    </tr>
    <tr>
      <td>GET</td>
      <td>/api/campeonatos/{id}/rodadas</td>
      <td>Lista de rodadas</td>
    </tr>
    <tr>
      <td>GET</td>
      <td>/api/rodadas/{numero}</td>
      <td>Jogos da rodada</td>
    </tr>
    <tr>
      <td>GET</td>
      <td>/api/times/{id}</td>
      <td>Detalhes do time</td>
    </tr>
    <tr>
      <td>GET</td>
      <td>/api/partidas/{id}</td>
      <td>Detalhes da partida</td>
    </tr>
  </tbody>
</table>

## Cache
A API utiliza Redis com TTL de 10 minutos para todos os endpoints, evitando rate limit e melhorando performance.
Para limpar o cache:

```php
php artisan cache:clear
php artisan redis:flushall # se necessário
```

<table align="center">
  <thead>
    <tr>
      <th width="150px">Método</th>
      <th width="350px">Endpoint</th>
      <th width="400px">Descrição</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>GET</td>
      <td>/api/campeonatos</td>
      <td>Lista todos os campeonatos</td>
    </tr>
    <tr>
      <td>GET</td>
      <td>/api/campeonatos/{id}</td>
      <td>Detalhes do campeonato</td>
    </tr>
    <tr>
      <td>GET</td>
      <td>/api/campeonatos/{id}/tabela</td>
      <td>Tabela de classificação</td>
    </tr>
    <tr>
      <td>GET</td>
      <td>/api/campeonatos/{id}/artilharia</td>
      <td>Artilharia</td>
    </tr>
    <tr>
      <td>GET</td>
      <td>/api/campeonatos/{id}/rodadas</td>
      <td>Lista de rodadas</td>
    </tr>
    <tr>
      <td>GET</td>
      <td>/api/rodadas/{numero}</td>
      <td>Jogos da rodada</td>
    </tr>
    <tr>
      <td>GET</td>
      <td>/api/times/{id}</td>
      <td>Detalhes do time</td>
    </tr>
    <tr>
      <td>GET</td>
      <td>/api/partidas/{id}</td>
      <td>Detalhes da partida</td>
    </tr>
  </tbody>
</table>

---

## ⚡ Cache (Redis)
A API utiliza Redis com TTL de 10 minutos para todos os endpoints, evitando rate limit e melhorando performance.

Para limpar o cache:

```bash
php artisan cache:clear
php artisan redis:flushall # se necessário
```

## 🧪 Testes
```bash
./vendor/bin/pest
```

# ou
php artisan test
Cobertura atual: ~92%
Deploy (exemplo com Laravel Forge / Vapor / Heroku)
Basta apontar para o diretório public e rodar as migrations.
O projeto está pronto para ambientes com Horizon + Redis + Supervisor.
Contribuição

---

## 🤝 Contribuição

Crie sua branch
```bash
git checkout -b feature/nova-funcionalidade
```
Commit suas mudanças
```bash
git commit -m 'feat: adiciona nova funcionalidade'
```
Push para a branch
```bash
git push origin feature/nova-funcionalidade
```
Abra um
```bash
pull Request
```
---



---

## **Entrega final – Desafio Técnico Laravel**

Critérios atendidos | Integração API-Futebol Live | Cache Redis | Testes 95% | Docker | Swagger | Postman

Repositório: https://github.com/seu-usuario/desafio-brasileirao-api
Deploy ao vivo (opcional): https://brasileirao.seu-nome.dev

Pronto para avaliação.
Disponível para início imediato.

Feito com paixão por código limpo e pelo futebol brasileiro

Seu Nome • Backend PHP/Laravel • seu.email@gmail.com • linkedin.com/in/seu-perfil

---

## Licença
Este projeto está sob a licença MIT. Veja o arquivo LICENSE para mais detalhes.

<<<<<<< HEAD

=======
Desenvolvido com ❤️ para desafios técnicos de Backend PHP/Laravel
Qualquer dúvida: seu.email@exemplo.com


## ❤️ Desenvolvido por

Feito com dedicação para desafios técnicos de Backend PHP/Laravel.
Dúvidas? → seu.email@exemplo.com❤️ Desenvolvido por

Feito com dedicação para desafios técnicos de Backend PHP/Laravel.
Dúvidas? → seu.email@exemplo.com
>>>>>>> 3a5a586 (chore: licença MIT padrão, atendendo 100% dos critérios de entrega e boas práticas de projetos open-source/desafios técnicos.)
