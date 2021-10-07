# Vacinação

Esse documento tem por objetivo refletir as principais alteraçãoes que aconteceram na API, desde o banco de dados até nas rotas, com a adição da feature de vacinação.

Esse feature tem por objetivo coletar e armazenar dados da vacinação dos usuário em relação à COVID-19 para fins de análise e estudo por parte da equipe de vigilância.

## Tabelas atributos e relacionamentos.

Foi adicionadado uma tabela _vaccine_ com os seguintes atributos:

- **name**: É o nome da vacina e, normalmente, é como ela é conhecidada popularmente.
- **laboratory**: É o nome do laboratório(s) que fabricaram a vacina. Em caso de mais de um laboratório recomenda-se separar o nome dos laboratórios por uma barra ('/').
- **min_dose_interval**: É o numero mínimo de dias necessários para a aplicação da segunda dose.
- **max_dose_interval**: É o número máximo de dias recomendados para a aplicação da segunda dose.
- **country_origin**: É uma string que guarda o país de origem ou onde a vacina foi criada/desenvolvida.
- **doses**: É o número de doses necessário para a imunização completa.
- **id**: É o identificador único de cada dado.
- **app_id**: Atua como foreign key referenciando o _id_ do app que a vacina pertence.

Além da criação da tabela _vaccine_ foi adicionado os seguntes campos na tabela _users_:

- **first_dose_date:** É a data que o usuário tomou a primeira dose.
- **second_dose_date:** É a data que o usuário tomou a segunda dose.
- **vaccine_id:** Atua com foreign key poara registrar qual vacina o usuário tomou. Vale também para a verificação da necessidade de se preencher a data da segunda dose, no caso de vacinas de dose única.

## Models

Foi adicionada uma model para representação dos dados da tabela criada. Além disso a model ainda adiciona algumas restrições aos dados. Dentre as restrições:
**Tabela _vaccine_:**

- Os campos _name_, _country_origin_ e _laboratory_ não podem ter valor null e tem comprimento entre 1 e 255 caracteres.
- O campo _doses_ não pode assumir valor null e tem que ter valor inteiroentre 1 e 10.

A model _Vaccine_ possui dois relacionamentos a nível de model:

- _vaccine has many users_
- _app has many vaccines_

Há um relacionamento entre a model _Vaccine_ e a model _User_ em que _User_ _belongs_to_ _Vaccine_.

As vacinas são filtradas pelo app_id do usuário.

## Controllers

Foi criada apenas a _controller vaccine_controller_ para administrar as rotas disponíveis.

### Rotas

Aqui é listado todas as rotas adicionadas/modificadas com a adição da feature de vacinação.

- GET _vaccine/_: Retorna todas as vacinas com o mesmo app_id do usuário (o filtro é aplicado na model)
- GET _vaccine/{id}/_: Retorna apenas a vacina com o id especificado.
- POST _vaccine/_: Cria uma vacina com o app_id do usuário que a criou.
- PATCH/PUT _vaccine/{id}/_: Atualiza os dados da vacina que tenha o id especificado.
- DELETE _vaccine/{id}/_: Deleta a vacina com o id especificado.

## Serializers

Foi adicionado uma _serializer_, _vaccine_serializer_ e feita alteração na de usuários retornar a vacina do usuário.

## Permissões

As permissões de cada usuário em relação à _vaccine_:

- **Admin**: Gerenciar
- **Usuários**: Ler
