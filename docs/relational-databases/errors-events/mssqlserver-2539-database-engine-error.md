---
title: MSSQLSERVER_2539 | Microsoft Docs
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
- 2539 (Database Engine error)
ms.assetid: e638efcc-56f4-40f9-9740-17ef67b47d79
caps.latest.revision: 16
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 89c01c5e8b2cb8948edd1e3a6092d0662c670b92
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

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
Nenhum.  
  

