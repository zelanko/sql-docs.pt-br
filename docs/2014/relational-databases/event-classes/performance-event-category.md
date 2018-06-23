---
title: Categoria de evento de desempenho | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
topic_type:
- apiref
helpviewer_keywords:
- SQL Server event classes, Performance event category
- Performance event category [SQL Server]
- event classes [SQL Server], Performance event category
ms.assetid: 708f3585-d8be-4980-bbff-672d7c59397e
caps.latest.revision: 31
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 35b8a30db1271f393b9252ed4088a4d628cd4f1e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36011768"
---
# <a name="performance-event-category"></a>Categoria de evento de desempenho
  Use a categoria de evento **Performance** para monitorar as classes de evento **Showplan** e as que são produzidas pela execução dos operadores DML (linguagem de manipulação de dados) do SQL.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Description|  
|-----------|-----------------|  
|[Classe de evento Auto Stats](auto-stats-event-class.md)|Indica que houve uma atualização automática de índice e estatísticas de coluna.|  
|[Classe de evento Grau de Paralelismo &#40;7.0 Insert&#41;](degree-of-parallelism-7-0-insert-event-class.md)|Indica que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executou uma instrução  SELECT, INSERT, UPDATE ou DELETE usando um plano consecutivo ou paralelo. O número de CPUs usado para executar a operação também é informado.|  
|[Classe de evento Performance Statistics](performance-statistics-event-class.md)|Monitora o desempenho das consultas que estão sendo executadas.|  
|[Classe de evento Showplan All](showplan-all-event-class.md)|Identifica os operadores de **Plano de execução** em uma instrução SQL.|  
|[Classe de evento Showplan All for Query Compile](showplan-all-for-query-compile-event-class.md)|Exibe dados de tempo de compilação para operadores de **Plano de execução** .|  
|[Classe de Evento Showplan Statistics Profile](showplan-statistics-profile-event-class.md)|Exibe o custo calculado de uma consulta.|  
|[Classe de evento Showplan XML](showplan-xml-event-class.md)|Identifica os operadores de **Plano de execução** em uma instrução SQL. A classe de evento armazena cada evento como um documento de XML bem definido.|  
|[Classe de evento Showplan XML for Query Compile](showplan-xml-for-query-compile-event-class.md)|Exibe dados de tempo de compilação para operadores de **Plano de execução** em formato de XML.|  
|[Classe de evento Showplan XML Statistics Profile](showplan-xml-statistics-profile-event-class.md)|Identifica os operadores de **Plano de execução** associados com uma instrução SQL. A saída é um documento de XML.|  
|[Classe de evento SQL:FullTextQuery](sql-fulltextquery-event-class.md)|Indica que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executou uma consulta de texto completo.|  
|[Classe de evento Plan Guide Successful](plan-guide-successful-event-class.md)|Indica que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] produziu com sucesso um plano de execução para uma consulta ou lote, que continha uma guia de plano.|  
|[Classe de evento Plan Guide Unsuccessful](plan-guide-unsuccessful-event-class.md)|Indica que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pôde produzir um plano de execução, para uma consulta ou lote, que continha uma guia de plano.|  
  
## <a name="see-also"></a>Consulte também  
 [Eventos estendidos](../extended-events/extended-events.md)  
  
  