---
title: Ajuda F1 do Visualizador de Perfil de Dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.dataprofileviewer.f1
helpviewer_keywords:
- Data Profile Viewer [Integration Services]
- Data Profiling task [Integration Services], viewer
ms.assetid: 3469c60a-8f4f-46ba-999a-cb9070197fea
author: chugugrace
ms.author: chugu
ms.openlocfilehash: d541e0c6143c9652629f80d911bf42db26e9a4ef
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85429713"
---
# <a name="data-profile-viewer-f1-help"></a>Ajuda de F1 do Visualizador de Perfil de Dados
  Use o Visualizador de Perfil de Dados para exibir a saída da tarefa Criação de Perfil de Dados.  
  
 Para obter mais informações sobre como usar o Visualizador de Perfil de Dados, consulte [Visualizador de Perfil de Dados](control-flow/data-profile-viewer.md). Para obter mais informações sobre como usar a tarefa Criação de Perfil de Dados, que cria a saída para análise no Visualizador de Perfil de Dados, consulte [Configuração da tarefa Criação de Perfil de Dados](control-flow/data-profiling-task.md).  
  
## <a name="static-options"></a>Opções estáticas  
 **Abrir**  
 Clique para buscar o arquivo salvo que contém a saída da tarefa Criação de Perfil de Dados.  
  
 Painel**Perfis**  
 Expanda a árvore no painel **Perfis** para ver os perfis incluídos na saída. Selecione um perfil para exibir os seus resultados.  
  
 Painel de **mensagens**  
 Exibe mensagens de estado.  
  
 Painel**Busca Detalhada**  
 Exibe as linhas de dados que correspondem a um valor na saída, se a fonte de dados usada pela tarefa Criação de Perfil de dados estiver disponível.  
  
 Por exemplo, se estiver exibindo a saída de um perfil Distribuição de Valor de Coluna para uma coluna Estado dos Estados Unidos da América, o painel **Distribuição de Valor Detalhado** pode conter uma linha para "WA". Clique duas vezes na linha do painel **Distribuição de Valor Detalhado** para ver as linhas de dados nas quais o valor da coluna de estado é “WA” no painel de busca detalhada.  
  
## <a name="dynamic-options"></a>Opções dinâmicas  
  
### <a name="profile-type--column-length-distribution-profile"></a>Tipo de Perfil = Perfil de Distribuição de Comprimento de Coluna  
  
#### <a name="column-length-distribution-profile---column-pane"></a>Perfil de distribuição de comprimento de coluna- \<column> painel  
 **Comprimento Mínimo**  
 Exibe o comprimento mínimo de valores nesta coluna.  
  
 **Comprimento máximo**  
 Exibe o comprimento máximo de valores nesta coluna.  
  
 **Ignorar Espaços à Esquerda**  
 Exibe se este perfil foi computado com um valor `IgnoreLeadingSpaces` de True ou False. Esta propriedade foi definida na página **Solicitações de Perfil** do Editor de Tarefa Criação de Perfil de Dados.  
  
 **Ignorar Espaços à Direita**  
 Exibe se este perfil foi computado com um valor `IgnoreTrailingSpaces` de True ou False. Esta propriedade foi definida na página **Solicitações de Perfil** do Editor de Tarefa Criação de Perfil de Dados.  
  
 **Contagem de linhas**  
 Exibe o número de linhas na tabela ou exibição.  
  
#### <a name="detailed-length-distribution-pane"></a>Painel Distribuição de Comprimento Detalhado  
 **Comprimento**  
 Exibe os comprimentos de coluna localizados na coluna perfilada.  
  
 **Count**  
 Exibe o número de linhas nas quais o valor da coluna cujo perfil está sendo criado tem o tamanho mostrado na coluna **Tamanho** .  
  
 **Porcentagem**  
 Exibe o percentual de linhas nas quais o valor da coluna cujo perfil está sendo criado tem o tamanho exibido na coluna **Tamanho** .  
  
