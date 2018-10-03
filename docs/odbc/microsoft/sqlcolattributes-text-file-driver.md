---
title: SQLColAttributes (Driver de arquivo de texto) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- text file driver [ODBC], SQLColAttributes
- SQLColAttribute function [ODBC], Text File Driver
ms.assetid: 132fd1c0-1921-4a7d-910e-aedf1bff5453
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8bb242dcaf34f8fe7fad2886b13ddf5209c20c18
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47855054"
---
# <a name="sqlcolattributes-text-file-driver"></a>SQLColAttributes (Driver de Arquivo de texto)
> [!NOTE]  
>  Este tópico fornece informações específicas de Driver de arquivo de texto. Para obter informações gerais sobre essa função, consulte o tópico apropriado sob [referência da API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|attribute|Comentários|  
|---------------|--------------|  
|SQL_COLUMN_DISPLAY_SIZE|Para dados LONGVARBINARY SQL_COLUMN_DISPLAY_SIZE é o comprimento máximo da coluna, não o comprimento máximo da coluna vezes 2.|  
|SQL_OWNER_NAME|Uma cadeia de caracteres vazia ("") será retornado nessa coluna porque não há suporte para o nome do proprietário.|  
|SQL_QUALIFIER_NAME|O caminho para um diretório é retornado.|  
|SQL_COLUMN_SEARCHABLE|Colunas LONGVARBINARY e LONGVARCHAR são relatadas como SQL_UNSEARCHABLE.<br /><br /> Binário de comprimento fixo e comprimento variável e tipos de dados de caracteres são pesquisáveis, mesmo que LONGVARBINARY e LONGVARCHAR não são.|
