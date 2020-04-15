---
title: SQLStatistics (Driver de acesso) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Access driver [ODBC], SQLStatistics
- SQLStatistics function [ODBC], Access Driver
ms.assetid: 6117ac77-1020-4f0c-8eed-e671c34c1f21
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f75f41bf63cbf224772955effa0f120b5d384111
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299356"
---
# <a name="sqlstatistics-access-driver"></a>SQLStatistics (Driver do Access)
> [!NOTE]  
>  Este tópico fornece informações específicas do Access Driver. Para obter informações gerais sobre esta função, consulte o tópico apropriado em [Referência à API oDBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|Coluna|Comentários|  
|------------|--------------|  
|TABLE_QUALIFIER|O caminho para um arquivo de banco de dados é devolvido para o Microsoft Access.<br /><br /> A correspondência de padrões não é suportada no argumento *szTableQualifier.*|  
|TABLE_OWNER|NULL é devolvido nesta coluna, porque o nome do proprietário não é suportado.|  
|TABLE_NAME|Nome de tabela não limitado.<br /><br /> A correspondência de padrões não é suportada no argumento *szTableName.*|  
|INDEX_QUALIFIER|NULL é sempre devolvido.|  
|INDEX_NAME|Dependente de índice.|  
|TYPE|Somente SQL_TABLE_STAT ou SQL_INDEX_OTHER serão devolvidos para TYPE.|  
|SEQ_IN_INDEX|Dependente de índice.|  
|COLUMN_NAME|Dependente de índice.|  
|COLLATION|Dependente de índice.|  
|CARDINALITY|Devolvido apenas para o Microsoft Access.|  
|PAGES|NULL é sempre devolvido.|  
  
 A filtragem é baseada na exclusividade (o argumento *fUnique).* O parâmetro *fAccuracy* é ignorado.
