# Aula 13 — Segmentação e clusterização
## Parte D — README do case

Crie `README.md` dentro de `projetos/13-segmentacao-clusterizacao/` na sua pasta de entregas:

**Fonte, período e tamanho da coleta:**

> Posts do TikTok coletados através do Zeeschuimer, em agosto de 2026, com 1416 posts. O vídeo mais antigo da coleta é de 11/12/2020 e o mais recente de 19/08/2026, com 2077 dias de período coberto.

**As duas variáveis que você criou (a contínua da Parte A e o rótulo da Parte B), com a fórmula/critério de cada uma:**

> Na Parte A a variável contínua criada foi a taxa de engajamento, a partir da soma de likes, comentários e compartilhamentos divido pela quantidade de plays. Já a variável da Parte B foi criada com base em plays, com percentil de 90, para o evento ser de fato caro mas com posts suficientes para o modelo aprender.

**As features usadas nas Partes A e B, e quais colunas você descartou por vazamento:**

> As features usadas foram: tamanho da legenda(`tam_legenda`), número de hashtags(`n_hashtags`), e hora(`timestamp`). Por vazamento eu descartei plays, likes, comments e shares.

**Parte A — resultado:** MAE e R² do modelo bobo, da linear e da árvore. O seu melhor modelo bateu o bobo?

> O meu melhor modelo, a Regressão Linear, ficou com MAE com uma diferença de apenas 0,04, errou só um pouquinho menos que simplesmente "chutar a média pra todo mundo", e R² ficou 0.012, um valor baixo mas positivo. Ele ficou praticamente empatado com o modelo bobo. Ele até é levemente melhor (MAE um pouquinho menor, R² levemente positivo), mas a melhora é tão pequena que, na prática, isso indica que as variáveis usadas como features não têm relação linear tão forte com a taxa de engajamento, pelo menos a capturada por esse modelo.

**Parte B — resultado:** a matriz de confusão e uma leitura: a favor de quem o modelo erra?

> A matriz de confusão foi [[VN: 319, FP: 0], [FN: 34, VP: 1]]: das 35 postagens que realmente viralizaram no conjunto de teste, o modelo identificou apenas 1 e deixou passar 34 sem perceber (recall de aproximadamente 0,03). Por outro lado, das 1 vez em que o modelo apostou em "viral", ele estava certo (precisão de 1,00), mas com uma única aposta essa precisão não é confiável. O modelo portanto não teve nenhum falso positivo, e teve 319 verdadeiros negativos. Ou seja, o modelo erra fortemente a favor de dizer "não viralizou": ele quase nunca aposta em viral, visto que ele eixou 34 posts virais passarem despercebidos, e por isso deixa passar a grande maioria dos posts que realmente bombaram. 

**Parte C — resultado:** quantos segmentos, como você escolheu `k`, e a descrição de cada segmento (uma frase com número).

> Escolhi segmentar criadores e dividi eles em 4 grupos. Escolhi `k` 4 pois a silhueta média fica em 0,665 para `k` = 4, praticamente igual até `k` = 7 (0,669), o que indica que criar mais grupos não melhora a separação. Além disso, o gráfico do cotovelo cai com uma certa constancia, então ele não dá uma resposta decisiva sozinho. Com `k` 7, muitos grupos tinham apenas aproximadamente 3 participantes, então eles ficavam muito discrepantes e separados. Também não escolhi `k` 2 ou 3, apesar de terem a silhueta maior, pois agrupariam em um mesmo segmento perfis muitos diferentes de criadores. Diante disso, optei pelo menor número de grupos que mantém a qualidade da separação e que resulta em segmentos que consigo descrever e usar.

**Uma conclusão que os seus dados sustentam** (sem extrapolar para além da sua coleta):

