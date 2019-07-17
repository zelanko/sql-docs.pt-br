---
title: SQLColumns (Driver do dBASE) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLColumns function [ODBC], dBASE Driver
- DBase driver [ODBC], SQLColumns
ms.assetid: 168171de-ab7d-4b5b-af7f-6e2106adfcce
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5afad2cc08910e036a571e3f32b144bc0b922dda
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68132598"
---
# <a name="sqlcolumns-dbase-driver"></a>SQLColumns (Driver do dBASE)
> [!NOTE]  
>  Este tópico fornece informações específicas do Driver do dBASE. Para obter informações gerais sobre essa função, consulte o tópico apropriado sob [referência da API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|coluna|Comentários|  
|------------|--------------|  
|TABLE_QUALIFIER|O caminho para um diretório é retornado.|  
|TABLE_OWNER|NULL será retornado nessa coluna porque não há suporte para o nome do proprietário.|  
|NULLABLE|SQL_NO_NULLS é retornado para colunas que participam em uma chave primária ou índice exclusivo.|
