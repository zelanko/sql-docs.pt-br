---
title: SqlGetTypeInfo (driver de arquivo de texto) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetTypeInfo function [ODBC], Text File Driver
- text file driver [ODBC], SQLGetTypeInfo
ms.assetid: 05a58975-093c-4bd9-bd72-b5f0026a6e36
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7b70b58e4760959db102450b5f8b7beed042df95
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81294996"
---
# <a name="sqlgettypeinfo-text-file-driver"></a>SQLGetTypeInfo (Driver de Arquivo de texto)
> [!NOTE]  
>  Este tópico fornece informações específicas do Driver de arquivo de texto. Para obter informações gerais sobre esta função, consulte o tópico apropriado em [Referência à API oDBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 O nome do tipo (TYPE_NAME) retornado na tabela produzida pelo **SQLGetTypeInfo** será o nome mais usado pela fonte de dados.  
  
 SQL_ALL_EXCEPT_LIKE serão devolvidos na coluna SEARCHABLE para os tipos de dados Byte, Counter, Double, Single, Long e Short. (A capacidade LIKE pode ser alcançada convertendo o valor em um caractere usando as funções de conversão canônica oDBC e, em seguida, realizando a comparação.)  
  
 Quando o driver de texto é usado, **o SQLGetTypeInfo** retorna um valor CASE_SENSITIVE de FALSE para os tipos de dados de texto (CHAR e LONGCHAR), quando os tipos de dados realmente são sensíveis a maiúsculas e minúsculas.
