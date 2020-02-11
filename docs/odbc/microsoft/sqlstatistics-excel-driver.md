---
title: SQLStatistics (driver do Excel) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Excel driver [ODBC], SQLStatistics
- SQLStatistics function [ODBC], Excel Driver
ms.assetid: 02506664-8dcc-4bd0-a8bb-d49fcbdd5722
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1c36d68f42b9b7f76310c453d704c6815ee6de22
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68132473"
---
# <a name="sqlstatistics-excel-driver"></a>SQLStatistics (Driver do Excel)
> [!NOTE]  
>  Este tópico fornece informações específicas do driver do Excel. Para obter informações gerais sobre essa função, consulte o tópico apropriado em [referência da API do ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
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
