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
ms.openlocfilehash: 899924b5c0847d5f42e383a9e04c33298bb368b9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68087751"
---
# <a name="unicode-data"></a>Dados Unicode
Os tipos de dados SQL Unicode são fornecidos para descrever os dados que residem em Unicode nativamente no DBMS. Um tipo de dados C Unicode é fornecido para permitir que um aplicativo vincule dados a um buffer Unicode. O Gerenciador de driver pode converter dados de um tipo C Unicode (SQL_C_WCHAR) para fazer com que ele funcione com um driver ANSI.  
  
 Um ODBC 3,0 ou 2. *x* o aplicativo sempre se associará aos tipos de dados ANSI. Para obter o desempenho ideal, um aplicativo ODBC 3,5 (ou superior) deve se associar ao tipo de dados C ANSI se o tipo de coluna SQL for ANSI e deve se associar ao tipo de dados C Unicode se o tipo de coluna SQL for Unicode.  
  
 Os indicadores de tipo Unicode do SQL são SQL_WCHAR, SQL_WVARCHAR e SQL_WLONGVARCHAR. SQL_WCHAR dados têm um comprimento de cadeia de caracteres fixo, enquanto SQL_WVARCHAR tem um comprimento variável com um máximo declarado e SQL_WLONGVARCHAR tem um comprimento variável com um máximo que depende da fonte de dados.  
  
 O indicador de tipo Unicode C é SQL_C_WCHAR. Esse é o padrão para cada um dos indicadores de tipo Unicode do SQL. Todos os tipos SQL podem ser convertidos em SQL_C_WCHAR e SQL_C_WCHAR podem ser convertidos em todos os tipos SQL. Um aplicativo pode recuperar dados de uma das três maneiras:  
  
-   Recupere os dados como SQL_C_CHAR.  
  
-   Recupere os dados como SQL_C_WCHAR.  
  
-   Declare os dados como SQL_C_TCHAR. Essa é uma macro que insere SQL_C_WCHAR se o aplicativo é compilado como um aplicativo Unicode ou insere SQL_C_CHAR se ele for compilado como um aplicativo ANSI.  
  
 SQL_C_TCHAR é declarado em uma função da seguinte maneira:  
  
```  
SQLBindParameter(StatementHandle, 1, SQL_PARAM_INPUT, SQL_C_TCHAR, SQL_WCHAR, NameLen, 0, Name, 0, &Name)  
```  
  
 Quando o aplicativo é compilado como um aplicativo Unicode, o argumento *ValueType* seria alterado de SQL_C_TCHAR para SQL_C_WCHAR. Quando o aplicativo é compilado como um aplicativo ANSI, o argumento *ValueType* seria alterado para SQL_C_CHAR.  
  
 Os drivers Unicode ainda devem oferecer suporte a tipos de dados ANSI, incluindo SQL_CHAR. Se um aplicativo que trabalha com um driver Unicode for associado a SQL_CHAR, o Gerenciador de driver não mapeará os dados de SQL_CHAR para SQL_WCHAR. O driver Unicode deve aceitar os dados de SQL_CHAR.  
  
 O Gerenciador de driver armazena nomes de driver e DSN em Unicode e os mapeia para ANSI, conforme necessário. Se um caractere Unicode não puder ser mapeado para um caractere ANSI (como pode ocorrer se os caracteres de uma página de código que não seja a página de código nativa do computador forem usados em nomes de drivers e DSN), os caracteres que não puderam ser convertidos serão representados por um sup de caracteres padrão plied pelo sistema.
