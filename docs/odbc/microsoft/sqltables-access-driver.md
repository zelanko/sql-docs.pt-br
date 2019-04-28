---
title: SQLTables (Access Driver) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9931d3d02ff2d0afe69f410d94474c16f235b94e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62686818"
---
# <a name="sqltables-access-driver"></a>SQLTables (Driver do Access)
> [!NOTE]  
>  Este tópico fornece informações específicas de Driver do Access. Para obter informações gerais sobre essa função, consulte o tópico apropriado sob [referência da API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|Argumento|Comentários|  
|--------------|--------------|  
|*szTableOwner*|O argumento só é válido para *szTableOwner* é NULL porque nenhum dos drivers dá suporte a nomes de proprietário. Com o *szTableOwner* definido como NULL, todas as tabelas são retornadas. NULL é retornado na coluna TABLE_OWNER.|  
|*szTableQualifier*|Na coluna TABLE_QUALIFIER **SQLTables** retornará o caminho para um arquivo de banco de dados.|  
|*SzTableType*|Quando o driver do Microsoft Access for usado, "Tabela de sistema" há suporte para *szTableType* para tabelas do sistema, "Sinônimo" há suporte para tabelas anexadas, e "VIEW" é suportado para retornar a linha consultas.|  
  
## <a name="see-also"></a>Consulte também  
 [Função SQLTables](../../odbc/reference/syntax/sqltables-function.md)
