
# A Viagem de Chihiro · Kit de Lógica

Projeto da disciplina **Lógica para Computação**: um pequeno "kit de lógica proposicional" programado em JavaScript e aplicado a um problema-contexto inspirado no filme *A Viagem de Chihiro* (Studio Ghibli).

🔗 **Site publicado:** [l](https://)ink

👥 **Grupo:** Larissa Rademaker Gabriel, Alessandro dos Santos, Yuri Kauã e Matheus Rodrigues Silva.

---

## O que o projeto faz

O programa modela nove acontecimentos do filme como variáveis lógicas (verdadeiro = aconteceu, falso = não aconteceu) e cinco restrições que dizem quais versões da história são possíveis. A página permite:

- alternar o valor de cada variável e ver quais restrições são respeitadas;
- testar as **512 valorações possíveis** (2⁹) por força bruta;
- converter fórmulas para **Forma Normal Conjuntiva (FNC)**;
- rodar testes automáticos que conferem se tudo está correto.

## Como usar

1. Baixe ou clone o repositório.
2. Abra o arquivo `chihiro-projeto.html` no navegador. Não precisa instalar nada.
3. Para publicar no GitHub Pages, renomeie o arquivo para `index.html`, envie ao repositório e ative o Pages em *Settings → Pages*.

### Imagens das variáveis

Cada variável tem um cartão com espaço para uma imagem. Crie uma pasta `imagens` ao lado do HTML com os arquivos:

```
imagens/A.png   imagens/B.png   ...   imagens/I.png
```

Se a imagem não existir, o cartão mostra um emoji no lugar. Também é possível clicar na imagem de um cartão para testar uma figura na hora (a escolha vale só naquele navegador). Para usar `.jpg`, troque a constante `EXT` no começo do script.

## As variáveis

| Letra | Significado                                    |
| ----- | ---------------------------------------------- |
| A     | Chihiro acerta quem são os pais (porcos)      |
| B     | Chihiro vai embora com os pais em forma humana |
| C     | Yubaba entrega o contrato                      |
| D     | Chihiro tem emprego                            |
| E     | Chihiro está salva                            |
| F     | Chihiro prende a respiração na ponte         |
| G     | Chihiro come a frutinha                        |
| H     | Chihiro desaparece                             |
| I     | Chihiro esquece quem é e seus pais            |

## As restrições

| #  | Fórmula                                                      | Em palavras                                      |
| -- | ------------------------------------------------------------- | ------------------------------------------------ |
| R1 | `G → ¬H`                                                  | Quem come a frutinha não desaparece             |
| R2 | `C → D`                                                    | Receber o contrato leva a ter emprego            |
| R3 | `H → ¬E`                                                  | Quem desaparece não está salva                 |
| R4 | `I → ¬B`                                                  | Esquecer quem é impede de ir embora com os pais |
| R5 | `[({(G → ¬H) ∧ [F ∨ (C → D)]} → E) ∧ A ∧ ¬I] → B` | A regra principal do filme                       |

Há também uma **variante insatisfatível**: com os fatos `A`, `¬I`, `E` e `¬B`, nenhuma versão do filme respeita as restrições, e o programa mostra "IMPOSSÍVEL".

## Requisitos do desafio e onde estão no código

Tudo está em um único arquivo, `chihiro-projeto.html`, com o código comentado.

| Requisito                                                                                                                                | Onde                                                       |
| ---------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------- |
| **R1** Estrutura de dados para fórmulas (árvore sintática com ¬, ∧, ∨, →, ↔)                                               | Funções`V`, `Not`, `And`, `Or`, `Imp`, `Iff` |
| **R2** Impressão infixa com parênteses e avaliação                                                                             | `pr` (imprime) e `ev` (avalia)                         |
| **R3** Busca de modelos por força bruta (satisfatível, modelo, contagem, válida/contingente/insatisfatível)                    | `vals` e `busca`                                       |
| **R4** Conversão para FNC (eliminar → e ↔, forma normal da negação, distribuição)                                           | `sem`, `nnf`, `dist`, `limpa`, `fnc`             |
| **R5** Problema-contexto com 5+ variáveis, 5+ restrições e uma variante insatisfatível, com solução em linguagem do problema | Constantes`R`, `W`, `FATOS` e a função `buscaUI` |
| **R6** Testes (tautologia, contradição, contingente) e verificação de que a FNC é equivalente à original                     | Lista`TS` e a função `testes`                        |

Nenhuma biblioteca de lógica foi usada: tudo foi programado do zero.

### Extras

- **Visualização interativa:** os cartões com imagem e botão verdadeiro/falso mostram, em tempo real, quais restrições são respeitadas.
- Parser de fórmulas em texto, DPLL e Tseitin/DIMACS **não foram implementados**.

## Testes incluídos

A seção "Testes" da página executa 7 casos ao abrir. Cada um classifica a fórmula, gera a FNC e compara as tabelas-verdade da FNC e da original:

1. Tautologia: `p ∨ ¬p`
2. Contradição: `p ∧ ¬p`
3. Contingente: `p → q`
4. De Morgan: `¬(p ∧ q) ↔ (¬p ∨ ¬q)`
5. Bicondicional contraditório: `(p ↔ q) ∧ ¬(p → q)`
6. Contingente com três variáveis: `(p → q) ↔ r`
7. Regra principal do filme (R5)

## Tecnologias

HTML, CSS e JavaScript puros (sem frameworks). As fontes (Nunito e Shippori Mincho) vêm do Google Fonts e precisam de internet; há fontes reserva caso não carreguem.

## Créditos

- Projeto desenvolvido para a disciplina **Lógica para Computação**, a partir das especificações do desafio de programação "Aspectos Computacionais da Lógica".
- O código, a revisão dos requisitos, o visual e este README foram feitos com a ajuda do **Claude**, assistente de IA da [Anthropic](https://www.anthropic.com).
- Filme *A Viagem de Chihiro* © Studio Ghibli. As referências ao filme e as imagens têm fins exclusivamente educacionais.
