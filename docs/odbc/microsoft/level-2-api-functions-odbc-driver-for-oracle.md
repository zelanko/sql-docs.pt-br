---
title: Funções de API nível 2 (Driver ODBC para Oracle) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b1e181c5863d6b906eaf9a3ba499728c595f0449
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284176"
---
# <a name="level-2-api-functions-odbc-driver-for-oracle"></a>Funções de API de nível 2 (Driver ODBC para Oracle)
> [!IMPORTANT]  
>  Esse recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 As funções neste nível fornecem conformidade de interface nível 1, além de funcionalidades adicionais, como suporte para marcadores, parâmetros dinâmicos e execução assíncrona das funções ODBC.  
  
|Função API|Observações|  
|------------------|-----------|  
|**SQLBindParameter**|Associa um buffer com um marcador de parâmetro em uma declaração SQL.|  
|**SQLBrowseConnect**|Retorna níveis sucessivos de atributos e valores de atributos.|  
|**SQLDataSources**|Lista nomes de origem de dados. Implementado pelo Driver Manager.|  
|**SQLDescribeParam**|Retorna a descrição de um marcador de parâmetro associado a uma declaração SQL preparada.<br /><br /> Retorna um melhor palpite de qual é o parâmetro, com base na análise da declaração. Se o tipo de parâmetro não puder ser determinado, SQL_VARCHAR retorna com comprimento 2000.|  
|**SQLDrivers**|Implementado pelo Driver Manager.|  
|**Sqlextendedfetch**|Semelhante ao **SQLFetch,** mas retorna várias linhas usando uma matriz para cada coluna. O conjunto de resultados é rolável para a frente e pode ser feito para trás se o cursor for definido como estático, não apenas para frente. Para cursores somente para encaminhamento com vinculação de coluna padrão, os dados da coluna de conjuntos de dados maiores que o atributo de conexão BUFFERSIZE são obtidos diretamente em buffers de dados. Não suporta marcadores de comprimento variável e não suporta buscar um conjunto de linhas em um offset (diferente de 0) de um marcador.|  
|**SQLForeignKeys**|Retorna uma lista de chaves estrangeiras em uma única tabela ou uma lista de chaves estrangeiras em outras tabelas que se referem a uma única tabela.|  
|**SQLMoreResults**|Determina se mais resultados estão pendentes em uma alça de declaração, hstmt, contendo instruções SELECT, UPDATE, INSERT ou DELETE e, se for o caso, inicia o processamento desses resultados.<br /><br /> O Oracle suporta vários conjuntos de resultados somente a partir de procedimentos armazenados, ao usar {resultset... } seqüências de fuga.|  
|**SQLNativeSql**|Para obter informações sobre o uso, consulte ['''Parâmetros do array' dos procedimentos armazenados](../../odbc/microsoft/returning-array-parameters-from-stored-procedures.md).|  
|**SQLNumParams**|Retorna o número de parâmetros em uma declaração SQL. O número de parâmetros deve ser igual ao número de pontos de interrogação na declaração SQL passada para **SQLPrepare**.|  
|**SQLPrimaryKeys**|Retorna os nomes da coluna que compõem a chave principal de uma tabela.|  
|**SQLProcedureColumns**|Retorna uma lista de parâmetros de entrada e saída, o valor de retorno, as colunas no conjunto de resultados de um único procedimento e duas colunas adicionais, OVERLOAD e ORDINAL_POSITION. OVERLOAD é a coluna OVERLOAD da tabela ALL_ARGUMENTS do Oracle Data Dictionary View. ORDINAL_POSITION é a coluna SEQÜENCIAl da tabela ALL_ARGUMENTS do Oracle Data Dictionary View. Para procedimentos empacotados, a coluna NOME DE PROCEDIMENTO está no formato *packagename.procedurename.* Não retorna as colunas de procedimento de um sinônimo criado que se refere a um procedimento ou função.|  
|**SQLProcedures**|Retorna uma lista de procedimentos na fonte de dados. Para procedimentos empacotados, a coluna NOME DE PROCEDIMENTO está no formato *packagename.procedurename.*<br /><br /> Como a Oracle não fornece uma maneira de distinguir procedimentos embalados das funções empacotadas, o driver retorna SQL_PT_UNKNOWN para a coluna PROCEDURE_TYPE.|  
|**SQLSetPos**|Define a posição do cursor em um conjunto de linhas. Você pode usar **SQLSetPos** com **SQLGetData** para recuperar linhas de colunas desvinculadas depois de posicionar o cursor para uma linha específica no conjunto de linhas. As linhas adicionadas ao conjunto de resultados usando *fOption* SQL_ADD são adicionadas após a última linha no conjunto de resultados.|  
|**Opções de SQLSetScroll**|Define opções que controlam o comportamento de cursores associados a uma alça de declaração, hstmt. Para obter detalhes, consulte [Tipo de Cursor e Combinações de Concorrência](../../odbc/microsoft/cursor-type-and-concurrency-combinations.md).|
