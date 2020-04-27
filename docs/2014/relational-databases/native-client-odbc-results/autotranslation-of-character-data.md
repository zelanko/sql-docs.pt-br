---
title: Tradução automática de dados de caractere | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- result sets [ODBC], autotranslating character data
- data types [ODBC], autotranslating character data
- ACPs
- SQL Server Native Client ODBC driver, result sets
- ODBC applications, result sets
- AutoTranslate feature
- ANSI code pages
- character data autotranslation [ODBC]
- autotranslating character data
- SQL Server Native Client ODBC driver, data types
- ODBC data types, autotranslating character data
ms.assetid: 86a8adda-c5ad-477f-870f-cb370c39ee13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5182ab1a72caac4181e50df2199f3e0457d3aaac
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63200216"
---
# <a name="autotranslation-of-character-data"></a>Tradução automática de dados de caracteres
  Os dados de caractere, como as variáveis de caractere ANSI declaradas com [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL_C_CHAR ou dados armazenados no usando os tipos de dados **Char**, **varchar**ou **Text** , podem representar apenas um número limitado de caracteres. Os dados de caractere armazenados que usam um byte por caractere podem representar apenas 256 caracteres. Os valores armazenados em variáveis SQL_C_CHAR são interpretados usando a ACP (página de código ANSI) do computador cliente. Os valores armazenados usando os tipos de dados **Char**, **varchar**ou **Text** no servidor são avaliados usando o ACP do servidor.  
  
 Se o servidor e o cliente tiverem o mesmo ACP, eles não terão problemas na interpretação dos valores armazenados nos objetos SQL_C_CHAR, **Char**, **varchar**ou **Text** . Se o servidor e o cliente tiverem ACPs diferentes, SQL_C_CHAR dados do cliente poderão ser interpretados como um caractere diferente no servidor se ele for usado nas colunas **Char**, **varchar**ou **Text** , Variables ou Parameters. Por exemplo, um byte de caractere contendo o valor 0xA5 é interpretado como o caractere?? em um computador usando a página de código 437 e é interpretado como o sinal de Iene (??) em um computador que executa a página de código 1252.  
  
 Dados de Unicode são armazenados usando dois bytes por caractere. Todos os caracteres estendidos são abordados pela especificação de Unicode. Dessa forma, todos os caracteres Unicode são interpretados da mesma maneira por todos os computadores.  
  
 O recurso de autotraduzir do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC do Native Client tenta minimizar os problemas na movimentação de dados de caractere entre um cliente e um servidor com páginas de código diferentes. A conversão automática pode ser definida na cadeia de conexão de [SQLDriverConnect](../native-client-odbc-api/sqldriverconnect.md), na cadeia de caracteres de configuração de [SQLConfigDataSource](../native-client-odbc-api/sqlconfigdatasource.md)ou ao configurar fontes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dados para o driver ODBC do Native Client usando o Administrador ODBC.  
  
 Quando AutoTranslate é definido como "no", nenhuma conversão é feita nos dados movidos entre SQL_C_CHAR variáveis nas colunas Client e **Char**, **varchar**ou **Text** , Variables ou Parameters em um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados. Os padrões de bit poderão ser interpretados de forma diferente nos computadores cliente e servidor se os dados contiverem caracteres estendidos e os dois computadores tiverem páginas de código diferentes. Os dados serão interpretados da mesma maneira se ambos os computadores tiverem a mesma página de código.  
  
 Quando AutoTranslate é definido como "Yes", o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC do Native Client usa Unicode para converter os dados movidos entre SQL_C_CHAR variáveis nas colunas Client e **Char**, **varchar**ou **Text** , Variables ou Parameters em um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados:  
  
-   Quando os dados são enviados de uma variável SQL_C_CHAR no cliente para uma coluna **Char**, **varchar**ou **Text** , uma variável ou um parâmetro em um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados, o driver ODBC primeiro converte de SQL_C_CHAR para Unicode usando o ACP do cliente e, em seguida, do Unicode de volta ao caractere usando o ACP do servidor.  
  
-   Quando os dados são enviados de uma coluna **Char**, **varchar**ou **Text** , variável ou parâmetro em um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados para uma SQL_C_CHAR variável no cliente, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC do Native Client primeiro converte de caractere para Unicode usando o ACP do servidor e, em seguida, do Unicode para SQL_C_CHAR usando o ACP do cliente.  
  
 Como todas essas conversões são feitas pelo driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client em execução no cliente, o servidor ACP deve ser uma das páginas de código instaladas no computador cliente.  
  
 Fazer as conversões de caractere por Unicode assegura a conversão adequada de todos os caracteres que existem nas duas páginas de código. Se um caractere existir em uma página de código, mas não em outra, entretanto, o caractere não poderá ser representado na página de código de destino. Por exemplo, a página de código 1252 tem o símbolo de marca registrada (??), enquanto a página de código 437 não.  
  
 A configuração AutoTranslate não tem nenhum efeito sobre essas conversões:  
  
-   Mover dados entre caracteres SQL_C_CHAR variáveis de cliente e colunas do Unicode **nchar**, **nvarchar**ou **ntext** , variáveis ou parâmetros em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bancos de dado.  
  
-   Mover dados entre Unicode SQL_C_WCHAR variáveis de cliente e caracteres **Char**, **varchar**, ou colunas de **texto** , variáveis ou parâmetros [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em bancos de dado.  
  
 Os dados devem sempre ser convertidos quando movidos de caractere para Unicode.  
  
## <a name="see-also"></a>Consulte Também  
 [Processando resultados &#40;&#41;ODBC](processing-results-odbc.md)   
 [Suporte a ordenações e a Unicode](../collations/collation-and-unicode-support.md)  
  
  
