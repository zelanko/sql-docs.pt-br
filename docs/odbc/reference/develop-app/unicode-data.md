---
title: Dados Unicode | Microsoft Docs
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
- Unicode [ODBC], data
- data types [ODBC], Unicode
- C data types [ODBC], Unicode
- SQL data types [ODBC], Unicode
ms.assetid: abc28718-e6d9-49fb-97ff-402d50c3c375
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ee404891b20f721cec0ea9e56b9eab1e78ad6f8f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32915811"
---
# <a name="unicode-data"></a>Dados Unicode
Tipos de dados SQL Unicode são fornecidos para descrever dados que residem em Unicode nativamente no DBMS. Um tipo de dados Unicode de C é fornecido para permitir que um aplicativo associar dados a um buffer de Unicode. O Gerenciador de Driver pode converter dados de um tipo de Unicode C (SQL_C_WCHAR) para torná-lo funcionar com um driver de ANSI.  
  
 ODBC 3.0 ou 2. *x* aplicativo sempre associará aos tipos de dados ANSI. Para um melhor desempenho, um aplicativo de ODBC 3.5 (ou superior) deve associar ao tipo de dados C ANSI se o tipo de coluna SQL for ANSI e deve ser associados ao tipo de dados Unicode C se o tipo de coluna SQL é Unicode.  
  
 Os indicadores de tipo SQL Unicode são SQL_WCHAR, SQL_WVARCHAR e SQL_WLONGVARCHAR. Dados SQL_WCHAR tem um comprimento de cadeia de caracteres fixa, enquanto SQL_WVARCHAR tem um comprimento variável com um máximo de declarados e SQL_WLONGVARCHAR tem um comprimento variável com um máximo que depende da fonte de dados.  
  
 O indicador de tipo C Unicode é SQL_C_WCHAR. Esse é o padrão para cada um dos indicadores de tipo SQL Unicode. Todos os tipos SQL podem ser convertidos em SQL_C_WCHAR, e SQL_C_WCHAR pode ser convertido em todos os tipos SQL. Um aplicativo pode recuperar dados de uma das três maneiras:  
  
-   Recupere os dados como SQL_C_CHAR.  
  
-   Recupere os dados como SQL_C_WCHAR.  
  
-   Declare os dados como SQL_C_TCHAR. Isso é uma macro que insere SQL_C_WCHAR se o aplicativo é compilado como um aplicativo Unicode ou insere SQL_C_CHAR se ele é compilado como um aplicativo de ANSI.  
  
 SQL_C_TCHAR é declarado em uma função, da seguinte maneira:  
  
```  
SQLBindParameter(StatementHandle, 1, SQL_PARAM_INPUT, SQL_C_TCHAR, SQL_WCHAR, NameLen, 0, Name, 0, &Name)  
```  
  
 Quando o aplicativo é compilado como um aplicativo de Unicode, o *ValueType* argumento seria alterado de SQL_C_TCHAR para SQL_C_WCHAR. Quando o aplicativo é compilado como um aplicativo de ANSI, o *ValueType* argumento seria alterado em SQL_C_CHAR.  
  
 Drivers de Unicode ainda devem dar suporte a tipos de dados ANSI, incluindo SQL_CHAR. Se um aplicativo trabalhando com um driver de Unicode associa a SQL_CHAR, o Gerenciador de Driver não mapeará os dados SQL_CHAR para SQL_WCHAR. O driver de Unicode deve aceitar os dados SQL_CHAR.  
  
 O Gerenciador de Driver armazena nomes DSN e o driver em Unicode e mapeá-las para ANSI, conforme necessário. Se um caractere Unicode não pode ser mapeado para um caractere ANSI (como pode ocorrer se os caracteres de uma página de código que não é a página de código nativo do computador são usados em nomes DSN e o driver), os caracteres que não puderam ser convertidos são representados por um sup de caractere padrão especializados pelo sistema.
