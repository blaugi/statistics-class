
PASSO 1: Comentário entre 6’48” e 6’58” no vídeo da Socratica.
A narradora diz: "Observe that walks with an even number of blocks leave you closer to home than walks one block shorter. In general, even walks end closer to home than odd walks."

**Por que isso acontece?**

Isso está relacionado à **paridade** e à possibilidade de retornar à origem (0,0) ou ficar muito próximo dela.

1.  **Retorno à Origem (0,0):**
    *   Para retornar à origem (0,0) em uma grade 2D, o número de passos para o Norte (N) deve ser igual ao número de passos para o Sul (S), E o número de passos para o Leste (E) deve ser igual ao número de passos para o Oeste (O).
    *   Seja $n_N$, $n_S$, $n_E$, $n_O$ o número de passos em cada direção.
    *   Para terminar em x=0: $n_E = n_O$.
    *   Para terminar em y=0: $n_N = n_S$.
    *   O número total de passos $n = n_N + n_S + n_E + n_O$.
    *   Se o caminhante retorna à origem, então $n = 2*n_N + 2*n_E = 2 * (n_N + n_E)$.
    *   Isso significa que o número total de passos $n$ **deve ser par** para que o caminhante tenha a possibilidade de terminar na origem (0,0).

2.  **Caminhadas Ímpares vs. Pares:**
    *   **Se $n$ é ímpar:** É impossível terminar na origem (0,0). A distância mínima da origem será de 1 bloco (por exemplo, em (1,0), (-1,0), (0,1) ou (0,-1)).
    *   **Se $n$ é par:** É possível terminar na origem (0,0). Além disso, há uma maior concentração de probabilidades em torno da origem para caminhadas pares.

Em resumo, a paridade do número de passos determina se é possível ou não retornar à origem. Caminhadas com um número par de passos têm a origem como uma posição final possível e uma distribuição de probabilidade mais concentrada em torno dela, levando a uma maior chance de terminar "perto de casa" em comparação com caminhadas de número ímpar de passos, que garantem uma distância de pelo menos um bloco da origem.

---

PASSO 2: No notebook `step2.ipynb`

---

PASSO 3: No notebook `step3.ipynb`

---

PASSO 4: Considerações comparativas entre resultados de grade hexagonal e quadrada.

1.  **Conectividade e Dimensões Efetivas:**
    *   **Quadrada:** 4 vizinhos. O movimento é restrito aos eixos cartesianos.
    *   **Hexagonal:** 6 vizinhos. A grade hexagonal é, em certo sentido, "mais densa" ou oferece mais direções de movimento. Cada passo em uma grade hexagonal pode ser visto como um movimento que tem componentes ao longo de três eixos (se usarmos um sistema de 3 eixos com q+r+s=0), embora seja um espaço 2D. Isso permite um movimento mais "isotrópico" (similar em todas as direções).

2.  **Difusão (Espalhamento):**
    *   Em uma grade hexagonal, com mais vizinhos, um caminhante aleatório tende a se espalhar (difundir) da origem de forma ligeiramente diferente do que em uma grade quadrada.
    *   **Para a grade quadrada**, a distância média da origem após `N` passos é proporcional a `sqrt(N)`.
    *   **Para a grade hexagonal**, a mesma relação `sqrt(N)` para a distância média da origem também se aplica, mas a constante de proporcionalidade ou a forma exata da distribuição de probabilidade para pequenas distâncias pode ser diferente.
    *   Intuitivamente, com mais direções para "escapar" da vizinhança imediata, mas também mais direções para retornar, o efeito líquido na probabilidade de estar perto da origem é complexo.

3.  **Distância Métrica:**
    *   Quadrada: Distância de Manhattan `d = |x| + |y|`.
    *   Hexagonal: Distância hexagonal `d = (|q| + |r| + |-q-r|) / 2`.
    *   Para o mesmo número de passos `n`, as distâncias máximas alcançáveis são `n` em ambas as grades.

4.  **Resultados da Simulação para o Desafio (P(distância <= 4) > 50%):**
    *   **Grade Quadrada (vídeo Socratica):** Aproximadamente 22 blocos.
    *   **Grade Hexagonal (minha simulação):** Aproximadamente 29 ou 30 blocos.

5.  **Interpretação da Diferença nos Resultados do Desafio:**
    *   O fato de a caminhada hexagonal permitir um número maior de passos (29-30 vs. 22) antes que a probabilidade de estar a 4 blocos ou menos caia abaixo de 50% sugere que, na grade hexagonal, o caminhante **permanece relativamente mais próximo da origem por mais tempo** ou, equivalentemente, **difunde-se mais lentamente para longe da origem em termos de probabilidade de estar a uma curta distância**.
    *   **Por que isso acontece?**
        *   **Paridade e Retorno à Origem:** Assim como na grade quadrada, para retornar à origem (0,0) em uma grade hexagonal, o número total de passos `n` deve ser par. Isso ocorre porque cada passo muda a soma `q+r+s` (que é sempre 0) de forma que a paridade de `q`, `r`, `s` muda. Para `q,r,s` serem todos pares (como em (0,0,0)), `n` deve ser par. Isso explica a oscilação observada nas probabilidades para comprimentos de caminhada pares vs. ímpares (similar ao vídeo da grade quadrada).
        *   **Forma da "Bola" de Alcance:** Em uma grade quadrada, após `n` passos, os pontos alcançáveis formam um "diamante" rotacionado. Em uma grade hexagonal, os pontos alcançáveis formam um hexágono. A distribuição de probabilidade dentro dessas formas é o que importa.
        *   **Menor "tendência" a se afastar rapidamente:** Com 6 vizinhos, há mais opções de movimento. Em uma grade quadrada, se você se move em uma direção (ex: Leste), para retornar, você precisa de um movimento oposto (Oeste). Em uma grade hexagonal, se você se move Leste (1,0), há duas direções (Noroeste (0,-1) e Sudoeste (-1,1)) que têm um componente "para trás" na direção q, e duas direções (Oeste (-1,0)) que são diretamente para trás. Essa maior conectividade e direções "oblíquas" podem contribuir para uma exploração mais eficiente do espaço próximo à origem, resultando em uma maior probabilidade de permanecer perto dela por mais tempo.

6.  **Conclusão Comparativa:**
    A grade hexagonal, devido à sua maior conectividade (6 vizinhos vs. 4), parece permitir que o caminhante aleatório permaneça dentro de um raio específico (como 4 blocos) com uma probabilidade >50% por um número maior de passos em comparação com a grade quadrada. Isso indica que a "taxa de escape" ou a rapidez com que a probabilidade de estar longe da origem aumenta é um pouco menor na grade hexagonal para o critério específico do desafio. As oscilações de paridade (caminhadas pares tendem a ter maior probabilidade de estar perto da origem do que caminhadas ímpares adjacentes) são observadas em ambas as grades.