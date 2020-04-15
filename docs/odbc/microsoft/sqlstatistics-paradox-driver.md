---
title: SQLStatistics (Driver Paradoxo) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5e9782eb22e4176a57aab7bdd3823982575a0d55
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299316"
---
# <a name="sqlstatistics-paradox-driver"></a>SQLStatistics (Driver do Paradox)
> [!NOTE]  
>  Este tópico fornece informações específicas do Paradox Driver. Para obter informações gerais sobre esta função, consulte o tópico apropriado em [Referência à API oDBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|Coluna|Comentários|  
|------------|--------------|  
|TABLE_QUALIFIER|O caminho para um diretório.<br /><br /> A correspondência de padrões não é suportada no argumento *szTableQualifier.*|  
|TABLE_OWNER|NULL é devolvido nesta coluna porque o nome do proprietário não é suportado.|  
|TABLE_NAME|Nome de tabela não limitado.<br /><br /> A correspondência de padrões não é suportada no argumento *szTableName.*|  
|INDEX_QUALIFIER|NULL é sempre devolvido.|  
|INDEX_NAME|Dependente de índice.|  
|TYPE|Somente SQL_TABLE_STAT ou SQL_INDEX_OTHER serão devolvidos para TYPE.|  
|SEQ_IN_INDEX|Dependente de índice.|  
|COLUMN_NAME|Dependente de índice.|  
|COLLATION|Dependente de índice.|  
|PAGES|NULL é sempre devolvido.|  
  
 A filtragem é baseada na exclusividade (o argumento *fUnique).* O parâmetro *fAccuracy* é ignorado.
