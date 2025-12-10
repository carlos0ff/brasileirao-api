# Desafio Técnico: API do Brasileirão (Laravel)

API RESTful desenvolvida em Laravel 11 que consome a API pública do Brasileirão (API-Futebol ou Brasil API) para fornecer informações atualizadas sobre campeonatos, times, jogos, tabelas e artilharia.

![Laravel](https://img.shields.io/badge/Laravel-11-ff2d20?logo=laravel&logoColor=white)
![PHP](https://img.shields.io/badge/PHP-8.2%2B-777bb4?logo=php&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-green)

## Funcionalidades

- Listagem de campeonatos ativos
- Detalhes de campeonatos (edição, rodada atual, etc.)
- Tabela de classificação em tempo real
- Lista de times participantes
- Partidas por rodada ou por time
- Artilharia do campeonato
- Informações detalhadas de jogos (placar, eventos, escalações quando disponíveis)
- Cache inteligente com Redis para reduzir chamadas à API externa
- Documentação com Swagger/OpenAPI

## Tecnologias Utilizadas

- Laravel 11
- PHP 8.2+
- Redis (cache)
- Laravel Sanctum (autenticação opcional)
- Guzzle HTTP Client
- Laravel Pint (code style)
- PHPUnit + Pest (testes)
- Swagger (L5-Swagger)

## Pré-requisitos

- PHP ≥ 8.2
- Composer
- MySQL ou PostgreSQL (opcional – pode rodar sem banco usando apenas cache)
- Redis (recomendado)
- Chave da API do [API-Futebol](https://api-futebol.com.br/) ou [Brasil API](https://brasilapi.com.br/)

## Instalação

```bash
# Clone o repositório
git clone https://github.com/seu-usuario/desafio-brasileirao-laravel.git
cd desafio-brasileirao-laravel

# Instale as dependências
composer install

# Copie o arquivo de ambiente
cp .env.example .env

# Configure seu .env (banco de dados opcional, Redis e chave da API)
php artisan key:generate

# Rode as migrations (se usar banco)
php artisan migrate

# Instale e gere a documentação Swagger
php artisan l5-swagger:generate

# Inicie o servidor
php artisan serve
```

## Configuração da API Externa
No arquivo .env, configure sua chave:
envAPI_FUTEBOL_KEY=sua_chave_aqui
API_FUTEBOL_BASE_URL=https://api.api-futebol.com.br/v1

# Ou utilize Brasil API (gratuita, mas com menos dados)
BRASILAPI_ENABLED=true


Método,Endpoint,Descrição
GET,/api/campeonatos,Lista todos os campeonatos
GET,/api/campeonatos/{id},Detalhes do campeonato
GET,/api/campeonatos/{id}/tabela,Tabela de classificação
GET,/api/campeonatos/{id}/artilharia,Artilharia
GET,/api/campeonatos/{id}/rodadas,Lista de rodadas
GET,/api/rodadas/{numero},Jogos da rodada
GET,`/api/times/{id},Detalhes do time
GET,/api/partidas/{id},Detalhes da partida

## Cache
A API utiliza Redis com TTL de 10 minutos para todos os endpoints, evitando rate limit e melhorando performance.
Para limpar o cache:

```php  php artisan cache:clear
        php artisan redis:flushall # se necessário
```

### Testes
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

## Fork o projeto
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

## Licença
Este projeto está sob a licença MIT. Veja o arquivo LICENSE para mais detalhes.

Desenvolvido com ❤️ para desafios técnicos de Backend PHP/Laravel
Qualquer dúvida: seu.email@exemplo.com
