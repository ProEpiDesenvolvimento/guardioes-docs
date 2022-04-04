# Biossegurança

Esse documento visa descrever o épico de biossegurança pelo ponto de vista da API.

Esse feature tem por objetivo coletar e armazenar as respostas dos usuários de uma instituição sobre as perguntas que são cadastradas por ela, em relação a biossegurança do local.

## Tabelas, atributos e relacionamentos

Foram adicionadas as seguintes tabelas para os formulários, com os seguintes atributos:

**forms**

- **id**: O número de identificação do objeto.
- **group_manager_id**: O ID do Group Manager que o formulário pertence.

**form_questions**

- **id**: O número de identificação do objeto.
- **kind**: O tipo de pergunta. enum("boolean", "multiple").
- **text**: O texto da pergunta.
- **order**: A ordem da pergunta no formulário. Ex: 1, 2, 3...
- **form_id**: O ID do formulário que a pergunta pertence.

**form_options**

- **id**: O número de identificação do objeto.
- **value**: O valor semântico da opção. Sempre `true` para perguntas do tipo "multiple", `true` ou `false` para opções do tipo "boolean".
- **text**: O texto da opção.
- **order**: A ordem da opção na pergunta. Ex: 1, 2, 3...
- **form_question_id**: O ID da pergunta que a opção pertence.

E para o usuário:

**form_answers**

- **id**: O número de identificação do objeto.
- **form_id**: O ID do formulário que a resposta pertence.
- **form_question_id**: O ID do pergunta respondida.
- **form_option_id**: O ID da opção escolhida.
- **user_id**: O ID do usuário que respondeu a pergunta.

## Tipos de perguntas

- **boolean**: Pergunta com apenas duas opções, sendo uma verdadeira (`true`) e outra falsa (`false`). Ex: Na sua instituição há disposição de álcool em gel? (Sim ou Não)
- **multiple**: Pergunta de múltipla escolha, todas as opções tem valor verdadeiro (`true`), mesmo se a afirmação for negativa. Ex: Com que frequência você lava as mãos por dia? (Várias opções)

## Valor da opção

- **true**: Opção com valor verdadeiro, utilizada com perguntas de tipo "multiple" e "boolean".
- **false**: Opção com valor falso, utilizada apenas em perguntas do tipo "boolean". Onde o valor da opção é importante.

## Models

Foram adicionadas as models para a ordenação dos dados, relações e controle de foreign_keys.

A model _Form_ possui três relacionamentos:

- _form belongs_to group_manager_
- _form has many form_questions_
- _form has many form_answers_

A model _FormQuestion_ possui dois relacionamentos:

- _form_question belongs_to form_
- _form_question has many form_options_

A model _FormOption_ possui dois relacionamentos:

- _form_option belongs_to form_question_
- _form_option has many form_answers_

A model _FormAnswers_ possui quatro relacionamentos:

- _form_answer belongs_to form_
- _form_answer belongs_to form_question_
- _form_answer belongs_to form_option_
- _form_answer belongs_to user_


No nível hierárquico da maior para menor, elas também possuem o atributo `:dependent => :destroy`, porque dependem uma das outras para existir.

## Controllers

Foram criadas controllers de todas as models para administrar as rotas disponíveis.

### Rotas

Aqui é listado as rotas mais comuns adicionadas/modificadas com a adição da feature de biossegurança.

- GET _/forms_: Retorna todos os formulários cadastrados com app_id do usuário (o filtro é aplicado na model).
- GET _/forms/{id}_: Retorna apenas o formulário com o id especificado.
- POST _/forms_: Cria um formulário com o id do Group Manager que a criou.
- PATCH/PUT _/forms/{id}_: Atualiza os dados do formulário com o id especificado.
- DELETE _/forms/{id}_: Deleta o formulário com o id especificado e todos os objetos filhos dependentes.

## Serializers

Foram adicionados os serializers de todas as models, também para ser retornado o **objeto inteiro** nas rotas, ao invés do id nas relações entre elas.

## Permissões

As permissões de cada usuário em relação ao _form_:

- **Group Manager**: Gerenciar todos os formulários, perguntas e opções. Vê as respostas dos usuários.
- **Usuários**: Enviar respostas e visualizar formulário da sua instituição.
