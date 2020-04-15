---
title: SQLStatistics (dBASE Driver) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLStatistics function [ODBC], dBASE Driver
- DBase driver [ODBC], SQLStatistics
ms.assetid: 631cec1b-66b7-4103-b9a7-ffd81da3c442
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: deec1d7cff9ea1d0f8560b3c9b866cad79e69a25
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299346"
---
# <a name="sqlstatistics-dbase-driver"></a>SQLStatistics (Driver do dBASE)
> [!NOTE]  
>  Este tópico fornece informações específicas do dBASE Driver. Para obter informações gerais sobre esta função, consulte o tópico apropriado em [Referência à API oDBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
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
