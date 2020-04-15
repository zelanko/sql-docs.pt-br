---
title: SQLTables (dBASE Driver) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- DBase driver [ODBC], SQLTables
- SQLTables function [ODBC], dBASE Driver
ms.assetid: 45938efb-b678-47d8-9345-644fa26ad679
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 242be06eafc7657f37f55ce266af471cbc72597f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306067"
---
# <a name="sqltables-dbase-driver"></a>SQLTables (Driver do dBASE)
> [!NOTE]  
>  Este tópico fornece informações específicas do dBASE Driver. Para obter informações gerais sobre esta função, consulte o tópico apropriado em [Referência à API oDBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|Argumento|Comentários|  
|--------------|--------------|  
|*szTableOwner*|O único argumento válido para *szTableOwner* é NULL porque nenhum dos drivers suporta nomes de proprietários. Com *szTableOwner* definido como NULL, todas as tabelas são devolvidas. NULL é devolvido na coluna TABLE_OWNER.|  
|*szTableQualifier*|Na coluna TABLE_QUALIFIER, o **SQLTables** retornará o caminho para um diretório.|  
|*SzTableType*|Para arquivos dBASE, "TABLE" é o único tipo de tabela suportado.|
