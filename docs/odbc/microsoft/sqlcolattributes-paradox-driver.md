---
title: SQLColAttributes (Driver Paradox) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLColAttribute function [ODBC], Paradox Driver
- Paradox driver [ODBC], SQLColAttributes
ms.assetid: bbeef024-d470-4d28-b61b-26997ef41007
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 414ad2afeb627b413ecfc3ee166f694813e2676a
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="sqlcolattributes-paradox-driver"></a>SQLColAttributes (Driver Paradox)
> [!NOTE]  
>  Este tópico fornece informações específicas de Driver Paradox. Para obter informações gerais sobre esta função, consulte o tópico apropriado em [referência da API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|Atributo|Comentários|  
|---------------|--------------|  
|SQL_COLUMN_DISPLAY_SIZE|Para dados LONGVARBINARY SQL_COLUMN_DISPLAY_SIZE é o comprimento máximo da coluna, não o comprimento máximo da coluna vezes 2.|  
|SQL_OWNER_NAME|Uma cadeia de caracteres vazia ("") será retornado nessa coluna porque não há suporte para o nome do proprietário.|  
|SQL_QUALIFIER_NAME|O caminho para um diretório é retornado.|  
|SQL_COLUMN_SEARCHABLE|Colunas LONGVARBINARY e LONGVARCHAR são relatadas como SQL_UNSEARCHABLE.<br /><br /> Tipos de dados de caractere e binário de comprimento fixo e comprimento variável são pesquisáveis, embora LONGVARBINARY e LONGVARCHAR não são.|  
  
> [!NOTE]  
>  As opções acima não é uma lista completa de atributos retornados pelo **SQLColAttributes**.
