---
title: SQLColAttributes (dBASE Driver) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLColAttribute function [ODBC], dBASE Driver
- DBase driver [ODBC], SQLColAttributes
ms.assetid: ed44de2b-0b01-4dce-a340-f5eb3aac30b7
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f294e40f71c30115b6bbaa54845aa5a72fe8eb76
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlcolattributes-dbase-driver"></a>SQLColAttributes (dBASE Driver)
> [!NOTE]  
>  Este tópico fornece informações de dBASE específica do Driver. Para obter informações gerais sobre esta função, consulte o tópico apropriado em [referência da API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|Atributo|Comentários|  
|---------------|--------------|  
|SQL_COLUMN_DISPLAY_SIZE|Para dados LONGVARBINARY SQL_COLUMN_DISPLAY_SIZE é o comprimento máximo da coluna, não o comprimento máximo da coluna vezes 2.|  
|SQL_OWNER_NAME|Uma cadeia de caracteres vazia ("") será retornado nessa coluna porque não há suporte para o nome do proprietário.|  
|SQL_QUALIFIER_NAME|O caminho para um diretório é retornado.|  
|SQL_COLUMN_SEARCHABLE|Colunas LONGVARBINARY e LONGVARCHAR são relatadas como SQL_UNSEARCHABLE.<br /><br /> Tipos de dados de caractere e binário de comprimento fixo e comprimento variável são pesquisáveis, embora LONGVARBINARY e LONGVARCHAR não são.|  
  
> [!NOTE]  
>  As opções acima não é uma lista completa de atributos retornados pelo **SQLColAttributes**.
