---
title: Categoria de evento de desempenho | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Server event classes, Performance event category
- Performance event category [SQL Server]
- event classes [SQL Server], Performance event category
ms.assetid: 708f3585-d8be-4980-bbff-672d7c59397e
caps.latest.revision: 32
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 094a75fe440ae2999d1a234c6e4d4dbaf1fd07d5
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39539596"
---
# <a name="performance-event-category"></a>Categoria de evento de desempenho
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Use a categoria de evento **Performance** para monitorar as classes de evento **Showplan** e as que são produzidas pela execução dos operadores DML (linguagem de manipulação de dados) do SQL.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Descrição|  
|-----------|-----------------|  
|[Classe de evento Auto Stats](../../relational-databases/event-classes/auto-stats-event-class.md)|Indica que houve uma atualização automática de índice e estatísticas de coluna.|  
|[Classe de evento Grau de Paralelismo &#40;7.0 Insert&#41;](../../relational-databases/event-classes/degree-of-parallelism-7-0-insert-event-class.md)|Indica que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executou uma instrução  SELECT, INSERT, UPDATE ou DELETE usando um plano consecutivo ou paralelo. O número de CPUs usado para executar a operação também é informado.|  
|[Classe de evento Performance Statistics](../../relational-databases/event-classes/performance-statistics-event-class.md)|Monitora o desempenho das consultas que estão sendo executadas.|  
|[Classe de evento Showplan All](../../relational-databases/event-classes/showplan-all-event-class.md)|Identifica os operadores de **Plano de execução** em uma instrução SQL.|  
|[Classe de evento Showplan All for Query Compile](../../relational-databases/event-classes/showplan-all-for-query-compile-event-class.md)|Exibe dados de tempo de compilação para operadores de **Plano de execução** .|  
|[Classe de Evento Showplan Statistics Profile](../../relational-databases/event-classes/showplan-statistics-profile-event-class.md)|Exibe o custo calculado de uma consulta.|  
|[Classe de evento Showplan XML](../../relational-databases/event-classes/showplan-xml-event-class.md)|Identifica os operadores de **Plano de execução** em uma instrução SQL. A classe de evento armazena cada evento como um documento de XML bem definido.|  
|[Classe de evento Showplan XML for Query Compile](../../relational-databases/event-classes/showplan-xml-for-query-compile-event-class.md)|Exibe dados de tempo de compilação para operadores de **Plano de execução** em formato de XML.|  
|[Classe de evento Showplan XML Statistics Profile](../../relational-databases/event-classes/showplan-xml-statistics-profile-event-class.md)|Identifica os operadores de **Plano de execução** associados com uma instrução SQL. A saída é um documento de XML.|  
|[Classe de evento SQL:FullTextQuery](../../relational-databases/event-classes/sql-fulltextquery-event-class.md)|Indica que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executou uma consulta de texto completo.|  
|[Classe de evento Plan Guide Successful](../../relational-databases/event-classes/plan-guide-successful-event-class.md)|Indica que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] produziu com sucesso um plano de execução para uma consulta ou lote, que continha uma guia de plano.|  
|[Classe de evento Plan Guide Unsuccessful](../../relational-databases/event-classes/plan-guide-unsuccessful-event-class.md)|Indica que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pôde produzir um plano de execução, para uma consulta ou lote, que continha uma guia de plano.|  
  
## <a name="see-also"></a>Consulte Também  
 [Eventos estendidos](../../relational-databases/extended-events/extended-events.md)  
  
  
