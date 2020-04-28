---
title: Funções de API de nível 1 (driver ODBC para Oracle) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- functions [ODBC], ODBC driver for Oracle
- ODBC level 1 API functions [ODBC]
- ODBC driver for Oracle [ODBC], functions
- level 1 API functions [ODBC]
- API functions [ODBC]
ms.assetid: 98cced6f-41b8-43c1-a3cd-f4ea1615c0af
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 37305ee75ebeb0686bafe039f1102cb3c6e18674
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299946"
---
# <a name="level-1-api-functions-odbc-driver-for-oracle"></a>Funções de API de nível 1 (Driver ODBC para Oracle)
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 As funções neste nível fornecem a conformidade da interface principal, além de funcionalidades adicionais, como o suporte a transações.  
  
|Função de API|Observações|  
|------------------|-----------|  
|**SQLColumns**|Cria um conjunto de resultados para uma tabela, que é a lista de colunas para a tabela ou tabelas especificadas. Quando você solicita colunas para um sinônimo público, deve definir o atributo de conexão SYNONYMCOLUMNS e especificou uma cadeia de caracteres vazia como o argumento *szTableOwner* . Ao retornar colunas para sinônimos públicos, o driver define a coluna de nome da tabela como uma cadeia de caracteres vazia. O conjunto de resultados contém uma coluna adicional, posição ORDINAL, no final de cada linha. Esse valor é a posição ordinal da coluna na tabela.|  
|**SQLDriverConnect**|Conecta-se a uma fonte de dados existente. Para obter detalhes, consulte [formato e atributos da cadeia de conexão](../../odbc/microsoft/connection-string-format-and-attributes.md).|  
|**SQLGetConnectOption**|Retorna a configuração atual de uma opção de conexão. Essa função tem suporte parcial. O driver dá suporte a todos os valores para o argumento *fOption* , mas não dá suporte a alguns valores de *vParam* para o argumento *fOption* [SQL_TXN_ISOLATION](../../odbc/microsoft/connect-options.md). Para obter mais informações, consulte [Opções de conexão](../../odbc/microsoft/connect-options.md).|  
|**SQLGetData**|Recupera o valor de um único campo no registro atual do conjunto de resultados fornecido.|  
|**SQLGetFunctions**|Retorna TRUE para todas as funções com suporte. Implementado pelo Gerenciador de driver.|  
|**SQLGetInfo**|Retorna informações, incluindo SQLHDBC, SQLUSMALLINT, sqlpointr, SQLSMALLINT e SQLSMALLINT \*, sobre o driver ODBC para Oracle e a fonte de dados associada a um identificador de conexão, *HDBC*.|  
|**SQLGetStmtOption**|Retorna a configuração atual de uma opção de instrução. Para obter mais informações, consulte [Opções de instrução](../../odbc/microsoft/statement-options.md).|  
|**SQLGetTypeInfo**|Retorna informações sobre os tipos de dados com suporte por uma fonte de dados. O driver retorna as informações em um conjunto de resultados SQL.|  
|**SQLParamData**|Usado em conjunto com **SQLPutData** para especificar dados de parâmetro no tempo de execução da instrução.|  
|**SQLPutData**|Permite que um aplicativo envie dados para um parâmetro ou coluna para o driver no momento da execução da instrução.|  
|**SQLSetConnectOption**|Fornece acesso a opções que regem aspectos da conexão. Esta função tem suporte parcial: o driver dá suporte a todos os valores para o argumento *fOption* , mas não dá suporte a alguns valores de *vParam* para o argumento *fOption* [SQL_TXN_ISOLATION](../../odbc/microsoft/connect-options.md). Para obter mais informações, consulte [Opções de conexão](../../odbc/microsoft/connect-options.md).|  
|**SQLSetStmtOption**|Define opções relacionadas a um identificador de instrução, *HSTMT*. Para obter mais informações, consulte [Opções de instrução](../../odbc/microsoft/statement-options.md).|  
|**SQLSpecialColumns**|Recupera o conjunto ideal de colunas que identifica exclusivamente uma linha na tabela.|  
|**SQLStatistics**|Recupera uma lista de estatísticas sobre uma única tabela e os índices, ou nomes de marca, associados à tabela. O driver retorna as informações como um conjunto de resultados.|  
|**SQLTables**|Retorna a lista de nomes de tabela especificada pelo parâmetro na instrução **SQLTables** . Se nenhum parâmetro for especificado, retornará os nomes de tabela armazenados na fonte de dados atual. O driver retorna as informações como um conjunto de resultados.<br /><br /> Chamadas de tipo de enumeração não receberão uma entrada de conjunto de resultados para exibições remotas ou exibições com parâmetros locais. No entanto, uma chamada para **SQLTables** com um especificador de nome de tabela exclusivo encontrará uma correspondência para tal exibição, se presente, com esse nome; Isso permite que a API Verifique se há conflitos de nome antes da criação de uma nova tabela.<br /><br /> Os sinônimos públicos são retornados com um valor TABLE_OWNER de "".<br /><br /> EXIBIções pertencentes a SYS ou SYSTEM são identificadas como exibição do sistema.|
