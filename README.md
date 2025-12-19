# IC_Informatividade_PLN-
Projeto de Iniciação Científica em Linguística Computacional que analisa respostas não esperadas em diálogos do português brasileiro, combinando critérios semântico-pragmáticos e modelos de PLN supervisionados.

Este projeto investiga respostas subinformativas, sobreinformativas e completas em diálogos do português brasileiro, a partir de uma perspectiva semântico-pragmática e computacional. O foco recai sobre respostas não esperadas a perguntas polares (sim/não), que aparentam violar a Máxima de Quantidade do Princípio Cooperativo de Grice (1975).

A pesquisa parte de dados experimentais oriundos de um estudo psicolinguístico, que mediu tempos de reação associados a diferentes tipos de resposta, e avança para uma abordagem de Linguística Computacional. O objetivo é desenvolver um modelo supervisionado capaz de classificar automaticamente pares pergunta–resposta segundo seu grau de informatividade (subinformativa, sobreinformativa ou completa), integrando critérios linguísticos explícitos e técnicas de Processamento de Linguagem Natural.

Inicialmente, os dados são anotados por meio de regras linguísticas inspiradas na literatura em semântica e pragmática, considerando propriedades como número de alternativas na pergunta, extensão da resposta e presença de quantificadores universais. Em seguida, os dados anotados são utilizados para treinar modelos computacionais, incluindo abordagens de baseline (TF-IDF + regressão logística) e modelos baseados em embeddings contextuais (BERTimbau).

A avaliação dos modelos é realizada por meio de métricas descritivas (acurácia, precisão, revocação e F1-score), bem como análises inferenciais que permitem comparar o desempenho entre diferentes abordagens. Os resultados são discutidos à luz de teorias semântico-pragmáticas, buscando compreender como inferências pragmáticas podem ser modeladas computacionalmente.

O projeto está organizado em pastas que separam dados, notebooks, scripts, modelos treinados e resultados, de modo a garantir reprodutibilidade e clareza metodológica.
