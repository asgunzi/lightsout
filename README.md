# Implementação do Ligths Out em Javascript D3

O objetivo deste projeto é criar uma versão do jogo “Lights Out”, algo como “Apague as luzes”.

A partir de um painel inicial, 5×5, devo apagar todas as luzes. O amarelo indica aceso, azul significa apagado.

![](https://ideiasesquecidas.files.wordpress.com/2023/08/light01.png)

Implementei em Javascript – D3. Jogue aqui no link: [https://asgunzi.neocities.org/ArteMatematica/luzes](https://asgunzi.neocities.org/ArteMatematica/luzes).

Código fonte aqui nos arquivos do Github.


Se eu tocar num quadrado, a célula tocada, as adjacentes superior, inferior, direita e esquerda mudam de estado: se apagadas ficam acesas, e vice-versa.

Por exemplo, digamos que eu toque bem no centro do tabuleiro, com todas as luzes apagadas. A peça do centro e as vizinhas de cima, de baixo, direita e esquerda se acenderão.

![](https://ideiasesquecidas.files.wordpress.com/2023/08/light02.png)


Para a inicialização, iniciamos com uma função que, aleatoriamente, atribui ligado ou desligado às luzes. Porém, nem todas as situações são resolvíveis. Somente um quarto dos tabuleiros inicializados desta maneira têm solução. Como saber qual terá ou não solução?

Usamos o teste descrito no paper de Anderson e Feil https://people.sc.fsu.edu/~jburkardt/classes/imps_2017/11_28/2690705.pdf

Se o produto escalar do tabuleiro e dois vetores especiais n1 e n2 der zero, na base 2, a configuração é resolvível.

              

                var n1 = [[0, 1, 1, 1, 0], [1, 0, 1, 0, 1], [1, 1, 0, 1, 1], [1, 0, 1, 0, 1], [0, 1, 1, 1, 0]];

                var n2 = [[1, 0, 1, 0, 1], [1, 0, 1, 0, 1], [0, 0, 0, 0, 0], [1, 0, 1, 0, 1], [1, 0, 1, 0, 1]];

Se o tabuleiro não tiver solução, reiniciamos e procuramos outra configuração, até achar alguma que tenha solução.

               

A cada inicialização, uma nova configuração resolvível será apresentada.

![](https://ideiasesquecidas.files.wordpress.com/2023/08/light03.png)

## Spoiler: como resolver o jogo das luzes apagadas
Para a resolução do jogo das luzes apagadas, há um procedimento relativamente simples, chamado “caça às luzes”. Comece na segunda linha. Clique abaixo da luz da linha de cima, de forma a apagá-la. Repita, até chegar à última linha.

Na última linha, há algumas situações possíveis. Proceder da seguinte forma:

– Primeira, segunda e terceira células da última linha ligadas: clique na segunda célula da primeira linha

– Primeira, segunda, quarta e quinta células da última linha ligadas: clique na terceira célula da primeira linha

– Primeira, terceira e quarta células da última linha ligadas: clique na quinta célula da primeira linha

– Primeira e quinta células da última linha ligadas: clique na primeira  e segunda células da primeira linha

– Segunda, terceira e quinta células da última linha ligadas: clique na primeira célula da primeira linha

– Segunda e quarta células da última linha ligadas: clique na primeira e quarta células da primeira linha

– Terceira, quarta e quinta células da última linha ligadas: clique na quarta célula da primeira linha

Daí, proceder o mesmo algoritmo de caça à luzes do passo 1, até resolver completamente!

![](https://ideiasesquecidas.files.wordpress.com/2023/08/light04.png)

Tabuleiro completamente resolvido!
