## Parte 6 — README de reprodução


**Fonte e período dos dados:**

> Dados do TikTok coletados pelo Zeeschuimer, em agosto de 2026.

**Quantos posts entraram no modelo (depois de remover duplicata e `plays` = 0):**

> 1416.

**Quais features você usou, e por quê:**

> Usei `n_hashtags`, `tam_legenda`, `seguidores_autor`e `hora`, para verificar se a quantidade de hashtags, o tamanho da legenda, o número de seguidores do autor e o horário da postagem influenciam na taxa de engajamento do post.

**Quais colunas você deixou de fora por vazamento, e por quê:**

> Likes, comments, shares e plays, porque são as features usadas e são definidas somente após a postagem.

**Resultado: MAE e R² do modelo bobo, da linear e da árvore. O seu melhor modelo bateu o bobo?**

Modelo bobo:       MAE = 0.0445   R2 = -0.000
Regressão linear:  MAE = 0.0440   R2 = 0.012
Árvore (prof. 5):  MAE = 0.0422   R2 = -0.080
>O modelo não bateu o bobo, o que mostra que o modelo como um todo está explicando muito pouco da variação dos dados.

**Uma leitura de coeficiente (associação, não causa):**

> Na minha coleta, quanto mais hashtags, menor o engajamento.

**Declaração de uso de IA:** ferramenta usada, em que trecho ou decisão desta entrega, e o que você conferiu ou alterou depois do resultado gerado (mesmo que a resposta seja "não usei IA nesta entrega", registre isso).

> Usei o Claude para entender melhor os conceitos porque confesso que não entendi quase nada dessa matéria, assim como no último período, rs.