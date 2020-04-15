---
title: SQLTables (Driver Paradoxo) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: aa13b5395d8f3c2cb470a4eff1b1ef02a43bad53
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299277"
---
# <a name="sqltables-paradox-driver"></a>SQLTables (Driver do Paradox)
> [!NOTE]  
>  Este tópico fornece informações específicas do Paradox Driver. Para obter informações gerais sobre esta função, consulte o tópico apropriado em [Referência à API oDBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|Argumento|Comentários|  
|--------------|--------------|  
|*szTableOwner*|O único argumento válido para *szTableOwner* é NULL porque nenhum dos drivers suporta nomes de proprietários. Com *szTableOwner* definido como NULL, todas as tabelas são devolvidas. NULL é devolvido na coluna TABLE_OWNER.|  
|*szTableQualifier*|Na coluna TABLE_QUALIFIER, o **SQLTables** retornará o caminho para um diretório.|  
|*SzTableType*|Para arquivos Paradox, "TABLE" é o único tipo de tabela suportado.|  
  
## <a name="see-also"></a>Consulte Também  
 [Função SQLTables](../../odbc/reference/syntax/sqltables-function.md)
