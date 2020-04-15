---
title: SQLTables (Driver Excel) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c436a1f52a862cda753d8c043515f5584607d98c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299296"
---
# <a name="sqltables-excel-driver"></a>SQLTables (Driver do Excel)
> [!NOTE]  
>  Este tópico fornece informações específicas do Excel Driver. Para obter informações gerais sobre esta função, consulte o tópico apropriado em [Referência à API oDBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|Argumento|Comentários|  
|--------------|--------------|  
|*szTableOwner*|O único argumento válido para *szTableOwner* é NULL porque nenhum dos drivers suporta nomes de proprietários. Com *szTableOwner* definido como NULL, todas as tabelas são devolvidas. NULL é devolvido na coluna TABLE_OWNER.|  
|*szTableQualifier*|Quando o driver Microsoft Excel 3.0 ou 4.0 é usado, se você chamar **SQLTables** com um valor para *szTableQualifier* que não é o nome de uma tabela existente, o driver criará uma tabela com esse nome.<br /><br /> Na coluna TABLE_QUALIFIER, o **SQLTables** retornará o caminho para um diretório.|  
|*SzTableType*|Para o Microsoft Excel 3.0 ou 4.0, "TABLE" é o único tipo de tabela suportado.<br /><br /> Para versões posteriores dos arquivos do Microsoft Excel, "SYSTEM TABLE" é devolvido para nomes de planilhas (tabelas com um "$" no final) e "TABLE" é devolvido para tabelas dentro de planilhas.|
