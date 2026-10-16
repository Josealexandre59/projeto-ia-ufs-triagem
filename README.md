# Triagem de chamados municipais

O notebook `analise_dados.ipynb` lê `chamados_municipais.csv` e treina o mesmo classificador do projeto: `CountVectorizer` com `MultinomialNB`.

## Banco revisado

São 320 reclamações distintas, com 80 exemplos em cada categoria:

- Iluminação Pública: iluminação de ruas e espaços públicos.
- Obras e Pavimentação: pavimento, calçadas e estruturas públicas.
- Saneamento e Limpeza: resíduos, esgoto, drenagem e abastecimento de água.
- Trânsito e Mobilidade: circulação, sinalização, estacionamento e transporte coletivo.

As frases variam em tamanho, tom, pontuação, formalidade e alguns erros de escrita. Os mesmos tipos de locais aparecem em diferentes categorias. Cada registro apresenta um problema principal para permitir uma única categoria. Por exemplo, lâmpada de iluminação pública fica em Iluminação; lâmpada de semáforo fica em Trânsito.

O banco anterior tinha 500 registros, mas apenas 64 textos diferentes, montados pelo mesmo molde. A revisão reduz essa repetição; não garante ausência de viés nem representa a frequência real dos chamados da população. O equilíbrio entre categorias foi uma escolha para o treinamento. O desempenho com reclamações reais ainda precisa ser verificado.

## Como executar

1. Instale as dependências com `pip install -r requirements.txt`.
2. Abra o Jupyter na pasta do projeto e execute o notebook do início ao fim.
