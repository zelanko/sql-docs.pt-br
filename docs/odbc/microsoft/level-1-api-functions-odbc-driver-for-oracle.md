---
title: Funções de API de nível 1 (Driver ODBC para Oracle) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6a70116fb0e8ef1236b18cb478184e96fe08fce5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63262227"
---
# <a name="level-1-api-functions-odbc-driver-for-oracle"></a>Funções de API de nível 1 (Driver ODBC para Oracle)
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 Suportam a funções com este nível forneça conformidade de interface de núcleo mais funcionalidades adicionais, como a transação.  
  
|Função de API|Observações|  
|------------------|-----------|  
|**SQLColumns**|Cria um conjunto de resultados de uma tabela, que é a lista de colunas da tabela especificada ou tabelas. Quando você solicita colunas para um sinônimo público, você deve definir o atributo de conexão SYNONYMCOLUMNS e especificado de uma cadeia de caracteres vazia como o *szTableOwner* argumento. Ao retornar colunas para sinônimos públicos, o driver define a coluna de nome de tabela para uma cadeia de caracteres vazia. O conjunto de resultados contém uma coluna adicional, a posição ORDINAL, no final de cada linha. Esse valor é a posição ordinal da coluna na tabela.|  
|**SQLDriverConnect**|Conecta-se a uma fonte de dados existente. Para obter detalhes, consulte [formato de cadeia de caracteres de Conexão e atributos](../../odbc/microsoft/connection-string-format-and-attributes.md).|  
|**SQLGetConnectOption**|Retorna a configuração atual de uma opção de conexão. Essa função tem suporte parcial. O driver dá suporte a todos os valores para o *fOption* argumento, mas não dá suporte para alguns *vParam* os valores para o *fOption* argumento [SQL_TXN_ISOLATION ](../../odbc/microsoft/connect-options.md). Para obter mais informações, consulte [opções de conexão de](../../odbc/microsoft/connect-options.md).|  
|**SQLGetData**|Recupera o valor de um único campo no registro atual do conjunto de resultados fornecido.|  
|**SQLGetFunctions**|Retorna TRUE para todas as funções com suporte. Implementado pelo Gerenciador de Driver.|  
|**SQLGetInfo**|Retorna informações, incluindo SQLHDBC, SQLUSMALLINT, SQLPOINTER, SQLSMALLINT e SQLSMALLINT \*, sobre o Driver ODBC para Oracle e fonte de dados associada com um identificador de conexão *hdbc*.|  
|**SQLGetStmtOption**|Retorna a configuração atual de uma opção de instrução. Para obter mais informações, consulte [opções de instrução](../../odbc/microsoft/statement-options.md).|  
|**SQLGetTypeInfo**|Retorna informações sobre os tipos de dados compatíveis com uma fonte de dados. O driver retorna as informações em um conjunto de resultados SQL.|  
|**SQLParamData**|Usado em conjunto com **SQLPutData** para especificar dados de parâmetro durante o tempo de execução de instrução.|  
|**SQLPutData**|Permite que um aplicativo enviar dados para uma coluna ou parâmetro para o driver durante o tempo de execução de instrução.|  
|**SQLSetConnectOption**|Fornece acesso às opções que controlam aspectos da conexão. Essa função tem suporte parcial: O driver dá suporte a todos os valores para o *fOption* argumento, mas não dá suporte para alguns *vParam* os valores para o *fOption* argumento [SQL_TXN_ISOLATION ](../../odbc/microsoft/connect-options.md). Para obter mais informações, consulte [opções de conexão de](../../odbc/microsoft/connect-options.md).|  
|**SQLSetStmtOption**|Define opções relacionadas a um identificador de instrução *hstmt*. Para obter mais informações, consulte [opções de instrução](../../odbc/microsoft/statement-options.md).|  
|**SQLSpecialColumns**|Recupera o conjunto ideal de colunas que identifica exclusivamente uma linha na tabela.|  
|**SQLStatistics**|Recupera uma lista de estatísticas sobre uma única tabela e os índices ou nomes de marca, associados à tabela. O driver retorna as informações como um conjunto de resultados.|  
|**SQLTables**|Retorna a lista de nomes de tabela especificado pelo parâmetro na **SQLTables** instrução. Se nenhum parâmetro for especificado, retorna os nomes de tabela, armazenados na fonte de dados atual. O driver retorna as informações como um conjunto de resultados.<br /><br /> Chamadas de tipo de enumeração não receberão uma entrada de conjunto de resultados para modos de exibição remotos ou locais exibições com parâmetros. No entanto, uma chamada para **SQLTables** com uma tabela exclusiva especificador de nome encontrará uma correspondência para exibição, se estiver presente, com esse nome; Isso permite que a API verificar se há conflitos de nome antes da criação de uma nova tabela.<br /><br /> Sinônimos públicos são retornados com um valor TABLE_OWNER "".<br /><br /> Modos de exibição pertencentes a SYS ou sistema são identificados como exibição do sistema.|
