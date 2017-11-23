---
title: SQLStatistics (Driver Paradox) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Paradox driver [ODBC], SQLStatistics
- SQLStatistics function [ODBC], Paradox Driver
ms.assetid: 886cab83-d599-4fbc-9c88-e8cb833aac4b
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 280fd298b66c751673594220d9826dd1c591511f
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="sqlstatistics-paradox-driver"></a>SQLStatistics (Driver Paradox)
> [!NOTE]  
>  Este tópico fornece informações específicas de Driver Paradox. Para obter informações gerais sobre esta função, consulte o tópico apropriado em [referência da API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|Coluna|Comentários|  
|------------|--------------|  
|TABLE_QUALIFIER|O caminho para um diretório.<br /><br /> Não há suporte para a correspondência de padrões no *szTableQualifier* argumento.|  
|TABLE_OWNER|NULL será retornado nessa coluna porque não há suporte para o nome do proprietário.|  
|TABLE_NAME|Nome da tabela não delimitado.<br /><br /> Não há suporte para a correspondência de padrões no *szTableName* argumento.|  
|INDEX_QUALIFIER|Sempre será retornado NULL.|  
|INDEX_NAME|Dependente de índice.|  
|TYPE|Somente SQL_TABLE_STAT ou SQL_INDEX_OTHER será retornado para o tipo.|  
|SEQ_IN_INDEX|Dependente de índice.|  
|COLUMN_NAME|Dependente de índice.|  
|COLLATION|Dependente de índice.|  
|PAGES|Sempre será retornado NULL.|  
  
 A filtragem se baseia a exclusividade (a *fUnique* argumento). O *fAccuracy* parâmetro é ignorado.
