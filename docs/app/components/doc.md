## Component Autocomplete

Esse componente é um pressionável que ao clicar abre um modal, mostrando as opções dispońiveis para completar. Em questões de estilização ele é um campo que vai ocupar 100% da largura do componente pai e tem altura fixa.
Para a implementação de um novo autocomplete, na pasta locales tem um objeto específico para placeholders costumizados.

Ele possui as seguintes props: 

 - **data**: São os dados que o usuário terá que selecionar. Deve ser uma array de objetos e cada objeto deve ter o campo 'label'. Obrigatório.
 - **value**: É o valor mostrado fora do modal no campo onde o usuário clica para abrir o modal. Obrigatório.
 - **onChange**: É a função que altera o **value**. É por ela que o component retorna o valor obtido para o Componente pai. Obrigatório. Ela retorna um objeto da array de **data**.
 - **textCancel**: Texto usado no botão de cancelar. Tem valor padrão: _translate('selector.cancelButton')_
 - **placeholder**: Placeholder do text input.