---
title: MSSQLSERVER_2508 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 2508 (Database Engine error)
ms.assetid: c37d40e5-c665-4d66-a727-5cb845634fcc
caps.latest.revision: 12
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: b5e66405fcdc57a971c1d098d105345ce141978d
ms.contentlocale: pt-br
ms.lasthandoff: 04/11/2017

---
# <a name="mssqlserver2508"></a>MSSQLSERVER_2508
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|2508|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DBCC_OUT_OF_DATE_PAGE_OR_ROW_COUNT|  
|Texto da mensagem|A contagem %.*ls de objetos "%.\*ls", IDs de índice %d, IDs de partição %I64d e IDs de unidade de alocação %I64d (tipo %.\*ls) está incorreta. Execute DBCC UPDATEUSAGE.|  
  
## <a name="explanation"></a>Explicação  
Em versões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anteriores ao [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], os valores referentes às contagens de linha de tabela e de índice e as contagens de página podem se tornar incorretas. Os bancos de dados criados em versões anteriores ao [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] podem conter contagens incorretas. O comando DBCC CHECKDB foi aprimorado para detectar esses erros e retorna essa mensagem de aviso quando detecta o erro.  
  
## <a name="user-action"></a>Ação do usuário  
Execute DBCC UPDATEUSAGE no objeto ou índice especificado ou no banco de dados em que o objeto está contido para corrigir as contagens inválidas.  
  

