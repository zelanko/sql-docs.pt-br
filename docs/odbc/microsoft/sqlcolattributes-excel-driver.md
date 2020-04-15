---
title: SQLColAttributes (Driver Excel) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Excel driver [ODBC], SQLColAttributes
- SQLColAttribute function [ODBC], Excel Driver
ms.assetid: 7c4833e3-ff0c-4313-9ab8-21379ceab656
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 218c442af6292b665764ed60dc5586710d820de6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307937"
---
# <a name="sqlcolattributes-excel-driver"></a>SQLColAttributes (Driver do Excel)
> [!NOTE]  
>  Este tópico fornece informações específicas do Excel Driver. Para obter informações gerais sobre esta função, consulte o tópico apropriado em [Referência à API oDBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|Atributo|Comentários|  
|---------------|--------------|  
|SQL_COLUMN_DISPLAY_SIZE|Para dados LONGVARBINARY, SQL_COLUMN_DISPLAY_SIZE é o comprimento máximo da coluna, não o comprimento máximo da coluna vezes 2.|  
|SQL_OWNER_NAME|Uma seqüência de string vazia ("") é devolvida nesta coluna porque o nome do proprietário não é suportado.|  
|SQL_QUALIFIER_NAME|O caminho para um diretório é devolvido.|  
|SQL_COLUMN_SEARCHABLE|As colunas LONGVARBINARY e LONGVARCHAR são relatadas como SQL_UNSEARCHABLE.<br /><br /> Os tipos de dados binários e de caracteres de comprimento fixo e de comprimento variável são pesquisáveis, embora LONGVARBINARY e LONGVARCHAR não sejam.|  
  
> [!NOTE]  
>  O acima não é uma lista completa dos atributos retornados por **SQLColAttributes**.