### <a name="profile-type--column-null-ratio-profile"></a>Tipo de Perfil = Perfil de Razão Nula de Coluna  
  
#### <a name="column-null-ratio-profile---column-pane"></a>Perfil de razão nula de coluna- \<column> painel  
 **Contagem Nula**  
 Exibe o número de linhas nas quais a coluna perfilada tem um valor nulo.  
  
 **Porcentagem nula**  
 Exibe a porcentagem de linhas nas quais a coluna cujo perfil está sendo criado tem um valor nulo  
  
 **Contagem de linhas**  
 Exibe o número de linhas na tabela ou exibição.  
  
### <a name="profile-type--column-pattern-profile"></a>Tipo de Perfil = Perfil Padrão de Coluna  
  
#### <a name="column-pattern-profile---column-pane"></a>Painel de Perfil de Padrão de Coluna \<column>  
 **Contagem de linhas**  
 Exibe o número de linhas na tabela ou exibição.  
  
#### <a name="pattern-distribution-pane"></a>Painel Distribuição de Padrão  
 **Padrão**  
 Exibe os padrões computados para a coluna cujo perfil está sendo criado.  
  
 **Porcentagem**  
 Exibe o percentual de linhas cujos valores correspondem ao padrão exibido na coluna **Padrão** .  
  
### <a name="profile-type--column-statistics-profile"></a>Tipo de Perfil = Perfil de Estatísticas da Coluna  
  
#### <a name="column-statistics-profile---column-pane"></a>Perfil de estatísticas de coluna – \<column> painel  
 **Máximo**  
 Exibe o valor mínimo localizado na coluna cujo perfil está sendo criado.  
  
 **Máximo**  
 Exibe o valor máximo localizado na coluna cujo perfil está sendo criado.  
  
 **Significa**  
 Exibe a média dos valores encontrados na coluna cujo perfil está sendo criado.  
  
 **Desvio padrão**  
 Exibe o desvio padrão dos valores encontrados na coluna cujo perfil está sendo criado.  
  
### <a name="profile-type--column-value-distribution-profile"></a>Tipo de Perfil = Perfil de Distribuição de Valor da Coluna  
  
#### <a name="column-value-distribution-profile---column-pane"></a>Perfil de distribuição de valor de coluna- \<column> painel  
 **Número de Valores Distintos**  
 Exibe a contagem de valores distintos encontrados na coluna cujo perfil está sendo criado.  
  
 **Contagem de linhas**  
 Exibe o número de linhas na tabela ou exibição.  
  
#### <a name="detailed-value-distribution-pane"></a>Painel Distribuição de Valor Detalhado  
 **Valor**  
 Exibe os valores distintos encontrados na coluna cujo perfil está sendo criado.  
  
 **Count**  
 Exibe o número de linhas nas quais a coluna cujo perfil está sendo criado tem o valor exibido na coluna **Valor** .  
  
 **Porcentagem**  
 Exibe o percentual de linhas nas quais a coluna cujo perfil está sendo criado tem o valor exibido na coluna **Valor** .  
  
### <a name="profile-type--candidate-key-profile"></a>Tipo de Perfil = Perfil-Chave de Candidato  
  
#### <a name="candidate-key-profile---table-pane"></a>Perfil-chave de candidato- \<table> painel  
 **Colunas de Chave**  
 Exibe as colunas que foram selecionadas para criação de perfil como chave candidata.  
  
 **Intensidade de Chave**  
 Exibe a intensidade (em porcentagem) da coluna da chave candidata ou da combinação de colunas. Uma intensidade de chave inferior a 100% indica que existem valores em duplicata.  
  
#### <a name="key-violations-pane"></a>Painel Violações de Chave  
 **\<column1>, \<column2> , etc.**  
 Exibe os valores em duplicata encontrados na coluna cujo perfil está sendo criado.  
  
 **Count**  
 Exibe o número de linhas nas quais a coluna especificada tem o valor exibido na primeira coluna.  
  
