# Projeto 4: Clipping comparativo de Lula e Flávio Bolsonaro

## 1. Objetivo e pergunta

Pergunta: o que este recorte de notícias da Agência Brasil e da CNN Brasil mostra sobre a cobertura de Lula e Flávio Bolsonaro?

A ideia foi transformar títulos e resumos em dados que dá pra conferir (texto preparado, tópicos, menções, fichas da IA e buscas) e tirar conclusões só do tamanho que a amostra permite.

- **Fonte:** base `noticias_lula_flavio_2026.csv`, do repositório da disciplina, com título, resumo, data, link e `texto_analise` (título + resumo). Não tem as matérias completas.
- **Janela temporal:** 03/10/2026 a 13/10/2026, 16 das 20 matérias da CNN Brasil são do dia 13/10.
- **Regra de seleção:** 10 matérias por combinação de veículo e foco. O foco é o motivo de a matéria entrar na base, não uma avaliação de tom. Não é uma amostra aleatória, então não mostra quanto cada veículo publicou sobre cada candidato.

| Veículo | Foco Lula | Foco Flávio Bolsonaro |
| Agência Brasil | 10 | 10 |
| CNN Brasil | 10 | 10 |

## 2. Preparação

Usei a função `preparar()` da Aula 21 para criar `texto_preparado`, mantendo `texto_analise` intacto. A função passa tudo para minúsculas, tira URLs e deixa só palavras. Não tirei stopwords nem lematizei, para não perder negações e nomes próprios. A base não tem textos vazios nem duplicatas, e a média caiu de 32,0 para 31,6 tokens por matéria. Nos casos lado a lado, P05 mantém o "não encontram", P11 mantém os nomes próprios e P29 mostra uma perda: "6x1" e "2º" somem porque são números.

## 3. Revisão de 21 e 22

Da Aula 21 usei a preparação com regex, a comparação antes e depois e as palavras frequentes com `Counter`. Da Aula 22 usei TF-IDF e NMF, a leitura das manchetes de maior peso antes de dar nome aos tópicos e o `nsmallest` para achar os casos de menor confiança. Tirei o filtro de 300 caracteres da Aula 22, porque aqui os textos são curtos, e usei os parâmetros do TF-IDF da Aula 23, feitos para esta base.

## 4. Roteiro de análise

1. Conferir as 40 linhas e o equilíbrio 10×4.
2. Preparar o texto e medir o efeito da limpeza.
3. Rodar TF-IDF e NMF com 4 tópicos e `random_state=42`, nomear os tópicos e cruzar com veículo e foco.
4. Contar menções a Lula e Flávio por grupo.
5. Extrair fichas com a Groq em 16 matérias (4 por grupo) e auditar 4.
6. Comparar busca por palavra e busca semântica com a mesma pergunta.

## 5. Prática aplicada

**Tópicos:** 0 é reta final do 2º turno e visitas ao pai (P39, P38, P37), 1 é Justiça Eleitoral e canal Exército do Lula (P05, P27, P09), 2 é atos de rua e apoios (P04, P15, P06) e 3 é misto (P26, P01, P16).

| Veículo | Foco | Tópico 0 | Tópico 1 | Tópico 2 | Tópico 3 |
| Agência Brasil | Flávio | 1 | 0 | 6 | 3 |
| Agência Brasil | Lula | 0 | 3 | 4 | 3 |
| CNN Brasil | Flávio | 6 | 2 | 1 | 1 |
| CNN Brasil | Lula | 2 | 2 | 3 | 3 |

**Tópico confuso:** o tópico 3 mistura custo de vida (P26), religião (P01), criptomoedas (P16) e pesquisa (P23). Acho que ele juntou palavras genéricas como "campanha", e não um assunto.

**Menções (denominador 10 por grupo):**

| Veículo | Foco | Menções a Lula | Menções a Flávio |
| Agência Brasil | Flávio | 6 | 13 |
| Agência Brasil | Lula | 13 | 4 |
| CNN Brasil | Flávio | 6 | 11 |
| CNN Brasil | Lula | 10 | 2 |

**Extração:** as 16 evidências são trechos literais do texto. Mas em geral o fato e a evidência são só o título copiado, então passar nesse teste é fácil.

