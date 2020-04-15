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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 73ea9035b05f04fec1527ca2aa98531a807db8cf
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307393"
---
# <a name="unicode-data"></a>Dados Unicode
Os tipos de dados SQL Unicode são fornecidos para descrever dados que residem no Unicode nativamente no DBMS. Um tipo de dados C Unicode é fornecido para permitir que um aplicativo vincule dados a um buffer Unicode. O Driver Manager pode converter dados de um tipo Unicode C (SQL_C_WCHAR) para fazê-lo funcionar com um driver ANSI.  
  
 Um ODBC 3.0 ou 2. *x* aplicativo sempre se ligará aos tipos de dados ANSI. Para obter um desempenho ideal, um aplicativo ODBC 3.5 (ou superior) deve se vincular ao tipo C de dados ANSI se o tipo de coluna SQL for ANSI, e deve se vincular ao tipo de dados Unicode C se o tipo de coluna SQL for Unicode.  
  
 Os indicadores do tipo SQL Unicode são SQL_WCHAR, SQL_WVARCHAR e SQL_WLONGVARCHAR. SQL_WCHAR dados tem um comprimento de corda fixo, enquanto SQL_WVARCHAR tem um comprimento variável com um máximo declarado e SQL_WLONGVARCHAR tem um comprimento variável com um máximo que depende da fonte de dados.  
  
 O indicador do tipo C Unicode é SQL_C_WCHAR. Este é o padrão para cada um dos indicadores do tipo SQL Unicode. Todos os tipos de SQL podem ser convertidos em SQL_C_WCHAR, e SQL_C_WCHAR podem ser convertidos para todos os tipos de SQL. Um aplicativo pode recuperar dados de três maneiras:  
  
-   Recupere os dados como SQL_C_CHAR.  
  
-   Recupere os dados como SQL_C_WCHAR.  
  
-   Declare os dados como SQL_C_TCHAR. Esta é uma macro que insere SQL_C_WCHAR se o aplicativo for compilado como um aplicativo Unicode ou inserir SQL_C_CHAR se for compilado como um aplicativo ANSI.  
  
 SQL_C_TCHAR é declarado em uma função da seguinte forma:  
  
```  
SQLBindParameter(StatementHandle, 1, SQL_PARAM_INPUT, SQL_C_TCHAR, SQL_WCHAR, NameLen, 0, Name, 0, &Name)  
```  
  
 Quando o aplicativo é compilado como um aplicativo Unicode, o argumento *ValueType* seria alterado de SQL_C_TCHAR para SQL_C_WCHAR. Quando o aplicativo é compilado como um aplicativo ANSI, o argumento *ValueType* seria alterado para SQL_C_CHAR.  
  
 Os drivers Unicode ainda devem suportar os tipos de dados ANSI, incluindo SQL_CHAR. Se um aplicativo que trabalha com um driver Unicode se vincular a SQL_CHAR, o Gerenciador de driver não mapeará os dados de SQL_CHAR para SQL_WCHAR. O driver Unicode deve aceitar os dados SQL_CHAR.  
  
 O Driver Manager armazena nomes de driver e DSN no Unicode e os mapeia para ANSI conforme necessário. Se um caractere Unicode não puder ser mapeado para um caractere ANSI (como pode ocorrer se caracteres de uma página de código que não é a página de código nativo do computador forem usados em nomes de driver e DSN), os caracteres que não puderam ser convertidos serão representados por um caractere padrão fornecido pelo sistema.
