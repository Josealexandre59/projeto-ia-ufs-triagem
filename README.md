# Triagem de chamados municipais

O notebook `analise_dados.ipynb` lê `chamados_municipais.csv` e treina o classificador do projeto: `CountVectorizer` (com limpeza do texto) e `MultinomialNB` (Naive Bayes). O sorteio de treino/teste é fixo (`random_state=42`), então os resultados se repetem a cada execução.

## Banco revisado

São 600 reclamações distintas, com 150 exemplos em cada categoria:

- Iluminação Pública: iluminação de ruas e espaços públicos.
- Obras e Pavimentação: pavimento, calçadas e estruturas públicas.
- Saneamento e Limpeza: resíduos, esgoto, drenagem e abastecimento de água.
- Trânsito e Mobilidade: circulação, sinalização, estacionamento e transporte coletivo.

As frases variam em tamanho, tom, pontuação, formalidade e alguns erros de escrita. Os mesmos tipos de locais aparecem em diferentes categorias. Por exemplo, lâmpada de iluminação pública fica em Iluminação; lâmpada de semáforo fica em Trânsito.

O banco anterior tinha 500 registros, mas apenas 64 textos diferentes, montados pelo mesmo molde. A revisão reduz essa repetição; não garante ausência de viés nem representa a frequência real dos chamados da população. O equilíbrio entre categorias foi uma escolha para o treinamento. O desempenho com reclamações reais ainda precisa ser verificado.

## Como executar

É necessário ter Python instalado no computador. As instruções abaixo são para Windows.

1. Extraia o ZIP e abra a pasta que contém `analise_dados.ipynb`, `chamados_municipais.csv` e `requirements.txt`. Mantenha esses arquivos juntos.
2. Na barra de endereço dessa pasta, digite `cmd` e pressione Enter para abrir o terminal nessa pasta.
3. Instale as dependências:

   ```bash
   python -m pip install -r requirements.txt
   ```

4. Abra o Jupyter:

   ```bash
   python -m jupyter notebook
   ```

5. Na página que abrir no navegador, clique em `analise_dados.ipynb`.
6. No menu **Kernel**, escolha **Restart & Run All** ou **Restart Kernel and Run All Cells**, conforme a versão. Confirme a execução, se solicitado. Isso executa todas as células em ordem e treina o modelo com o CSV.

Se o comando `python` não for reconhecido, tente usar `py` no lugar de `python` nos dois comandos. Se nenhum funcionar, instale o Python e habilite a opção de adicioná-lo ao PATH; depois reabra o terminal.

## Como testar outra reclamação

Na última célula de código (seção 9), altere somente a frase dentro de `chamado_teste`. Por exemplo:

```python
chamado_teste = "O ônibus do meu bairro demora demais"
classificar_chamado(chamado_teste)
```

Clique nessa célula e pressione **Shift + Enter**. Aparece a secretaria escolhida e a probabilidade de cada uma. É a resposta do modelo, que pode estar errada. Probabilidades perto de 50% indicam que o modelo está em dúvida.

Você pode trocar a frase e executar a célula de novo quantas vezes quiser, sem retreinar. Prefira frases que não estejam no CSV, para observar como o modelo classifica reclamações novas.

Se aparecer `NameError`, execute todas as células em ordem. Se aparecer `FileNotFoundError` para o CSV, confira se ele está na mesma pasta do notebook e se o nome é `chamados_municipais.csv`. Se aparecer `ModuleNotFoundError: matplotlib`, rode de novo `python -m pip install -r requirements.txt`. Salve suas alterações com **Ctrl + S**.

## Avaliação (Check-in 3)

O notebook separa 80% dos chamados para treino e 20% para teste, sem frases repetidas entre os dois, e mostra:

- acurácia, precision, recall e F1-Score por categoria;
- matriz de confusão;
- validação cruzada em 5 rodadas;
- lista dos chamados de teste que o modelo errou;
- teste com 12 frases novas, escritas fora do dataset.

## Como acrescentar reclamações

Para juntar contribuições, acrescente as linhas ao mesmo CSV, mantendo os nomes das categorias. Se o texto tiver vírgula, use aspas no campo, como nos exemplos já presentes no arquivo. Antes de treinar, revise duplicatas, frases muito semelhantes e categorias inconsistentes.
