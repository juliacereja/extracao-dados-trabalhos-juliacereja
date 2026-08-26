# Engajamento por hashtag na coleta de vídeos do nicho de maquiagem.

## Pergunta

> Vídeos de tutorial de maquiagem perfoam melhor do que vídeos de arrume-se comigo (grwm)?

## Dados

**Fonte:** exportação do TikTok via Zeeschuimer.

**Período coletado:**
Alguns minutos do dia 19 de agosto de 2026.

**Tamanho da amostra:** 1416 posts

**Limites conhecidos da coleta:** dados coletados em somente uma plataforma, com apenas 1416 posts, coletados todos no mesmo dia e horário em alguns minutos e quantidade de posts por hashtag muito vareada.

## Método

Descreva o que foi calculado e como, incluindo toda decisão de tratamento (duplicatas removidas, denominador usado na taxa de engajamento, corte de linhas com denominador zero). Se usou uma fórmula, escreva a fórmula.

>Foi calculada a diferença de engajamento das hashtags grwm e tutorial em vídeos relacionados a maquiagem. Foram coletados dados de 1416 postas com hashtags do mesmo nicho, removidas as duplicatas que nesse caso foram 0 com df = df.drop_duplicates(),linhas com o denominador 0 foram removidas assim df_posts = df[df["plays"] > 0].copy() e a taxa de engajamento foi calcula pela soma de likes, comentários e compartilhamentos e dividida por plays dessa forma df_posts["taxa_engajamento"] = (df_posts["likes"] + df_posts["comments"] + df_posts["shares"]) / df_posts["plays"] .

## Achados

Liste cada achado como uma frase apoiada num número, uma linha de tabela ou um gráfico específico. Anexe ou referencie a tabela (`dados/resumo_hashtags.csv`) e o(s) gráfico(s) (`dados/grafico_relatorio.png` ou outro nome que você tenha usado).

- a taxa de engajamento de grwm é 0,04 maior do que de tutorial (`dados/resumo_hashtags.csv`)
- a #tutorial tem um engajamento mais constante do que #grwm (`grafico_comparacao_hashtags`)
- a #grwm continua sendo usada e tento bons resultados e a #tutorial continua ativa (`grafico_comparacao_hashtags`)

## Limitações

O que os dados **não** permitem concluir. Seja específico desta coleta, não genérico.

- os dados não nos permitem concluir que usar a #grwm tenha mais engajamento garantido do que #tutorial
- não é possível concluir que uma # tomou o lugar da outra, as duas continuam ativas.

## Recomendações

O que fazer a partir disso. Para cada recomendação, indique de qual achado específico ela depende.

- analisar uma maior quantidade de posts maior e por um periodo mais longo de tempo pode nos trazer dados mais confiáveis e uma análise mais profunda, para verificar se a taxa de engajamento é de fato maior e não está enviesada na nossa coleta.
- coletar mais dados para entender o porque dos picos altos e baixos da #grwm.

## Revisão por pares

**Revisado por:**   Sabrina Azulay Lewin

**Comentários recebidos:**

> Sim, a pergunta está clara e reprodutível.
> Sim, todos os dados possuem gráficos que os comprovam.
> Sim, o método está reproduzível.
> Sim, os achados possuem evidências.
> Não, as conclusões não extrapolam as evidências.
> Sim, achado e recomendações estão separados.

OBS:
> As recomendações não estão com a indicação de qual achado elas dependem.
> Os gráficos estão sem local e período de coleta
> As tabelas não estão sendo direcionadas para a pasta dados.
> A referência de onde o primeiro achado está, não está certa. Deveria ser "dados\resumo_hashtags.csv" (depois de colocar as tabelas feitas na pasta dados)

**O que mudou no relatório por causa da revisão (ou por que nada mudou):**

>Mudei apenas coisas mais técnicas como salvar a tabela em resumo hashtags e mudar no achados, e colocar fonte e período da coleta.

## Declaração de uso de IA

Ferramenta usada, em que trecho ou decisão desta entrega, e o que você conferiu ou alterou depois do resultado gerado. Se não usou IA, registre isso também. Nesse trabalho, está proibido usar IA para gerar códigos. 

> Não usei IA nessa entrega.
