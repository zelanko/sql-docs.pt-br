---
title: SQLStatistics (driver de arquivo de texto) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- text file driver [ODBC], SQLStatistics
- SQLStatistics function [ODBC], Text File Driver
ms.assetid: 311afc01-d656-425f-be43-4a8e7cbc9a97
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4deede2060821ed05a58a637adcf09493fd910dc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68037825"
---
# <a name="sqlstatistics-text-file-driver"></a>SQLStatistics (Driver de Arquivo de texto)
> [!NOTE]  
>  Este tópico fornece informações específicas do driver de arquivo de texto. Para obter informações gerais sobre essa função, consulte o tópico apropriado em [referência da API do ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
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
