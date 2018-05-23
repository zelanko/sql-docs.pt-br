---
title: MSSQLSERVER_2508 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 2508 (Database Engine error)
ms.assetid: c37d40e5-c665-4d66-a727-5cb845634fcc
caps.latest.revision: 12
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 37a5f8976dabed380173dc56bb99edd07daec4df
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2018
---
# <a name="mssqlserver2508"></a>MSSQLSERVER_2508
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
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
  
