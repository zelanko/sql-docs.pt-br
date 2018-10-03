---
title: SQLStatistics (Driver do dBASE) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9bac3e235197838442a2cdde24926b37ac90524c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47656108"
---
# <a name="sqlstatistics-dbase-driver"></a>SQLStatistics (Driver do dBASE)
> [!NOTE]  
>  Este tópico fornece informações específicas do Driver do dBASE. Para obter informações gerais sobre essa função, consulte o tópico apropriado sob [referência da API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
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
