---
title: Funções de API de nível 2 (Driver ODBC para Oracle) | Microsoft Docs
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
- ODBC level 2 API functions [ODBC]
- functions [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], functions
- ODBC API functions [ODBC]
- API functions [ODBC]
- level 2 API functions [ODBC]
ms.assetid: d9f49520-72d7-4234-8635-260d0ce4199c
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a3209e07c2601de33b9d83a422ca8f986fb9326b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="level-2-api-functions-odbc-driver-for-oracle"></a>Funções de API de nível 2 (Driver ODBC para Oracle)
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 Funções neste nível fornecem funcionalidade adicional, como suporte a indicadores, parâmetros dinâmicos e execução assíncrona de funções ODBC além de conformidade de interface de nível 1.  
  
|Função de API|Observações|  
|------------------|-----------|  
|**SQLBindParameter**|Associa um buffer com um marcador de parâmetro em uma instrução SQL.|  
|**SQLBrowseConnect**|Retorna os níveis sucessivos de atributos e valores de atributo.|  
|**SQLDataSources**|Lista os nomes de fonte de dados. Implementado pelo Gerenciador de Driver.|  
|**SQLDescribeParam**|Retorna a descrição de um marcador de parâmetro associado com uma instrução SQL preparada.<br /><br /> Retorna uma estimativa melhor do que o parâmetro é, com base na análise de instrução. Se o tipo de parâmetro não pode ser determinado, SQL_VARCHAR retorna com comprimento de 2000.|  
|**SQLDrivers**|Implementado pelo Gerenciador de Driver.|  
|**SQLExtendedFetch**|Semelhante ao **SQLFetch** mas retorna várias linhas usando uma matriz para cada coluna. O conjunto de resultados é rolável de avanço e pode ser feito com versões anteriores rolável se o cursor está definido para ser estático, não somente de encaminhamento. Para cursores de somente avanço com associação de coluna padrão, os dados da coluna de conjuntos de dados maiores do que o atributo de conexão BUFFERSIZE são buscados diretamente em buffers de dados. Não oferece suporte a indicadores de comprimento variável e não dá suporte a busca de um conjunto de linhas em um deslocamento (diferente de 0) de um indicador.|  
|**SQLForeignKeys**|Retorna uma lista de chaves estrangeiras em uma única tabela ou uma lista de chaves estrangeiras em outras tabelas que fazem referência a uma única tabela.|  
|**SQLMoreResults**|Determina se houver mais resultados pendentes em um identificador de instrução, hstmt, contendo instruções SELECT, UPDATE, INSERT ou DELETE e em caso afirmativo, inicializa o processamento para esses resultados.<br /><br /> Oracle oferece suporte a vários conjuntos de resultados somente de procedimentos armazenados, ao usar sequências de escape {resultset...}.|  
|**SQLNativeSql**|Para obter informações sobre o uso, consulte [retornar parâmetros do conjunto de procedimentos armazenados](../../odbc/microsoft/returning-array-parameters-from-stored-procedures.md).|  
|**SQLNumParams**|Retorna o número de parâmetros em uma instrução SQL. O número de parâmetros deve ser igual ao número de pontos de interrogação na instrução SQL passada para **SQLPrepare**.|  
|**SQLPrimaryKeys**|Retorna os nomes das colunas que compõem a chave primária para uma tabela.|  
|**SQLProcedureColumns**|Retorna uma lista de parâmetros de saída e entrada, o valor de retorno, as colunas no conjunto de resultados de um único procedimento e duas colunas adicionais, sobrecarga e ORDINAL_POSITION. SOBRECARGA é a coluna de sobrecarga da tabela ALL_ARGUMENTS da exibição de dicionário de dados Oracle. ORDINAL_POSITION é a coluna de SEQUÊNCIA da tabela ALL_ARGUMENTS da exibição de dicionário de dados Oracle. Para procedimentos de pacotes, a coluna de nome de procedimento está em *packagename.procedurename* formato. Não retorna as colunas do procedimento de um sinônimo criado que se refere a um procedimento ou função.|  
|**SQLProcedures**|Retorna uma lista de procedimentos na fonte de dados. Para procedimentos de pacotes, a coluna de nome de procedimento está em *packagename.procedurename* formato.<br /><br /> Como o Oracle não fornece uma forma de distinguir empacotados procedimentos de funções empacotadas, o driver retorna SQL_PT_UNKNOWN para a coluna PROCEDURE_TYPE.|  
|**SQLSetPos**|Define a posição do cursor em um conjunto de linhas. Você pode usar **SQLSetPos** com **SQLGetData** para recuperar linhas de colunas desassociadas depois posicionando o cursor para uma linha específica no conjunto de linhas. Linhas adicionadas ao conjunto de resultados usando *fOption* SQL_ADD são adicionados após a última linha no conjunto de resultados.|  
|**SQLSetScrollOptions**|Define as opções que controlam o comportamento de cursores associado com um identificador de instrução, hstmt. Para obter detalhes, consulte [combinações de simultaneidade e o tipo de Cursor](../../odbc/microsoft/cursor-type-and-concurrency-combinations.md).|
