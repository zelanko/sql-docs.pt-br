---
title: MSSQLSERVER_2538 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 2538 (Database Engine error)
ms.assetid: 0a0f7d79-f1ba-4749-8804-fb660cca3492
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6b696097a4bfdec2e625de4523fc7689f230f6cc
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver2538"></a>MSSQLSERVER_2538
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|2538|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DBCC_ALLOCATION_SUMMARY_PER_FILE|  
|Texto da mensagem|Arquivo FILE: Número de extensões = EXTENTS, páginas usadas = USED_PAGES, páginas reservadas = RESERVED_PAGES.|  
  
## <a name="explanation"></a>Explicação  
Essas informações fazem parte da saída do comando DBCC CHECKALLOC. Elas são um resumo por arquivo de extensões alocadas, páginas usadas e páginas reservadas para o banco de dados especificado.  
  
## <a name="user-action"></a>Ação do usuário  
Nenhum.  
  
