# Resumo Executivo

## O problema

Órgãos de saúde precisam priorizar quais vírus merecem atenção especial, haja vista a quantidade de vírus catalogados crescer constantemente. Fazer essa triagem manualmente é demorado.

O objetivo deste projeto foi responder a uma pergunta prática: dado o perfil de um vírus, ele representa alto risco para saúde pública ou não?

## A abordagem

Trabalhei com uma base de 70 vírus catalogados, contendo informações biológicas (como família, tipo de genoma) e epidemiológicas (como taxa de mortalidade, forma de transmissão).

O projeto seguiu três etapas:

1. **Limpeza e organização dos dados** — identifiquei e corrigi problemas como registros duplicados, erros de digitação, valores impossíveis (mortalidade negativa ou acima de 100%) e ausência de informações em parte dos registros.

2. **Análise exploratória** — investiguei os padrões que diferenciam vírus de alto risco dos demais, pra entender o que o modelo precisaria aprender.

3. **Construção do modelo preditivo** — testei diferentes algoritmos pra escolher aquele que melhor identifica vírus de alto risco, dada a natureza desafiadora da base.

## Principais achados

- A taxa de mortalidade é, de longe, o fator mais determinante para identificar alto risco. Vírus de alto risco têm mortalidade entre 80% e 99%.

- A base tem apenas 2 vírus classificados como alto risco entre os 70 registros (HIV e Raiva). Esse desbalanceamento severo limita a capacidade do modelo de generalizar para perfis muito diferentes desses dois vírus.

- Identifiquei um registro na base com mortalidade de 99,9% mas classificado como baixo risco. A inconsistência é forte indicativo de erro de rotulagem nesse registro específico, e mereceria revisão por um especialista em um cenário real.

- 58% dos vírus da base não têm caracterização biológica completa. Em vez de descartar mais da metade dos registros, optei por tratar essa ausência de informação como uma categoria própria, preservando os dados pro modelo.

## A solução

O modelo escolhido foi capaz de identificar corretamente os dois vírus de alto risco presentes na base, com apenas um alerta adicional. Curiosamente, esse "alerta extra" é exatamente o registro com a inconsistência mencionada acima, o que mostra que o modelo está fazendo o trabalho dele, apenas refletindo um problema que existe nos dados originais.

Logo: o modelo não deixa passar vírus perigosos.

A solução foi construída sobre uma base pequena, com pouquíssimos exemplos de vírus de alto risco. Isso significa que:

- O modelo aprendeu o padrão a partir de 2 vírus específicos e generaliza bem pra perfis similares
- Vírus de alto risco com características muito diferentes de HIV e Raiva podem não ser identificados pelo modelo
- A solução deve ser usada como triagem inicial, não como decisão final
- Conforme novos vírus de alto risco forem entrando, o modelo pode ser atualizado e ficar mais robusto

## Impacto esperado

A solução serve como uma primeira camada de triagem que ajuda a priorizar quais vírus merecem investigação mais aprofundada, reduzindo o tempo gasto na análise inicial de grandes volumes de dados.

## Recomenda-se os seguintes passos

- Expandir a base com mais exemplos de vírus de alto risco, especialmente com características diversas
- Revisar registros sinalizados como inconsistentes pelo modelo, com apoio de especialistas da área
- Validar a solução em um cenário controlado antes de uso em produção
- Retreinar o modelo periodicamente conforme novos vírus forem catalogados