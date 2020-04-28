---
title: SQLColAttributes (driver do dBASE) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLColAttribute function [ODBC], dBASE Driver
- DBase driver [ODBC], SQLColAttributes
ms.assetid: ed44de2b-0b01-4dce-a340-f5eb3aac30b7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a9e9d5adb75a99784d7244852bfda0499e481fc4
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307947"
---
# <a name="sqlcolattributes-dbase-driver"></a>SQLColAttributes (Driver do dBASE)
> [!NOTE]  
>  Este tópico fornece informações específicas do driver do dBASE. Para obter informações gerais sobre essa função, consulte o tópico apropriado em [referência da API do ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|Atributo|Comentários|  
|---------------|--------------|  
|SQL_COLUMN_DISPLAY_SIZE|Para dados LONGVARBINARY, SQL_COLUMN_DISPLAY_SIZE é o comprimento máximo da coluna, não o comprimento máximo da coluna vezes 2.|  
|SQL_OWNER_NAME|Uma cadeia de caracteres vazia ("") é retornada nesta coluna porque não há suporte para o nome do proprietário.|  
|SQL_QUALIFIER_NAME|O caminho para um diretório é retornado.|  
|SQL_COLUMN_SEARCHABLE|As colunas LONGVARBINARY e LONGVARCHAR são relatadas como SQL_UNSEARCHABLE.<br /><br /> Os tipos de dados Binary e Character de comprimento fixo e variável são pesquisáveis, mesmo que LONGVARBINARY e LONGVARCHAR não estejam.|  
  
> [!NOTE]  
>  O acima não é uma lista completa dos atributos retornados por **SQLColAttributes**.
