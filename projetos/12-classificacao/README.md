## Parte 5 — README de reprodução

Crie `README.md` dentro de `projetos/12-classificacao/` na sua pasta de entregas:

**Fonte e período dos dados; quantos posts entraram:**

> Posts do TikTok coletados pelo Zeeschuimer, em agosto de 2026.

**Como você definiu "viralizou", e por quê:**

> Escolhi plays no percentil 90 como corte de 'viralizou' porque é a métrica mais completa da base e resulta numa classe viral pequena (10%), mas com exemplos suficientes para o modelo treinar.

**Quantos posts ficaram como "viral" (a classe é rara?):**

> 140, sim é uma classe rara visto que a coleta total tem mais de 1400 posts.

**Features usadas; colunas descartadas por vazamento:**

> Features usadas: seguidores do autor, tamanho da legenda, número de hashtags e horário. Colunas descartadas por vazamento: likes, comments, shares e plays.

**Matriz de confusão do seu melhor modelo, e uma leitura: a favor de quem ele erra?** (deixa passar muitos virais = recall baixo; ou dá muito alarme falso = precisão baixa)

> A matriz de confusão foi [[317, 2], [33, 2]]: das 35 postagens que realmente viralizaram no conjunto de teste, o modelo só identificou 2 e deixou passar 33 sem perceber (recall de 0,06). Por outro lado, das 4 vezes que o modelo apostou em 'viral', 2 estavam certas (precisão de 0,50). Ou seja, meu modelo erra fortemente a favor de dizer 'não viralizou': ele quase nunca aposta em viral, e por isso deixa passar a grande maioria dos posts que realmente bombaram. Isso seria ruim para uma equipe que não pode se perder um post promissor, mas seria aceitável para um uso em que cada alarme de 'viral' tem um custo alto e por isso só vale a pena confiar quando o modelo tem bastante certeza.

**O que mudou quando você baixou o threshold:**

> Quanto mais baixei o threshold mais conteúdos virais foram captados, porem a quantidade de alarmes falsos subiu consideravelmente, ou seja, mais vídeos foram considerados virais mas a presição diminuiu consideravelmente.

**Declaração de uso de IA:** ferramenta usada, em que trecho ou decisão, e o que você conferiu ou alterou depois (mesmo que seja "não usei IA nesta entrega").

> Usei o Claude e pedi para ele me explicar o conceito como se eu fosse uma criança, porque foi difícil entender. Mas entendi!