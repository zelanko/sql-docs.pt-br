---
title: Resumo de função ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- functions [ODBC], listed by task
ms.assetid: 7aa635da-e6b7-439f-8e9b-c3860e24de5e
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9aab042c14953c170d86dda5fcd3432a471a12b6
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="odbc-function-summary"></a>Resumo de função ODBC
A tabela a seguir lista funções ODBC, agrupadas por tipo de tarefa e inclui a designação de conformidade e uma breve descrição da finalidade de cada função. Para obter mais informações sobre as designações de conformidade, consulte [ODBC e a CLI padrão](../../../odbc/reference/odbc-and-the-standard-cli.md). Para obter mais informações sobre a sintaxe e semântica para cada função, consulte [referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Um aplicativo pode chamar o **SQLGetInfo** função para obter informações sobre um driver de compatibilidade. Para obter informações sobre o suporte para uma função específica em um driver, um aplicativo pode chamar **SQLGetFunctions**.  
  
|Tarefa|Nome da função|Conformidade|Finalidade|  
|----------|-------------------|-----------------|-------------|  
|Conectando-se a uma fonte de dados|[SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)|ISO 92|Obtém um identificador de ambiente, conexão, instrução ou descritor.|  
||[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)|ISO 92|Se conecta a um driver específico pelo nome da fonte de dados, ID de usuário e senha.|  
||[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|ODBC|Se conecta a um driver específico por solicitações que o Gerenciador de Driver e o driver exibem caixas de diálogo de conexão para o usuário ou de cadeia de caracteres de conexão.|  
||[SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|ODBC|Retorna os níveis sucessivos de atributos de conexão e valores de atributo válido. Quando um valor foi especificado para cada atributo de conexão, conecta-se à fonte de dados.|  
|Obtendo informações sobre um driver e uma fonte de dados|[SQLDataSources](../../../odbc/reference/syntax/sqldatasources-function.md)<br /><br /> [SQLDrivers](../../../odbc/reference/syntax/sqldrivers-function.md)|ISO 92<br /><br /> ODBC|Retorna a lista de fontes de dados disponíveis.<br /><br /> Retorna a lista de drivers instalados e seus atributos.|  
||[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)|ISO 92|Retorna informações sobre uma fonte de dados e o driver específica.|  
||[SQLGetFunctions](../../../odbc/reference/syntax/sqlgetfunctions-function.md)|ISO 92|Retorna a funções de driver com suporte.|  
||[SQLGetTypeInfo](../../../odbc/reference/syntax/sqlgettypeinfo-function.md)|ISO 92|Retorna informações sobre os tipos de dados com suporte.|  
|Configurando e recuperando os atributos de driver|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)<br /><br /> [SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|ISO 92<br /><br /> ISO 92|Define um atributo de conexão.<br /><br /> Retorna o valor de um atributo de conexão.|  
||[SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)|ISO 92|Define um atributo de ambiente.|  
||[SQLGetEnvAttr](../../../odbc/reference/syntax/sqlgetenvattr-function.md)|ISO 92|Retorna o valor de um atributo de ambiente.|  
||[SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|ISO 92|Define um atributo de instrução.|  
||[SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|ISO 92|Retorna o valor de um atributo de instrução.|  
|Configurando e recuperando os campos de descritor|[SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md)<br /><br /> [SQLGetDescRec](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|ISO 92<br /><br /> ISO 92|Retorna o valor de um campo de descritor único.<br /><br /> Retorna os valores de vários campos de descritor.|  
||[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|ISO 92|Define um campo de descritor único.|  
||[SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|ISO 92|Define vários campos de descritor.|  
||[SQLCopyDesc](../../../odbc/reference/syntax/sqlcopydesc-function.md)|ISO 92|Copia informações do descritor de identificador de um descritor para outro.|  
|Solicitações de preparação do SQL|[SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|ISO 92|Prepara uma instrução SQL para execução posterior.|  
||[SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)|ODBC|Atribui o armazenamento para um parâmetro em uma instrução SQL.|  
||[SQLGetCursorName](../../../odbc/reference/syntax/sqlgetcursorname-function.md)|ISO 92|Retorna o nome de cursor associado a um identificador de instrução.|  
||[SQLSetCursorName](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|ISO 92|Especifica um nome de cursor.|  
||[SQLSetScrollOptions](../../../odbc/reference/syntax/sqlsetscrolloptions-function.md)|ODBC|Define as opções que controlam o comportamento do cursor.|  
|Enviando solicitações|[SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)<br /><br /> [SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|ISO 92<br /><br /> ISO 92|Executa uma instrução preparada.<br /><br /> Executa uma instrução.|  
||[SQLNativeSql](../../../odbc/reference/syntax/sqlnativesql-function.md)|ODBC|Retorna o texto de uma instrução SQL, conforme convertidos pelo driver.|  
||[SQLDescribeParam](../../../odbc/reference/syntax/sqldescribeparam-function.md)|ODBC|Retorna a descrição de um parâmetro específico em uma instrução.|  
||[SQLNumParams](../../../odbc/reference/syntax/sqlnumparams-function.md)|ISO 92|Retorna o número de parâmetros em uma instrução.|  
||[SQLParamData](../../../odbc/reference/syntax/sqlparamdata-function.md)|ISO 92|Usado em conjunto com **SQLPutData** para fornecer dados de parâmetro em tempo de execução. (Útil para valores de dados longos).|  
||[SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)|ISO 92|Envia parte ou todo um valor de dados para um parâmetro. (Útil para valores de dados longos).|  
|Recuperando informações sobre os resultados e resultados|[SQLRowCount](../../../odbc/reference/syntax/sqlrowcount-function.md)<br /><br /> [SQLNumResultCols](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|ISO 92<br /><br /> ISO 92|Retorna o número de linhas afetadas por uma inserção, atualização ou solicitação de exclusão.<br /><br /> Retorna o número de colunas no conjunto de resultados.|  
||[SQLDescribeCol](../../../odbc/reference/syntax/sqldescribecol-function.md)|ISO 92|Descreve uma coluna no conjunto de resultados.|  
||[SQLColAttribute](../../../odbc/reference/syntax/sqlcolattribute-function.md)|ISO 92|Descreve os atributos de uma coluna no conjunto de resultados.|  
||[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|ISO 92|Atribui o armazenamento para uma coluna de resultado e especifica o tipo de dados.|  
||[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|ISO 92|Retorna várias linhas de resultado.|  
||[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|ISO 92|Retorna as linhas de resultados roláveis.|  
||[SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)|ISO 92|Retorna parte ou toda uma coluna de uma linha de um resultado definido. (Útil para valores de dados longos).|  
||[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)|ODBC|Posiciona um cursor em um bloco de busca de dados e permite que um aplicativo para atualizar dados no conjunto de linhas ou atualizar ou excluir dados no conjunto de resultados.|  
||[SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|ODBC|Executa inserções em massa e indicador em massa operações, incluindo atualização, excluir e buscar por indicador.|  
||[SQLMoreResults](../../../odbc/reference/syntax/sqlmoreresults-function.md)|ODBC|Determina se há mais conjuntos de resultados disponíveis e, nesse caso, inicializa o processamento para o próximo conjunto de resultados.|  
||[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)|ISO 92|Retorna informações adicionais de diagnóstico (um único campo da estrutura de dados de diagnóstico).|  
||[SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)|ISO 92|Retorna informações adicionais de diagnóstico (vários campos da estrutura de dados de diagnóstico).|  
|Obtendo informações sobre tabelas do sistema da fonte de dados (funções de catálogo)|[SQLColumnPrivileges](../../../odbc/reference/syntax/sqlcolumnprivileges-function.md)<br /><br /> [SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md)|ODBC<br /><br /> Open Group|Retorna uma lista de colunas e os privilégios associados para uma ou mais tabelas.<br /><br /> Retorna a lista de nomes de colunas em tabelas especificadas.|  
||[SQLForeignKeys](../../../odbc/reference/syntax/sqlforeignkeys-function.md)|ODBC|Retorna uma lista de nomes de colunas que constituem as chaves estrangeiras, se eles existem para uma tabela especificada.|  
||[SQLPrimaryKeys](../../../odbc/reference/syntax/sqlprimarykeys-function.md)|ODBC|Retorna a lista de nomes de colunas que compõem a chave primária para uma tabela.|  
||[SQLProcedureColumns](../../../odbc/reference/syntax/sqlprocedurecolumns-function.md)|ODBC|Retorna a lista de parâmetros de saída e entrada, bem como as colunas que compõem o conjunto de resultados para os procedimentos especificados.|  
||[SQLProcedures](../../../odbc/reference/syntax/sqlprocedures-function.md)|ODBC|Retorna a lista de nomes de procedimentos armazenados em uma fonte de dados específico.|  
||[SQLSpecialColumns](../../../odbc/reference/syntax/sqlspecialcolumns-function.md)|Open Group|Retorna informações sobre o conjunto ideal de colunas que identifica exclusivamente uma linha em uma tabela especificada ou as colunas que são atualizadas automaticamente quando qualquer valor na linha é atualizada por uma transação.|  
||[SQLStatistics](../../../odbc/reference/syntax/sqlstatistics-function.md)|ISO 92|Retorna estatísticas sobre uma única tabela e a lista de índices associados à tabela.|  
||[SQLTablePrivileges](../../../odbc/reference/syntax/sqltableprivileges-function.md)|ODBC|Retorna uma lista de tabelas e os privilégios associados a cada tabela.|  
||[SQLTables](../../../odbc/reference/syntax/sqltables-function.md)|Open Group|Retorna a lista de nomes de tabela armazenada em uma fonte de dados específico.|  
|Encerrando uma instrução|[SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md)|ISO 92|Termina o processamento de instrução, descartará resultados pendentes e, opcionalmente, libera todos os recursos associados com o identificador de instrução.|  
||[SQLCloseCursor](../../../odbc/reference/syntax/sqlclosecursor-function.md)|ISO 92|Fecha um cursor que foi aberto em um identificador de instrução.|  
||[SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|ISO 92|Cancela o processamento em uma instrução.|  
||[SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md)|ODBC|Cancela o processamento em uma instrução ou a conexão.|  
||[SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)|ISO 92|Confirma ou reverte uma transação.|  
|Encerrar uma conexão|[SQLDisconnect](../../../odbc/reference/syntax/sqldisconnect-function.md)<br /><br /> [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)|ISO 92<br /><br /> ISO 92|Fecha a conexão.<br /><br /> Libera um identificador de ambiente, conexão, instrução ou descritor.|
