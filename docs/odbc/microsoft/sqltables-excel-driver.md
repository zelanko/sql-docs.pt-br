---
title: SQLTables (Excel Driver) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Excel driver [ODBC], SQLTables
- SQLTables function [ODBC], Excel Driver
ms.assetid: 9410b686-4b5b-4b51-b5ef-f9d2e7a48faa
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 23ce67350b7fa7d0a88f3d51e618ce9bb9f9ebcf
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63287284"
---
# <a name="sqltables-excel-driver"></a>SQLTables (Driver do Excel)
> [!NOTE]  
>  Este tópico fornece informações específicas de Driver do Excel. Para obter informações gerais sobre essa função, consulte o tópico apropriado sob [referência da API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|Argumento|Comentários|  
|--------------|--------------|  
|*szTableOwner*|O argumento só é válido para *szTableOwner* é NULL porque nenhum dos drivers dá suporte a nomes de proprietário. Com o *szTableOwner* definido como NULL, todas as tabelas são retornadas. NULL é retornado na coluna TABLE_OWNER.|  
|*szTableQualifier*|Quando o Microsoft Excel 3.0 ou 4.0 do driver é usado, se você chamar **SQLTables** com um valor para *szTableQualifier* que não é o nome de uma tabela existente, o driver criará uma tabela com esse nome.<br /><br /> Na coluna TABLE_QUALIFIER **SQLTables** retornará o caminho para um diretório.|  
|*SzTableType*|Para o Microsoft Excel 3.0 ou 4.0, "Tabela" é o único tipo de tabela com suporte.<br /><br /> Para versões posteriores de arquivos do Microsoft Excel, "Tabela de sistema" é retornada para os nomes de planilha (tabelas com "$" no final) e "TABLE" é retornado para tabelas em planilhas.|
