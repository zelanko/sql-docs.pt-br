---
title: Função SQLRowCount | Microsoft Docs
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
apiname:
- SQLRowCount
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLRowCount
helpviewer_keywords:
- SQLRowCount function [ODBC]
ms.assetid: 61e00a8a-9b3b-45b9-b397-7fe818822416
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 04a4e5061a80fec51361e82c57102df8e3fa34c8
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="sqlrowcount-function"></a>Função SQLRowCount
**Conformidade**  
 Versão introduzidas: Conformidade de padrões 1.0 ODBC: 92 ISO  
  
 **Resumo**  
 **SQLRowCount** retorna o número de linhas afetadas por uma **atualização**, **inserir**, ou **excluir** instrução; um SQL_ADD SQL_UPDATE_BY_BOOKMARK ou SQL _ Operação de DELETE_BY_BOOKMARK em **SQLBulkOperations**; ou uma operação SQL_UPDATE ou SQL_DELETE em **SQLSetPos**.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SQLRETURN SQLRowCount(  
      SQLHSTMT   StatementHandle,  
      SQLLEN *   RowCountPtr);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Identificador de instrução.  
  
 *RowCountPtr*  
 [Saída] Aponta para um buffer no qual retornar uma contagem de linhas. Para **atualização**, **inserir**, e **excluir** instruções para as operações SQL_ADD, SQL_UPDATE_BY_BOOKMARK e SQL_DELETE_BY_BOOKMARK no  **SQLBulkOperations**e para as operações SQL_UPDATE ou SQL_DELETE **SQLSetPos**, o valor retornado em **RowCountPtr* é o número de linhas afetadas pelo solicitação ou -1 se o número de linhas afetadas não está disponível.  
  
 Quando **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, **SQLSetPos ou SQLMoreResults** é chamado, o SQL_DIAG_ROW_COUNT campo da estrutura de dados de diagnóstico é definido como a contagem de linhas e a contagem de linhas é armazenado em cache de forma dependente de implementação. **SQLRowCount** retorna o valor de contagem de linha em cache. O valor de contagem de linha em cache é válido até que o identificador de instrução é redefinido para o estado preparado ou alocado, a instrução for executado novamente, ou **SQLCloseCursor** é chamado. Observe que, se uma função foi chamada porque o campo SQL_DIAG_ROW_COUNT foi definido, o valor retornado por **SQLRowCount** pode ser diferente do valor no campo SQL_DIAG_ROW_COUNT porque o campo SQL_DIAG_ROW_COUNT é redefinido para 0 por qualquer chamada de função.  
  
 Para outras instruções e funções, o driver pode definir o valor retornado em \* *RowCountPtr*. Por exemplo, algumas fontes de dados poderá retornar o número de linhas retornadas por uma **selecione** instrução ou uma função de catálogo antes de buscar as linhas.  
  
> [!NOTE]  
>  Várias fontes de dados não podem retornar o número de linhas em um conjunto de resultados antes buscando-los; para interoperabilidade máxima, aplicativos não devem depender esse comportamento.  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>diagnóstico  
 Quando **SQLRowCount** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtida chamando **SQLGetDiagRec** com um *HandleType* de SQL _ HANDLE_STMT e um *tratar* de *StatementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLRowCount** e explica cada uma no contexto dessa função; a notação "(DM)" precede as descrições de SQLSTATEs retornados pelo Gerenciador de Driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado em contrário.  
  
|SQLSTATE|Erro|Description|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem de informação específica do driver. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|HY000|Erro geral|Ocorreu um erro para o qual não houve nenhuma SQLSTATE específico e para o qual nenhuma SQLSTATE específicos de implementação foi definida. A mensagem de erro retornada pelo **SQLGetDiagRec** no  *\*MessageText* buffer descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar a memória necessária para dar suporte a execução ou a conclusão da função.|  
|HY010|Erro de sequência de função|(DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado a *StatementHandle*. Essa função assíncrona ainda estava em execução quando o **SQLRowCount** função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, ou **SQLMoreResults** foi chamado para o *StatementHandle* e retornado SQL_PARAM_DATA_ DISPONÍVEL. Essa função foi chamada antes de recuperação para todos os parâmetros de fluxo de dados.<br /><br /> (DM), a função foi chamada antes de chamar **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, ou **SQLSetPos** para o  *StatementHandle*.<br /><br /> (DM) uma função de execução assíncrona foi chamada para o *StatementHandle* e ainda estava em execução quando esta função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, ou **SQLSetPos** foi chamado para o  *StatementHandle* e retorna SQL_NEED_DATA. Essa função foi chamada antes de dados foi enviados para todas as colunas ou parâmetros de dados em execução.|  
|HY013|Erro de gerenciamento de memória|Não foi possível processar a chamada de função porque os objetos de memória subjacente não podem ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY117|Conexão está suspenso devido ao estado de transação desconhecido. Somente Desconecte e funções de somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tempo limite de Conexão expirou|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não dá suporte a esta função|O driver em (DM) associado a *StatementHandle* não oferece suporte para a função.|  
  
## <a name="comments"></a>Comentários  
 Se a última instrução SQL executada no identificador da instrução não era um **atualização**, **inserir**, ou **excluir** instrução ou se o *operação* argumentos na chamada anterior para **SQLBulkOperations** não era SQL_ADD, SQL_UPDATE_BY_BOOKMARK ou SQL_DELETE_BY_BOOKMARK, ou se o *operação* argumentos na chamada anterior para  **SQLSetPos** não era SQL_UPDATE ou SQL_DELETE, o valor de **RowCountPtr* é definido pelo driver. Para obter mais informações, consulte [determinando o número de linhas afetadas](../../../odbc/reference/develop-app/determining-the-number-of-affected-rows.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Executar uma instrução SQL|[Função SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Executar uma instrução preparada do SQL|[Função SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