> Segundos os dados analisados percebemos que o tamanho da legenda, o número de hashtags e a data da postagem explicam muito pouco ou nada da taxa de engajamento de um vídeo, pelo menos no modelo linear e de árvore, que foram utilizados nessa análise. Seria interessante testar outras features para ver a diferença entre os resultados. 
> Além disso, pela classificação percebemos que esse modelo erra fortemente para dizer que "não viralizou", o modelo é conservador demais. Esse modelo pode ser até ser útil para uma empresa que não pode apostar em diferentes conteúdos e precisa produzir um post certeiro, porém não seria interessante para uma equipe que precisa apostar em mais de um conteúdo com potencial viral.
> E quanto aos dados analisados na segmentação percebemos que criadores de conteúdo menos ativos nas redes possuem menos seguidores e um engajamento menor (grupo 0), potencialmente são pessoas que estão começando agora a postar ou que não tem uma rotina de postagem, por outro lado os criadores mais ativos (grupo 2) possuem engajamento razoável, não muito alto, aparentam, pelos dados analisados, ter presença mas não serem bombados ou virais. Percebi também que os criadores com engajamento maior (grupos 1 e 3) não postam com tanta frequencia mas tem presença, as métricas deles refletem que os "poucos" vídeos que postaram tiveram um alcance muito bom. 
> Na segmentação, os criadores menos ativos na minha coleta apresentaram menos seguidores e menos curtidas. Uma hipótese é que sejam pessoas que estão começando agora a postar ou que não têm uma rotina de postagem, mas não tenho dados sobre a data de criação das contas para confirmar isso. Os criadores mais ativos tiveram engajamento razoável, mas não muito alto, o que sugere que têm presença na plataforma sem que seus vídeos tenham se tornado virais. Já os criadores com maior engajamento aparecem na minha coleta com poucos vídeos, cujas métricas indicam um alcance muito bom. Vale observar que o número de vídeos de cada criador é a contagem dentro da minha amostra, e não do total do perfil, então esse padrão pode refletir a forma como os dados foram coletados e não necessariamente a frequência real de postagem. Nos dados coletados, postar mais não veio acompanhado de maior engajamento, e criadores com poucos vídeos na amostra chegaram a ter as métricas mais altas. Isso é uma associação observada na minha amostra e não permite concluir que a frequência de postagem cause (ou deixe de causar) um perfil viral. 
> É fundamental esclarecer que os achados se referem apenas aos dados coletados e têm limitações. Os plays não são as impressões reais, pois não temos acesso às métricas de alcance dos criadores, apenas aos dados públicos que qualquer pessoa consegue observar. Os vídeos também têm idades diferentes, e vídeos mais antigos tendem a acumular mais views e curtidas, o que pode distorcer as comparações, além de a coleta ser uma foto de um momento, já que as métricas continuam mudando com o tempo. Por isso, o que apresento são hipóteses dentro da minha coleta, e não conclusões gerais sobre os criadores de maquiagem no TikTok. Para quem quer produzir conteúdo de maquiagem, esta análise permite dizer que, nos dados coletados, o tamanho da legenda, o número de hashtags e a data de postagem não bastam para prever o engajamento, e que postar com mais frequência não garante mais alcance. Ela não permite dizer o que faz um vídeo viralizar, porque o modelo não conseguiu antecipar os vídeos virais e fatores como o público do criador e o próprio conteúdo do vídeo não foram analisados.

**Revisão por pares:** nome do colega **da turma** que revisou, o que ele apontou, e o que você mudou (ou por que não mudou).

> Revisado por: João Vianna: Você poderia ter detalhado mais o período da coleta, trazendo qual a data de publicação do primeiro vídeo e do último vídeo da amostra. Trazer exatamente o que é cada um desses valores da matriz de confusão (ex: VN: 319). Gostei bastante da análise da matriz, parabéns. Uma mudança que faria era expandir a coleta, ou seja, trazer mais vídeos, tendo que o percentil de viralização usado é o de 90%, ter uma amostra mais robusta garantiria um número maior de vídeos "viralizados” e assim conseguiríamos fazer uma obsevação melhor da eficácia desses modelos.

> A partir da revisão do João deixei a explicação da matriz de confusão mais completa e analisei a data mais antiga e mais recente da minha coleta com `min()`e `max()`.

**Declaração de uso de IA:** ferramenta usada, em que trecho ou decisão, e o que você conferiu ou alterou depois (mesmo que seja "não usei IA nesta entrega"). Lembre: nesta entrega, IA não pode ser usada para gerar o código de análise.

> Nessa entrega usei IA para interpretar melhor conceitos e delinear pensamentos, mas não para escrever nem criar códigos. Usei também códigos e análises que eu havia feito anteriormente nas aulas 11, 12 e 13.

**obs para o Mateus**
Não estou muito confiante com essa minha entrega, mas queria dizer que me esforçei muito para dar conta de me atualizar das 6 aulas que perdi por conta do processo de trainee. Fiz questão de fazer as aulas anteriores e aprender os conceitos em dois dias, foi difícil e imagino que tenham ficado algumas lacunas, mas realmente me esforçei como prometi a você! Não é um obs para ganhar mais nota rs, é para dizer que prometi a você que ia dar conta e foi difícil mas dei meu máximo. Sei que essa análise não está perfeita, mas tentei meu melhor com o tempo que tive e espero não decepcionar :)
