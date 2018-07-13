---
title: MSSQLSERVER_2508 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 2508 (Database Engine error)
ms.assetid: c37d40e5-c665-4d66-a727-5cb845634fcc
caps.latest.revision: 12
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ac343cb92828e16cb87bc6e6f979a73a2a4adf47
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37407395"
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
  
  
