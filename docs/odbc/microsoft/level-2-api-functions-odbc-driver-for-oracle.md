---
title: Funções de API de nível 2 (driver ODBC para Oracle) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC level 2 API functions [ODBC]
- functions [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], functions
- ODBC API functions [ODBC]
- API functions [ODBC]
- level 2 API functions [ODBC]
ms.assetid: d9f49520-72d7-4234-8635-260d0ce4199c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7600734fef44071b1f5e35c136a6b9facdb8b390
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67949031"
---
# <a name="level-2-api-functions-odbc-driver-for-oracle"></a>Funções de API de nível 2 (Driver ODBC para Oracle)
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 As funções nesse nível fornecem conformidade de interface de nível 1, além de funcionalidades adicionais, como suporte para indicadores, parâmetros dinâmicos e execução assíncrona de funções ODBC.  
  
|Função de API|Observações|  
|------------------|-----------|  
|**SQLBindParameter**|Associa um buffer a um marcador de parâmetro em uma instrução SQL.|  
|**SQLBrowseConnect**|Retorna níveis sucessivos de atributos e valores de atributo.|  
|**SQLDataSources**|Lista nomes de fontes de dados. Implementado pelo Gerenciador de driver.|  
|**SQLDescribeParam**|Retorna a descrição de um marcador de parâmetro associado a uma instrução SQL preparada.<br /><br /> Retorna uma melhor estimativa do que é o parâmetro, com base na análise da instrução. Se o tipo de parâmetro não puder ser determinado, SQL_VARCHAR retornará com o comprimento 2000.|  
|**SQLDrivers**|Implementado pelo Gerenciador de driver.|  
|**SQLExtendedFetch**|Semelhante a **SQLFetch** , mas retorna várias linhas usando uma matriz para cada coluna. O conjunto de resultados é de encaminhamento progressivo e pode ser rolado para trás se o cursor for definido como estático, não somente encaminhamento. Para cursores de somente avanço com associação de coluna padrão, os dados de coluna de conjuntos de dados maiores do que o atributo de conexão BUFFERSIZE são buscados diretamente nos buffers de dados. O não oferece suporte a indicadores de comprimento variável e não oferece suporte à busca de um conjunto de linhas em um deslocamento (diferente de 0) a partir de um indicador.|  
|**SQLForeignKeys**|Retorna uma lista de chaves estrangeiras em uma única tabela ou uma lista de chaves estrangeiras em outras tabelas que se referem a uma única tabela.|  
|**SQLMoreResults**|Determina se mais resultados estão pendentes em um identificador de instrução, HSTMT, contendo instruções SELECT, UPDATE, INSERT ou DELETE e, nesse caso, inicializa o processamento para esses resultados.<br /><br /> O Oracle dá suporte a vários conjuntos de resultados somente de procedimentos armazenados, ao usar as sequências de escape {ResultSet...}.|  
|**SQLNativeSql**|Para obter informações sobre o uso, consulte [retornando parâmetros de matriz de procedimentos armazenados](../../odbc/microsoft/returning-array-parameters-from-stored-procedures.md).|  
|**SQLNumParams**|Retorna o número de parâmetros em uma instrução SQL. O número de parâmetros deve ser igual ao número de pontos de interrogação na instrução SQL passado para **SQLPrepare**.|  
|**SQLPrimaryKeys**|Retorna os nomes de coluna que compõem a chave primária de uma tabela.|  
|**SQLProcedureColumns**|Retorna uma lista de parâmetros de entrada e saída, o valor de retorno, as colunas no conjunto de resultados de um único procedimento e duas colunas adicionais, sobrecarga e ORDINAL_POSITION. OVERLOAD é a coluna OVERLOAD da tabela ALL_ARGUMENTS da exibição do dicionário de dados Oracle. ORDINAL_POSITION é a coluna de sequência da tabela ALL_ARGUMENTS da exibição do dicionário de dados Oracle. Para procedimentos empacotados, a coluna de nome do procedimento está no formato *PackageName.* testnamename. Não retorna as colunas de procedimento de um sinônimo criado que se refere a um procedimento ou função.|  
|**SQLProcedures**|Retorna uma lista de procedimentos na fonte de dados. Para procedimentos empacotados, a coluna de nome do procedimento está no formato *PackageName.* testnamename.<br /><br /> Como a Oracle não fornece uma maneira de distinguir os procedimentos empacotados das funções empacotadas, o driver retorna SQL_PT_UNKNOWN para a coluna PROCEDURE_TYPE.|  
|**SQLSetPos**|Define a posição do cursor em um conjunto de linhas. Você pode usar **SQLSetPos** com **SQLGetData** para recuperar linhas de colunas desassociadas depois de posicionar o cursor em uma linha específica no conjunto de linhas. As linhas adicionadas ao conjunto de resultados usando *fOption* SQL_ADD são adicionadas após a última linha no conjunto de resultados.|  
|**SQLSetScrollOptions**|Define opções que controlam o comportamento dos cursores associados a um identificador de instrução, HSTMT. Para obter detalhes, consulte [tipos de cursor e combinações de simultaneidade](../../odbc/microsoft/cursor-type-and-concurrency-combinations.md).|