### <a name="profile-type--functional-dependency-profile"></a>Tipo de Perfil = Perfil de Dependência Funcional  
  
#### <a name="functional-dependency-profile-pane"></a>Painel do perfil de Dependência Funcional  
 **Colunas Determinantes**  
 Exibe a coluna ou colunas selecionadas como coluna ou colunas determinantes. No exemplo no qual o mesmo Código Postal dos Estados Unidos deveria ter sempre o mesmo estado, a coluna Código Postal é a coluna determinante.  
  
 **Colunas Dependentes**  
 Exibe a coluna ou colunas selecionadas como coluna ou colunas dependentes. No exemplo no qual o mesmo Código Postal dos Estados Unidos deveria ter sempre o mesmo estado, a coluna Estado é a coluna dependente.  
  
 **Intensidade de Dependência Funcional**  
 Exibe a intensidade (em porcentagem) da dependência funcional entre colunas. Uma intensidade de chave inferior a 100% indica que há casos nos quais o valor determinante não determina o valor dependente. No exemplo no qual o mesmo Código Postal dos Estados Unidos deveria ter sempre o mesmo estado, isso provavelmente indica que alguns valores de estado são inválidos  
  
#### <a name="functional-dependency-violations-pane"></a>Painel Violações de Dependência Funcional  
  
> [!NOTE]  
>  Uma porcentagem alta de valores errôneos nos dados poderia conduzir a resultados inesperados de um perfil Dependência Funcional. Por exemplo, 90% das linhas têm um valor de “WI” em Estado para um valor de Código Postal de "98052". O perfil informa linhas que contêm o valor de estado correto de "WA" como violações.  
  
 **\<determinant column name>**  
 Exibe o valor da coluna determinante ou combinação de colunas na instância de uma violação de dependência funcional.  
  
 **\<dependent column name>**  
 Exibe o valor da coluna dependente na instância de uma violação de dependência funcional.  
  
 **Contagem de Suporte**  
 Exibe o número de linhas nas quais o valor de coluna determinante determina a coluna dependente.  
  
 **Contagem de Violação**  
 Exibe o número de linhas nas quais o valor de coluna determinante não determina a coluna dependente (Essas são as linhas em que o valor dependente é o valor mostrado na **\<dependent column name>** coluna.)  
  
 **Percentual de Suporte**  
 Exibe a porcentagem de linhas nas quais a coluna determinante determina a coluna dependente.  
  
### <a name="profile-type--value-inclusion-profile"></a>Tipo de Perfil = Perfil de Inclusão de Valor  
  
#### <a name="value-inclusion-profile-pane"></a>Painel do Perfil de Inclusão de Valor  
 **Colunas Laterais de Subconjunto**  
 Exibe a coluna ou combinação de colunas cujo perfil foi criado para determinar se elas estão nas colunas do superconjunto.  
  
 **Colunas Laterais de Superconjunto**  
 Exibe a coluna ou combinação de colunas cujo perfil foi criado para determinar se elas incluem os valores nas colunas do subconjunto.  
  
 **Intensidade de Inclusão**  
 Exibe a intensidade (em porcentagem) da sobreposição entre colunas. Uma intensidade de chave inferior a 100% indica que há casos nos quais o valor do subconjunto não está localizado entre os valores do superconjunto.  
  
#### <a name="inclusion-violations-pane"></a>Painel Violações de Inclusão  
 **\<column1>, \<column2> , etc.**  
 Exibe os valores na coluna de subconjunto ou colunas que não foram localizadas na coluna ou colunas do superconjunto.  
  
 **Count**  
 Exibe o número de linhas nas quais a coluna especificada tem o valor exibido na primeira coluna.  
  
## <a name="see-also"></a>Consulte Também  
 [Visualizador de Perfil de Dados](control-flow/data-profile-viewer.md)   
 [Tarefa e visualizador da tarefa Criação de Perfil de Dados](control-flow/data-profiling-task-and-viewer.md)  
  
  
