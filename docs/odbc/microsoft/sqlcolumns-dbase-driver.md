---
title: SQLColumns (driver do dBASE) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 242e4c2c95340aaf8bd4a8d8d41959b388a1cf70
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307887"
---
# <a name="sqlcolumns-dbase-driver"></a>SQLColumns (Driver do dBASE)
> [!NOTE]  
>  Este tópico fornece informações específicas do driver do dBASE. Para obter informações gerais sobre essa função, consulte o tópico apropriado em [referência da API do ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|Coluna|Comentários|  
|------------|--------------|  
|TABLE_QUALIFIER|O caminho para um diretório é retornado.|  
|TABLE_OWNER|NULL é retornado nesta coluna porque não há suporte para o nome do proprietário.|  
|NULLABLE|SQL_NO_NULLS é retornado para colunas que participam de uma chave primária ou índice exclusivo.|
