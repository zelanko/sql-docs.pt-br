---
title: SQLTables (driver do Excel) | Microsoft Docs
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
ms.openlocfilehash: 89157178aa9c134bdb1b9518343007adb1e1e05f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68132420"
---
# <a name="sqltables-excel-driver"></a>SQLTables (Driver do Excel)
> [!NOTE]  
>  Este tópico fornece informações específicas do driver do Excel. Para obter informações gerais sobre essa função, consulte o tópico apropriado em [referência da API do ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|Argumento|Comentários|  
|--------------|--------------|  
|*szTableOwner*|O único argumento válido para *szTableOwner* é nulo porque nenhum dos drivers dá suporte a nomes de proprietários. Com *szTableOwner* definido como NULL, todas as tabelas são retornadas. NULL é retornado na coluna TABLE_OWNER.|  
|*szTableQualifier*|Quando o driver do Microsoft Excel 3,0 ou 4,0 for usado, se você chamar **SQLTables** com um valor para *szTableQualifier* que não seja o nome de uma tabela existente, o driver criará uma tabela com esse nome.<br /><br /> Na coluna TABLE_QUALIFIER, **SQLTables** retornará o caminho para um diretório.|  
|*SzTableType*|Para o Microsoft Excel 3,0 ou 4,0, "TABLE" é o único tipo de tabela com suporte.<br /><br /> Para versões posteriores de arquivos do Microsoft Excel, "tabela do sistema" é retornada para nomes de planilhas (tabelas com um "$" no final) e "tabela" é retornada para tabelas em planilhas.|
