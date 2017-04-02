---
title: "Consultar os par&#226;metros usados para criar um modelo de minera&#231;&#227;o | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "consultas a conteúdo [DMX]"
ms.assetid: ce7719e0-6127-4d9c-a753-0e0a3db065e1
caps.latest.revision: 13
author: "Minewiskan"
ms.author: "owend"
manager: "jhubbard"
caps.handback.revision: 13
---
# Consultar os par&#226;metros usados para criar um modelo de minera&#231;&#227;o
  A composição de um modelo de mineração é afetada não apenas pelos casos de treinamento, mas também pelos parâmetros que foram definidos quando o modelo foi criado. Portanto, talvez seja útil recuperar as configurações de parâmetro de um modelo existente para compreender melhor o comportamento do modelo. A recuperação de parâmetros também é útil na documentação de uma versão específica desse modelo.  
  
 Para localizar parâmetros que foram usados quando o modelo foi criado, você cria uma consulta em um dos conjuntos de linhas do esquema do modelo de mineração. No [!INCLUDE[ssASCurrent](../../includes/ssascurrent-md.md)], esses conjuntos de linhas de esquema são expostos como um conjunto de exibições do sistema que pode ser consultado facilmente com a sintaxe Transact-SQL. Este procedimento descreve como criar uma consulta que retorna os parâmetros usados para criar o modelo de mineração especificado.  
  
### Para abrir uma janela Consulta para uma consulta de conjunto de linhas de esquema  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], abra a instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que contém o modelo que deseja consultar.  
  
2.  Clique com o botão direito do mouse no nome da instância, selecione **Nova Consulta** e selecione **DMX**.  
  
    > [!NOTE]  
    >  Você também pode criar uma consulta para um modelo de mineração de dados usando o modelo **MDX**.  
  
3.  Se a instância tiver vários bancos de dados, selecione o banco de dados que contém o modelo que deseja consultar na lista **Banco de Dados Disponíveis** da barra de ferramentas.  
  
### Para retornar parâmetros de modelo para um modelo de mineração existente  
  
1.  No painel de consulta DMX, digite ou cole o seguinte texto:  
  
    ```  
    SELECT MINING_PARAMETERS  
    FROM $system.DMSCHEMA_MINING_MODELS  
    WHERE MODEL_NAME = ''  
    ```  
  
2.  No Pesquisador de Objetos, selecione o modelo de mineração desejado e arraste-o no painel de consulta DMX, entre as aspas simples.  
  
3.  Pressione F5 ou clique em **Executar**.  
  
## Exemplo  
 O código a seguir retorna uma lista dos parâmetros usados para criar o modelo de mineração que você criou no [Basic Data Mining Tutorial](../Topic/Basic%20Data%20Mining%20Tutorial.md). Esses parâmetros incluem os valores explícitos de todos os padrões usados pelos serviços de mineração disponíveis dos provedores no servidor.  
  
```  
SELECT MINING_PARAMETERS   
FROM $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'TM Clustering'  
```  
  
 O exemplo de código retorna os seguintes parâmetros para o modelo de clustering:  
  
 Resultados de eExample:  
  
 MINING_PARAMETERS  
  
 CLUSTER_COUNT=10,CLUSTER_SEED=0,CLUSTERING_METHOD=1,MAXIMUM_INPUT_ATTRIBUTES=255,MAXIMUM_STATES=100,MINIMUM_SUPPORT=1,MODELLING_CARDINALITY=10,SAMPLE_SIZE=50000,STOPPING_TOLERANCE=10  
  
## Consulte também  
 [Tarefas e instruções de consulta de mineração de dados](../../analysis-services/data-mining/data-mining-query-tasks-and-how-tos.md)   
 [Consultas de mineração de dados](../../analysis-services/data-mining/data-mining-queries.md)  
  
  