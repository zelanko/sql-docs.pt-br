---
title: SQLStatistics (Driver Paradox) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Paradox driver [ODBC], SQLStatistics
- SQLStatistics function [ODBC], Paradox Driver
ms.assetid: 886cab83-d599-4fbc-9c88-e8cb833aac4b
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 18e323ff059fdeb70fcadd256728de8050eea56a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32903281"
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
