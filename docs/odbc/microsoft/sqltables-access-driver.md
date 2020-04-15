---
title: SQLTables (Driver de acesso) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLTables function [ODBC], Access Driver
- Access driver [ODBC], SQLTables
ms.assetid: 94423cf9-341a-4db6-bb10-8f5448df7fc3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: df3a23af365efbef6a0f0da2c52568501425ecb3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306087"
---
# <a name="sqltables-access-driver"></a>SQLTables (Driver do Access)
> [!NOTE]  
>  Este tópico fornece informações específicas do Access Driver. Para obter informações gerais sobre esta função, consulte o tópico apropriado em [Referência à API oDBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|Argumento|Comentários|  
|--------------|--------------|  
|*szTableOwner*|O único argumento válido para *szTableOwner* é NULL porque nenhum dos drivers suporta nomes de proprietários. Com *szTableOwner* definido como NULL, todas as tabelas são devolvidas. NULL é devolvido na coluna TABLE_OWNER.|  
|*szTableQualifier*|Na coluna TABLE_QUALIFIER, o **SQLTables** retornará o caminho para um arquivo de banco de dados.|  
|*SzTableType*|Quando o driver Microsoft Access é usado, "SYSTEM TABLE" é suportado para *szTableType* para tabelas do sistema, "SYNONYM" é suportado para tabelas anexadas e "VIEW" é suportado para consultas de retorno de linha.|  
  
## <a name="see-also"></a>Consulte Também  
 [Função SQLTables](../../odbc/reference/syntax/sqltables-function.md)
