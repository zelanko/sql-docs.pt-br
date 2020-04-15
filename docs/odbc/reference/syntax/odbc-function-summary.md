---
title: Resumo da função ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- functions [ODBC], listed by task
ms.assetid: 7aa635da-e6b7-439f-8e9b-c3860e24de5e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c10cc7880cf941a1490f963e21e8b44bc91db215
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298917"
---
# <a name="odbc-function-summary"></a>Resumo de funções do ODBC
A tabela a seguir lista as funções oDBC, agrupadas por tipo de tarefa, e inclui a designação de conformidade e uma breve descrição do propósito de cada função. Para obter mais informações sobre designações de conformidade, consulte [ODBC e a CLI Padrão](../../../odbc/reference/odbc-and-the-standard-cli.md). Para obter mais informações sobre a sintaxe e semântica de cada função, consulte [API Reference .](../../../odbc/reference/syntax/odbc-api-reference.md)  
  
 Um aplicativo pode chamar a função **SQLGetInfo** para obter informações de conformidade sobre um driver. Para obter informações sobre o suporte para uma função específica em um driver, um aplicativo pode chamar **SQLGetFunctions**.  
  
|Tarefa|Nome da função|Conformidade|Finalidade|  
|----------|-------------------|-----------------|-------------|  
|Conectando-se a uma fonte de dados|[SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)|ISO 92|Obtém um ambiente, conexão, declaração ou alça descritor.|  
||[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)|ISO 92|Conecta-se a um driver específico por nome de origem de dados, ID de usuário e senha.|  
||[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|ODBCODBC|Conecta-se a um driver específico por seqüência de conexão ou solicita que o Gerenciador de driver e as caixas de diálogo de conexão do driver exibam para o usuário.|  
||[SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|ODBCODBC|Retorna níveis sucessivos de atributos de conexão e valores de atributos válidos. Quando um valor foi especificado para cada atributo de conexão, conecta-se à fonte de dados.|  
|Obtenção de informações sobre um driver e fonte de dados|[SQLDataSources](../../../odbc/reference/syntax/sqldatasources-function.md)<br /><br /> [SQLDrivers](../../../odbc/reference/syntax/sqldrivers-function.md)|ISO 92<br /><br /> ODBCODBC|Retorna a lista de fontes de dados disponíveis.<br /><br /> Retorna a lista de drivers instalados e seus atributos.|  
||[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)|ISO 92|Retorna informações sobre um driver específico e fonte de dados.|  
||[SQLGetFunctions](../../../odbc/reference/syntax/sqlgetfunctions-function.md)|ISO 92|Retorna funções de driver suportadas.|  
||[SQLGetTypeInfo](../../../odbc/reference/syntax/sqlgettypeinfo-function.md)|ISO 92|Retorna informações sobre tipos de dados suportados.|  
|Configuração e recuperação de atributos do driver|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)<br /><br /> [SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|ISO 92<br /><br /> ISO 92|Define um atributo de conexão.<br /><br /> Retorna o valor de um atributo de conexão.|  
||[SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)|ISO 92|Define um atributo de ambiente.|  
||[SQlGetEnvAttr](../../../odbc/reference/syntax/sqlgetenvattr-function.md)|ISO 92|Retorna o valor de um atributo de ambiente.|  
||[SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|ISO 92|Define um atributo de declaração.|  
||[SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|ISO 92|Retorna o valor de um atributo de declaração.|  
|Configuração e recuperação de campos descritores|[SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md)<br /><br /> [SQLGetDescRec](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|ISO 92<br /><br /> ISO 92|Retorna o valor de um único campo descritor.<br /><br /> Retorna os valores de vários campos descritores.|  
||[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|ISO 92|Define um único campo descritor.|  
||[SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|ISO 92|Define vários campos de descritores.|  
||[SQLCopyDesc](../../../odbc/reference/syntax/sqlcopydesc-function.md)|ISO 92|Copia informações do descritor de uma alça de descritor para outra.|  
|Preparando solicitações sql|[SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|ISO 92|Prepara uma declaração SQL para execução posterior.|  
||[SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)|ODBCODBC|Atribui o armazenamento de um parâmetro em uma instrução SQL.|  
||[SQLGetCursorName](../../../odbc/reference/syntax/sqlgetcursorname-function.md)|ISO 92|Retorna o nome do cursor associado a uma alça de declaração.|  
||[Sqlsetcursorname](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|ISO 92|Especifica um nome do cursor.|  
||[Opções de SQLSetScroll](../../../odbc/reference/syntax/sqlsetscrolloptions-function.md)|ODBCODBC|Define opções que controlam o comportamento do cursor.|  
|Envio de solicitações|[SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)<br /><br /> [SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|ISO 92<br /><br /> ISO 92|Executa uma instrução preparada.<br /><br /> Executa uma instrução.|  
||[SQLNativeSql](../../../odbc/reference/syntax/sqlnativesql-function.md)|ODBCODBC|Retorna o texto de uma declaração SQL traduzida pelo driver.|  
||[SQLDescribeParam](../../../odbc/reference/syntax/sqldescribeparam-function.md)|ODBCODBC|Retorna a descrição para um parâmetro específico em uma declaração.|  
||[SQLNumParams](../../../odbc/reference/syntax/sqlnumparams-function.md)|ISO 92|Retorna o número de parâmetros em uma declaração.|  
||[SQLParamData](../../../odbc/reference/syntax/sqlparamdata-function.md)|ISO 92|Usado em conjunto com **o SQLPutData** para fornecer dados de parâmetros no momento da execução. (Útil para longos valores de dados.)|  
||[SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)|ISO 92|Envia parte ou todo um valor de dados para um parâmetro. (Útil para longos valores de dados.)|  
|Recuperando resultados e informações sobre resultados|[SQLRowCount](../../../odbc/reference/syntax/sqlrowcount-function.md)<br /><br /> [SQLNumResultCols](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|ISO 92<br /><br /> ISO 92|Retorna o número de linhas afetadas por uma solicitação de inserção, atualização ou exclusão.<br /><br /> Retorna o número de colunas no conjunto de resultados.|  
||[SQLDescribeCol](../../../odbc/reference/syntax/sqldescribecol-function.md)|ISO 92|Descreve uma coluna no conjunto de resultados.|  
||[SQLColAttribute](../../../odbc/reference/syntax/sqlcolattribute-function.md)|ISO 92|Descreve atributos de uma coluna no conjunto de resultados.|  
||[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|ISO 92|Atribui o armazenamento a uma coluna de resultados e especifica o tipo de dados.|  
||[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|ISO 92|Retorna várias linhas de resultados.|  
||[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|ISO 92|Retorna linhas de resultados roláveis.|  
||[SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)|ISO 92|Retorna parte ou todas de uma coluna de uma linha de um conjunto de resultados. (Útil para longos valores de dados.)|  
||[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)|ODBCODBC|Posiciona um cursor dentro de um bloco de dados e permite que um aplicativo atualize dados no conjunto de linhas ou atualize ou exclua dados no conjunto de resultados.|  
||[SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|ODBCODBC|Executa inserções em massa e operações de marcação em massa, incluindo atualização, exclusão e busca por marcador.|  
||[SQLMoreResults](../../../odbc/reference/syntax/sqlmoreresults-function.md)|ODBCODBC|Determina se há mais conjuntos de resultados disponíveis e, se for o caso, inicia o processamento para o próximo conjunto de resultados.|  
||[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)|ISO 92|Retorna informações de diagnóstico adicionais (um único campo da estrutura de dados diagnósticos).|  
||[SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)|ISO 92|Retorna informações de diagnóstico adicionais (vários campos da estrutura de dados diagnósticos).|  
|Obtenção de informações sobre as tabelas do sistema da fonte de dados (funções de catálogo)|[SQLColumnPrivileges](../../../odbc/reference/syntax/sqlcolumnprivileges-function.md)<br /><br /> [SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md)|ODBCODBC<br /><br /> Grupo Aberto|Retorna uma lista de colunas e privilégios associados para uma ou mais tabelas.<br /><br /> Retorna a lista de nomes da coluna em tabelas especificadas.|  
||[SQLForeignKeys](../../../odbc/reference/syntax/sqlforeignkeys-function.md)|ODBCODBC|Retorna uma lista de nomes de coluna que compõem chaves estrangeiras, se existirem para uma tabela especificada.|  
||[SQLPrimaryKeys](../../../odbc/reference/syntax/sqlprimarykeys-function.md)|ODBCODBC|Retorna a lista de nomes de coluna que compõem a chave principal de uma tabela.|  
||[SQLProcedureColumns](../../../odbc/reference/syntax/sqlprocedurecolumns-function.md)|ODBCODBC|Retorna a lista de parâmetros de entrada e saída, bem como as colunas que compõem o conjunto de resultados para os procedimentos especificados.|  
||[SQLProcedures](../../../odbc/reference/syntax/sqlprocedures-function.md)|ODBCODBC|Retorna a lista de nomes de procedimento armazenados em uma fonte de dados específica.|  
||[SQLSpecialColumns](../../../odbc/reference/syntax/sqlspecialcolumns-function.md)|Grupo Aberto|Retorna informações sobre o conjunto ideal de colunas que identificam exclusivamente uma linha em uma tabela especificada ou as colunas que são atualizadas automaticamente quando qualquer valor na linha é atualizado por uma transação.|  
||[SQLStatistics](../../../odbc/reference/syntax/sqlstatistics-function.md)|ISO 92|Retorna estatísticas sobre uma única tabela e a lista de índices associados à tabela.|  
||[SQLTablePrivileges](../../../odbc/reference/syntax/sqltableprivileges-function.md)|ODBCODBC|Retorna uma lista de tabelas e os privilégios associados a cada tabela.|  
||[SQLTables](../../../odbc/reference/syntax/sqltables-function.md)|Grupo Aberto|Retorna a lista de nomes de tabela armazenados em uma fonte de dados específica.|  
|Terminando uma declaração|[SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md)|ISO 92|Encerra o processamento da declaração, descarta os resultados pendentes e, opcionalmente, libera todos os recursos associados à alça da declaração.|  
||[SQLCloseCursor](../../../odbc/reference/syntax/sqlclosecursor-function.md)|ISO 92|Fecha um cursor que foi aberto em uma alça de declaração.|  
||[SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|ISO 92|Cancela o processamento em uma declaração.|  
||[SQLCancelhandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md)|ODBCODBC|Cancela o processamento em uma declaração ou conexão.|  
||[SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)|ISO 92|Compromete ou reverte uma transação.|  
|Terminando uma conexão|[Sqldisconnect](../../../odbc/reference/syntax/sqldisconnect-function.md)<br /><br /> [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)|ISO 92<br /><br /> ISO 92|Encerra a conexão.<br /><br /> Libera um ambiente, conexão, declaração ou alça descritor.|
