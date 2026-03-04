<p align="justify"><h1>Otimização de Cobertura em Telefonia Celular (Set Cover Problem)</h1></p>

<p align="justify">O modelo implementado visa resolver o <b>Problema de Cobertura de Conjuntos</b> aplicado à infraestrutura de telefonia celular. Este é um desafio clássico de otimização onde buscamos a melhor distribuição de recursos para cobrir uma área demarcada. Abaixo, detalhamos os componentes matemáticos e os principais desafios operacionais encontrados no desenvolvimento.</p>

<p align="justify"><h3>1. Definição do Problema</h3></p>

<p align="justify">O objetivo central é determinar a configuração de antenas de menor custo capaz de fornecer sinal para uma área geográfica contínua. Essa área é representada por uma grade de pontos discretos que devem ser obrigatoriamente atendidos pelo sinal. Trata-se de um problema de <b>Programação Linear Inteira</b> (MILP), onde as decisões são binárias (sim ou não). Cada antena candidata é ou instalada completamente em sua capacidade total (1), ou é descartada (0).</p>

<p align="justify"><h3>2. Função Objetivo: O que minimizamos?</h3></p>

<p align="justify">A função objetivo busca a <b>Minimização do Custo Total de Implementação</b> do sistema de antenas. No modelo proposto, o custo está diretamente atrelado ao esforço físico e ao alcance de cada unidade instalada:</p>

<p align="justify">1. <b>Variável de Decisão (xi​):</b> Assume valor 1 se a antena i for selecionada e 0 caso contrário.</p>

<p align="justify">2. <b>Peso do Custo (ci​):</b> Definido como ci​=πri2​, penalizando antenas com raios maiores e áreas de cobertura mais extensas.</p>

<p align="justify">3. <b>Equilíbrio:</b> O solver busca um balanço entre poucas antenas grandes (caras) versus várias antenas pequenas (mais baratas).</p>

<p align="justify">4. <b>Equação Matemática:</b> O modelo resolve a somatória dada por min∑(ci​⋅xi​).</p>

<p align="justify"><h3>3. As Restrições: O que limita a solução?</h3></p>

<p align="justify">A principal barreira matemática é a <b>Garantia de Conectividade Total</b> em todos os pontos da malha geográfica definida.</p>

<p align="justify">1. <b>Matriz de Incidência (A):</b> Relaciona cada ponto da grade com as antenas que conseguem efetivamente alcançá-lo.</p>

<p align="justify">2. <b>Critério de Cobertura:</b> Se a distância entre o ponto e o centro da antena for menor ou igual ao raio, o valor na matriz é 1.</p>

<p align="justify">3. <b>Cobertura Mínima:</b> Para cada ponto j na grade, a soma das antenas que o cobrem deve ser maior ou igual a 1, ou seja: ∑Aji​xi​≥1.</p>

<p align="justify">4. <b>Complexidade:</b> Variáveis binárias x∈{0,1} impedem soluções fracionárias, tornando o problema classificado como <b>NP-Hard</b>.</p>

<p align="justify"><h3>4. Problemas de Inviabilidade (Infeasibility)</h3></p>

<p align="justify">O status de <b>Inviabilidade</b> ocorre quando o solver prova que as restrições não podem ser atendidas simultaneamente.</p>

<p align="justify">1. <b>Lacunas Geográficas:</b> Se o número de candidatos for baixo, podem surgir pontos na grade inalcançáveis por qualquer antena.</p>

<p align="justify">2. <b>Rigidez do Modelo:</b> A exigência de cobertura de 100% dos pontos torna o problema impossível se houver um único ponto isolado.</p>

<p align="justify">3. <b>Falha de Solver:</b> Quando o problema é inviável, o solver não gera valores, resultando no erro de <b>NoneType</b> no Python.</p>

<div>
<p align="justify">4. <b>Parâmetros Aleatórios:</b> Como os centros são sorteados, a viabilidade depende da distribuição inicial das antenas no plano.</p>
</div>