| ID | Grupo | Problema encontrado |
| P12 | Agência Brasil, Flávio | Ausência: deixa de fora que ele aguarda horário para visitar o pai. |
| P02 | Agência Brasil, Lula | Atribuição ambígua: põe Lula como pessoa central, mas o ato foi dos apoiadores. Ausência: ignora a votação da 6x1. |
| P37 | CNN Brasil, Flávio | Atribuição ambígua: a pessoa central deveria ser o Centrão. Ausência: não cita o apoio dos partidos. |
| P28 | CNN Brasil, Lula | Ausência: falta que o TSE suspendeu o grupo até o registro. |

**Buscas:** pergunta "Quais notícias tratam de pesquisas de opinião sobre os candidatos?".

| Método | Top 3 | Relevantes |
| Palavra | P08, P33, P17 | nenhuma |
| Semântica | P24, P21, P03 | só P24 |

A busca por palavra errou porque "sobre" não está nas stopwords e "pesquisas" está no plural, enquanto a base só tem "pesquisa". A semântica achou a [P24](https://www.cnnbrasil.com.br/eleicoes/gerp-lula-e-rejeitado-por-53-dos-eleitores-flavio-por-42/), mas deixou de fora a P23 e trouxe a P21, que fala de apoio de partido e não de pesquisa.

## 6. Resultados do desafio

**Descrição dos dados**

1. Nos dois veículos, as matérias com foco em Flávio citam Lula 6 vezes, e as com foco em Lula citam Flávio 4 vezes (Agência Brasil) e 2 (CNN Brasil). Exemplo: [P17](https://agenciabrasil.ebc.com.br/politica/noticia/2026-10/mendonca-multa-flavio-por-impulsionar-post-negativo-contra-lula), em que Flávio é multado por um post contra Lula.
2. Nas matérias com foco em Flávio, 6 de 10 da Agência Brasil caem em atos e apoios, como [P15](https://agenciabrasil.ebc.com.br/politica/noticia/2026-10/flavio-bolsonaro-diz-que-fara-guerra-ao-crime-organizado), e 6 de 10 da CNN Brasil caem em reta final e visitas ao pai, como [P38](https://www.cnnbrasil.com.br/blogs/jussara-soares/eleicoes/flavio-buscara-orientacao-de-bolsonaro-para-reta-final-dizem-aliados/).

**Interpretação**

O primeiro achado pode ter a ver com o segundo turno, em que o adversário costuma ser noticiado em relação ao presidente, mas a base não permite testar isso. O segundo pode ser diferença de pauta entre os veículos, mas também pode ser efeito da data, já que quase toda a CNN é do dia 13/10, quando Flávio voltou a visitar o pai. Com 10 matérias por grupo, não dá pra falar em viés do jornal.

**Limitações:** só 40 matérias escolhidas, só título e resumo, 11 dias de janela, tópicos instáveis com textos curtos, limpeza que apaga números, contagem que não separa Jair de Flávio quando aparece só "Bolsonaro" e extração auditada em só 4 das 16 fichas.

## 7. Entrega

- `projeto-4-noticias.ipynb`: notebook executado
- `fichas_extraidas.csv`: as 16 fichas da Groq, sem edição (enviei o arquivo salvo do Colab)
- `tabela_topicos.csv` e `tabela_mencoes.csv`: tabelas de resultado (enviei os arquivos salvos do Colab)

A chave Groq foi digitada com `getpass` e não está em nenhum arquivo.

## 8. Declaração de uso de IA

Usei o Claude para discutir as ideias delinear pensamentos (e para deixar os markdowns e esse readme organizados, mandei o que escrevi e ele só estruturou). Usei o modelo `openai/gpt-oss-20b`, pela Groq, para extrair as fichas. A execução do notebook, a leitura das matérias, a auditoria e a avaliação das buscas foram feitas por mim.

## 9. Checklist

- [x] 40 linhas: 10 por veículo × foco.
- [x] Chave pessoal fora dos arquivos entregues.
- [x] Extração em amostra de 16, com quatro auditorias.
- [x] Conclusões citam IDs e links e respeitam o recorte.
- [x] Notebook executa de cima a baixo no Colab.