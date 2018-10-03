---
title: Dados Unicode | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Unicode [ODBC], data
- data types [ODBC], Unicode
- C data types [ODBC], Unicode
- SQL data types [ODBC], Unicode
ms.assetid: abc28718-e6d9-49fb-97ff-402d50c3c375
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 74de6c44aaf109a434f0cf76c6902abfba92efe1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47655014"
---
# <a name="unicode-data"></a>Dados Unicode
Tipos de dados SQL Unicode são fornecidos para descrever dados que residem no Unicode nativamente no DBMS. Um tipo de dados Unicode de C é fornecido para permitir que um aplicativo associar dados a um buffer de Unicode. O Gerenciador de Driver pode converter dados de um tipo de C Unicode (SQL_C_WCHAR) para torná-lo funcionar com um driver de ANSI.  
  
 ODBC 3.0 ou 2. *x* aplicativo sempre se associará aos tipos de dados ANSI. Para um desempenho ideal, um aplicativo de ODBC 3.5 (ou superior) deve associar ao tipo de dados C ANSI, se o tipo de coluna SQL for ANSI e deve associar ao tipo de dados C Unicode se o tipo de coluna SQL for Unicode.  
  
 Os indicadores de tipo SQL Unicode são SQL_WCHAR, SQL_WVARCHAR e SQL_WLONGVARCHAR. Dados SQL_WCHAR tem um comprimento de cadeia de caracteres fixa, enquanto SQL_WVARCHAR tem um comprimento variável com um máximo declarado e SQL_WLONGVARCHAR tem um comprimento variável com um máximo que depende da fonte de dados.  
  
 O indicador de tipo C Unicode é SQL_C_WCHAR. Esse é o padrão para cada um dos indicadores de tipo SQL Unicode. Todos os tipos SQL podem ser convertidos em SQL_C_WCHAR, e SQL_C_WCHAR pode ser convertido em todos os tipos SQL. Um aplicativo pode recuperar dados em uma das três maneiras:  
  
-   Recupere os dados como SQL_C_CHAR.  
  
-   Recupere os dados como SQL_C_WCHAR.  
  
-   Declare os dados como SQL_C_TCHAR. Isso é uma macro que insere SQL_C_WCHAR se o aplicativo é compilado como um aplicativo Unicode ou insere SQL_C_CHAR se ele é compilado como um aplicativo ANSI.  
  
 SQL_C_TCHAR é declarado em uma função da seguinte maneira:  
  
```  
SQLBindParameter(StatementHandle, 1, SQL_PARAM_INPUT, SQL_C_TCHAR, SQL_WCHAR, NameLen, 0, Name, 0, &Name)  
```  
  
 Quando o aplicativo é compilado como um aplicativo Unicode, o *ValueType* argumento seria alterado de SQL_C_TCHAR para SQL_C_WCHAR. Quando o aplicativo é compilado como um aplicativo ANSI, o *ValueType* argumento seria alterado para SQL_C_CHAR.  
  
 Drivers Unicode ainda devem oferecer suporte a tipos de dados ANSI, incluindo SQL_CHAR. Se um aplicativo funcionando com um driver de Unicode se associar ao SQL_CHAR, o Gerenciador de Driver não mapeará os dados SQL_CHAR SQL_WCHAR. O driver de Unicode deve aceitar os dados SQL_CHAR.  
  
 O Gerenciador de Driver armazena o driver e nomes DSN em Unicode e mapeá-las para ANSI, conforme necessário. Se um caractere Unicode não pode ser mapeado para um caractere ANSI (como pode ocorrer se os caracteres de uma página de código que não é a página de código nativo do computador são usados em nomes DSN e driver), os caracteres que não puderam ser convertidos são representados por um sup de caractere padrão especializados pelo sistema.
