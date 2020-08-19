---
description: SQLStatistics (Driver do dBASE)
title: SQLStatistics (driver do dBASE) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLStatistics function [ODBC], dBASE Driver
- DBase driver [ODBC], SQLStatistics
ms.assetid: 631cec1b-66b7-4103-b9a7-ffd81da3c442
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9285f78bbafb7594e3a9cbab2845cedeff0c1af9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421560"
---
# <a name="sqlstatistics-dbase-driver"></a>SQLStatistics (Driver do dBASE)
> [!NOTE]  
>  Este tópico fornece informações específicas do driver do dBASE. Para obter informações gerais sobre essa função, consulte o tópico apropriado em [referência da API do ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|Coluna|Comentários|  
|------------|--------------|  
|TABLE_QUALIFIER|O caminho para um diretório.<br /><br /> Não há suporte para a correspondência de padrões no argumento *szTableQualifier* .|  
|TABLE_OWNER|NULL é retornado nesta coluna porque não há suporte para o nome do proprietário.|  
|TABLE_NAME|Nome de tabela não delimitado.<br /><br /> Não há suporte para a correspondência de padrões no argumento *szTableName* .|  
|INDEX_QUALIFIER|NULL é sempre retornado.|  
|INDEX_NAME|Dependente de índice.|  
|TYPE|Somente SQL_TABLE_STAT ou SQL_INDEX_OTHER serão retornados para o tipo.|  
|SEQ_IN_INDEX|Dependente de índice.|  
|COLUMN_NAME|Dependente de índice.|  
|COLLATION|Dependente de índice.|  
|PAGES|NULL é sempre retornado.|  
  
 A filtragem se baseia na exclusividade (o argumento *fUnique* ). O parâmetro *fAccuracy* é ignorado.
