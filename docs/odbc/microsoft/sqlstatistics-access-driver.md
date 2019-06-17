---
title: SQLStatistics (Driver do Access) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bc5a354aeaf186b4baeabd96e7424939fe463bfb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62687126"
---
# <a name="sqlstatistics-access-driver"></a>SQLStatistics (Driver do Access)
> [!NOTE]  
>  Este tópico fornece informações específicas de Driver do Access. Para obter informações gerais sobre essa função, consulte o tópico apropriado sob [referência da API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|coluna|Comentários|  
|------------|--------------|  
|TABLE_QUALIFIER|O caminho para um arquivo de banco de dados é retornado para o Microsoft Access.<br /><br /> Correspondência de padrões não é compatível com o *szTableQualifier* argumento.|  
|TABLE_OWNER|NULL será retornado nessa coluna, porque não há suporte para o nome do proprietário.|  
|TABLE_NAME|Nome da tabela não delimitado.<br /><br /> Correspondência de padrões não é compatível com o *szTableName* argumento.|  
|INDEX_QUALIFIER|Sempre será retornado NULL.|  
|INDEX_NAME|Índice dependente.|  
|TYPE|Somente SQL_TABLE_STAT ou SQL_INDEX_OTHER será retornado para o tipo.|  
|SEQ_IN_INDEX|Índice dependente.|  
|COLUMN_NAME|Índice dependente.|  
|COLLATION|Índice dependente.|  
|CARDINALITY|Retornado somente para o Microsoft Access.|  
|PAGES|Sempre será retornado NULL.|  
  
 Filtragem se baseia nos exclusividade (a *fUnique* argumento). O *fAccuracy* parâmetro será ignorado.
