---
title: SQLTables (Driver do Paradox) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Paradox driver [ODBC], SQLTables
- SQLTables function [ODBC], Paradox Driver
ms.assetid: d68adad6-97bd-4b47-bcf9-0102aafb00d4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c845bd2e5e3ec5e52cfd6d1c0891f8825af1e148
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62735186"
---
# <a name="sqltables-paradox-driver"></a>SQLTables (Driver do Paradox)
> [!NOTE]  
>  Este tópico fornece informações específicas de Driver do Paradox. Para obter informações gerais sobre essa função, consulte o tópico apropriado sob [referência da API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|Argumento|Comentários|  
|--------------|--------------|  
|*szTableOwner*|O argumento só é válido para *szTableOwner* é NULL porque nenhum dos drivers dá suporte a nomes de proprietário. Com o *szTableOwner* definido como NULL, todas as tabelas são retornadas. NULL é retornado na coluna TABLE_OWNER.|  
|*szTableQualifier*|Na coluna TABLE_QUALIFIER **SQLTables** retornará o caminho para um diretório.|  
|*SzTableType*|Para arquivos do Paradox, "Tabela" é o único tipo de tabela com suporte.|  
  
## <a name="see-also"></a>Consulte também  
 [Função SQLTables](../../odbc/reference/syntax/sqltables-function.md)
