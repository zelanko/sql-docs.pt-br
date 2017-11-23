---
title: Testar um modelo no modo DirectQuery | Microsoft Docs
ms.custom: 
ms.date: 07/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 11260792-ff8b-4d0e-b845-ca210dd3fced
caps.latest.revision: "11"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: d6f55de10089d304fe5dc5d00c388d007a2241a6
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="test-a-model-in-directquery-mode"></a>Testar um modelo no modo DirectQuery

[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  Examine as opções para testar um modelo de tabela no DirectQuery em cada estágio do desenvolvimento, começando pelo design.  
  
## <a name="test-in-excel"></a>Testar no Excel 
  
 Ao criar seu modelo no SSDT, você pode usar o recurso **Analisar no Excel** para testar suas decisões de modelagem em um conjunto de dados na memória de exemplo ou no banco de dados relacional.  Quando você clica em Analisar no Excel, é aberta uma caixa de diálogo em que você pode especificar as opções.
 
 ![Opções do DirectQuery em Analisar no Excel](../../analysis-services/tabular-models/media/analyze-in-excel-directquery-options.png)
 
 Se o modo DirectQuery do modelo estiver ativado, você poderá especificar o modo de conexão DirectQuery, em que você terá duas opções:
 - **Exibição de dados de exemplo** – Com essa opção, todas as consultas do Excel são direcionadas para as partições de exemplo que contém um conjunto de dados na memória de exemplo. Essa opção é útil quando você quer ter certeza de que todas as fórmulas DAX que você têm em medidas, em colunas calculadas ou na segurança em nível de linha são executadas corretamente.
 
 - **Exibição de dados completa** – Com essa opção, todas as consultas do Excel são enviadas ao Analysis Services e, em seguida, ao banco de dados relacional. De fato, essa opção tem pleno funcionamento no modo DirecQuery.
 
 ### <a name="other-clients"></a>Outros clientes
 Quando você usa o recurso Analisar no Excel, um arquivo de conexão .odc é criado. Você pode usar as informações de cadeia de conexão deste arquivo para se conectar ao seu modelo por meio de outros aplicativos cliente. Um parâmetro adicional, DataView=Sample, é adicionado para especificar se o cliente deve se conectar às partições de dados de exemplo.  
  
## <a name="monitor-query-execution-on-backend-systems-using-xevents-or-sql-profiler"></a>Monitorar a execução da consulta em sistemas de back-end usando o xEvents ou o SQL Profiler 
 Inicie um rastreamento de sessão, conectado ao banco de dados relacional do SQL Server para monitorar as conexões do modelo Tabular:  
  
-   [Monitorar o Analysis Services com Eventos Estendidos do SQL Server](../../analysis-services/instances/monitor-analysis-services-with-sql-server-extended-events.md)  
  
-   [Usar o SQL Server Profiler para monitorar o Analysis Services](../../analysis-services/instances/use-sql-server-profiler-to-monitor-analysis-services.md)  
  
 Se você estiver usando o Oracle ou o Teradata, use as ferramentas de monitoramento de rastreamento para esses sistemas.  
  
  
