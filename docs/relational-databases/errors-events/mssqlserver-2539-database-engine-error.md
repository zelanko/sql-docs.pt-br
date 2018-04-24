---
title: MSSQLSERVER_2539 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 2539 (Database Engine error)
ms.assetid: e638efcc-56f4-40f9-9740-17ef67b47d79
caps.latest.revision: 16
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 26c4dd19ac5e09e39e431d650390eb012ec192e8
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver2539"></a>MSSQLSERVER_2539
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|2539|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DBCC_ALLOCATION_SUMMARY_FOR_DATABASE|  
|Texto da mensagem|O número total de extensões = EXTENTS, páginas usadas = USED_PAGES, páginas reservadas = RESERVED_PAGES neste banco de dados.|  
  
## <a name="explanation"></a>Explicação  
Essas informações fazem parte da saída do comando DBCC CHECKALLOC. Elas são um resumo de extensões alocadas, páginas usadas e páginas reservadas para o banco de dados especificado.  
  
## <a name="user-action"></a>Ação do usuário  
Nenhum  
  
