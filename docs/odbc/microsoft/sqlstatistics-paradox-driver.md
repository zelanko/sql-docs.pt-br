---
title: SQLStatistics (Driver do Paradox) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Paradox driver [ODBC], SQLStatistics
- SQLStatistics function [ODBC], Paradox Driver
ms.assetid: 886cab83-d599-4fbc-9c88-e8cb833aac4b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 634fbcdbf78515e59295e679072ffa5fd08e4823
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62686933"
---
# <a name="sqlstatistics-paradox-driver"></a>SQLStatistics (Driver do Paradox)
> [!NOTE]  
>  Este tópico fornece informações específicas de Driver do Paradox. Para obter informações gerais sobre essa função, consulte o tópico apropriado sob [referência da API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|coluna|Comentários|  
|------------|--------------|  
|TABLE_QUALIFIER|O caminho para um diretório.<br /><br /> Correspondência de padrões não é compatível com o *szTableQualifier* argumento.|  
|TABLE_OWNER|NULL será retornado nessa coluna porque não há suporte para o nome do proprietário.|  
|TABLE_NAME|Nome da tabela não delimitado.<br /><br /> Correspondência de padrões não é compatível com o *szTableName* argumento.|  
|INDEX_QUALIFIER|Sempre será retornado NULL.|  
|INDEX_NAME|Índice dependente.|  
|TYPE|Somente SQL_TABLE_STAT ou SQL_INDEX_OTHER será retornado para o tipo.|  
|SEQ_IN_INDEX|Índice dependente.|  
|COLUMN_NAME|Índice dependente.|  
|COLLATION|Índice dependente.|  
|PAGES|Sempre será retornado NULL.|  
  
 Filtragem se baseia nos exclusividade (a *fUnique* argumento). O *fAccuracy* parâmetro será ignorado.
