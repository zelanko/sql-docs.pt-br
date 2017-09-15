---
title: SQLGetTypeInfo (Driver de arquivo de texto) | Microsoft Docs
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
- SQLGetTypeInfo function [ODBC], Text File Driver
- text file driver [ODBC], SQLGetTypeInfo
ms.assetid: 05a58975-093c-4bd9-bd72-b5f0026a6e36
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: be45f11a17e340fb3a6999c242fce208ae733210
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="sqlgettypeinfo-text-file-driver"></a>SQLGetTypeInfo (Driver de arquivo de texto)
> [!NOTE]  
>  Este tópico fornece informações específicas de Driver do arquivo de texto. Para obter informações gerais sobre esta função, consulte o tópico apropriado em [referência da API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 O nome do tipo (TYPE_NAME) retornado na tabela produzida pela **SQLGetTypeInfo** será o nome mais comumente usado pela fonte de dados.  
  
 SQL_ALL_EXCEPT_LIKE será retornado na coluna PESQUISÁVEL por Byte, contador, Double, tipos de dados único, longa e curta. (O recurso LIKE pode ser obtido ao converter o valor para um caractere usando as funções de conversão canônica ODBC, em seguida, executar a comparação.)  
  
 Quando o driver de texto é usado, **SQLGetTypeInfo** retorna um valor CASE_SENSITIVE False para o texto de tipos de dados (CHAR e LONGCHAR), quando os tipos de dados, na verdade, diferenciam maiusculas de minúsculas.
