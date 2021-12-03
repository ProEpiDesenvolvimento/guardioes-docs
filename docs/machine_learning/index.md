# Estudo de machine learning

## Algoritmo

O objetivo desse estudo é verificar a possibilidade de haver um mecanismo de machine learning para gerar um alogiritmo que possa detectar síndromes, como a COVID-19. Para isso foi testado alguns modelos usando os dados com um certo nível de tratamento.

Os modelos disponíveis atualmente conseguiram acurácia de 56% em média considerando apenas os dados que possuem algum sintoma, a idade da pesssoa, o resultado do teste, se eles tem alguma condição preexistente e o sexo.

Para maiores detalhes rode os dois notebooks onde os testes dos modelos estão hospedados. Eles se encontram na pasta docs/machine_learning.

## Execução dos notebooks

Para rodá-los basta instalar os seguintes pacotes:<br>

- [Python](https://tutorial.djangogirls.org/pt/python_installation/)<br>
- [Jupyter notebook](https://jupyter.org/install)<br>
- Para os pacotes que são importados em cada um dos arquivos basta dar o seguinte comando para cada pacote:

```Shell
pip3 install <nome-do-pacote>
```

obs: Alguns pacotes podem ter nomes diferentes dos imports, nesse caso procure a documentação do pacote para instalá-lo corretamente.

## Preparação dos dados

Para executar o notebook de preparação dos dados no arquivo: ./prepare_data.ipynb basta criar uma pasta chamada data_city/ para armazenar os arquivos que contem os casos por cidade. Para execução desse script também é necessário que baixe os dados de Goias no site do [e-sus](https://opendatasus.saude.gov.br/gl/dataset/casos-nacionais).

## Dados

Alguns dados de amostra já pré-tratados já estão disponíveis na pasta /docs/machine_learning/data. Os dados originais se encontram neste [site].(https://opendatasus.saude.gov.br/gl/dataset/casos-nacionais)


