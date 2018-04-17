---
title: SQLTables (Driver do Excel) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Excel driver [ODBC], SQLTables
- SQLTables function [ODBC], Excel Driver
ms.assetid: 9410b686-4b5b-4b51-b5ef-f9d2e7a48faa
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9f7dbfc5174b832b5878096868bc2498105ae212
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="sqltables-excel-driver"></a>SQLTables (Driver do Excel)
> [!NOTE]  
>  Este tópico fornece informações específicas de Driver do Excel. Para obter informações gerais sobre esta função, consulte o tópico apropriado em [referência da API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|Argumento|Comentários|  
|--------------|--------------|  
|*szTableOwner*|O argumento só é válido para *szTableOwner* é NULL porque nenhum dos drivers de suporte a nomes de proprietário. Com *szTableOwner* definido como NULL, todas as tabelas são retornadas. NULL é retornado na coluna TABLE_OWNER.|  
|*szTableQualifier*|Quando o Microsoft Excel 3.0 ou 4.0 do driver é usado, se você chamar **SQLTables** com um valor para *szTableQualifier* que não é o nome de uma tabela existente, o driver criará uma tabela com esse nome.<br /><br /> Na coluna TABLE_QUALIFIER, **SQLTables** retornará o caminho para um diretório.|  
|*SzTableType*|Para o Microsoft Excel 3.0 ou 4.0, "TABLE" é o único tipo de tabela com suporte.<br /><br /> Para versões mais recentes de arquivos do Microsoft Excel, "Tabela de sistema" é retornada para os nomes de planilha (tabelas com "$" no final) e "TABLE" é retornado para as tabelas em planilhas.|
