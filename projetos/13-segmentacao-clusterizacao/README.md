# Aula 13 — Segmentação e clusterização
## Parte D — README do case

Crie `README.md` dentro de `projetos/13-segmentacao-clusterizacao/` na sua pasta de entregas:

**Fonte, período e tamanho da coleta:**

> Posts do TikTok coletados através do Zeeschuimer, em agosto de 2026, com 1416 posts.

**As duas variáveis que você criou (a contínua da Parte A e o rótulo da Parte B), com a fórmula/critério de cada uma:**

> Na Parte A a variável contínua criada foi a taxa de engajamento, a partir da soma de likes, comentários e compartilhamentos divido pela quantidade de plays. Já a variável da Parte B foi criada com base em plays, com percentil de 90, para o evento ser de fato caro mas com posts suficientes para o modelo aprender.

**As features usadas nas Partes A e B, e quais colunas você descartou por vazamento:**

> As features usadas foram: tamanho da legenda(`tam_legenda`), número de hashtags(`n_hashtags`), e hora(`timestamp`). Por vazamento eu descartei plays, likes, comments e shares.

**Parte A — resultado:** MAE e R² do modelo bobo, da linear e da árvore. O seu melhor modelo bateu o bobo?

> O meu melhor modelo, a Regressão Linear, ficou com MAE com uma diferença de apenas 0,04, errou só um pouquinho menos que simplesmente "chutar a média pra todo mundo", e R² ficou 0.012, um valor baixo mas positivo. Ele ficou praticamente empatado com o modelo bobo. Ele até é levemente melhor (MAE um pouquinho menor, R² levemente positivo), mas a melhora é tão pequena que, na prática, isso indica que as variáveis usadas como features não têm relação linear tão forte com a taxa de engajamento, pelo menos a capturada por esse modelo.

**Parte B — resultado:** a matriz de confusão e uma leitura: a favor de quem o modelo erra?

> A matriz de confusão foi [[319, 0], [34, 1]]: das 35 postagens que realmente viralizaram no conjunto de teste, o modelo identificou apenas 1 e deixou passar 34 sem perceber (recall de aproximadamente 0,03). Por outro lado, das 1 vez em que o modelo apostou em "viral", ele estava certo (precisão de 1,00), mas com uma única aposta essa precisão não é confiável. Ou seja, o modelo erra fortemente a favor de dizer "não viralizou": ele quase nunca aposta em viral, e por isso deixa passar a grande maioria dos posts que realmente bombaram. 

**Parte C — resultado:** quantos segmentos, como você escolheu `k`, e a descrição de cada segmento (uma frase com número).

> Escolhi segmentar criadores e dividi eles em 4 grupos. Escolhi `k` 4 pois a silhueta média fica em 0,665 para `k` = 4, praticamente igual até `k` = 7 (0,669), o que indica que criar mais grupos não melhora a separação. Além disso, o gráfico do cotovelo cai com uma certa constancia, então ele não dá uma resposta decisiva sozinho. Com `k` 7, muitos grupos tinham apenas aproximadamente 3 participantes, então eles ficavam muito discrepantes e separados. Também não escolhi `k` 2 ou 3, apesar de terem a silhueta maior, pois agrupariam em um mesmo segmento perfis muitos diferentes de criadores. Diante disso, optei pelo menor número de grupos que mantém a qualidade da separação e que resulta em segmentos que consigo descrever e usar.

**Uma conclusão que os seus dados sustentam** (sem extrapolar para além da sua coleta):

> Escreva aqui.

**Revisão por pares:** nome do colega **da turma** que revisou, o que ele apontou, e o que você mudou (ou por que não mudou).

> Escreva aqui.

**Declaração de uso de IA:** ferramenta usada, em que trecho ou decisão, e o que você conferiu ou alterou depois (mesmo que seja "não usei IA nesta entrega"). Lembre: nesta entrega, IA não pode ser usada para gerar o código de análise.

> Nessa entrega não usei IA, mas usei coisas que eu havia feito anteriormente nas aulas 11, 12 e 13.
