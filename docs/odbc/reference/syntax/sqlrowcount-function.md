---
title: Função SQLrowcount | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLRowCount
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLRowCount
helpviewer_keywords:
- SQLRowCount function [ODBC]
ms.assetid: 61e00a8a-9b3b-45b9-b397-7fe818822416
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2cbca03e7c3e381b803196a1bf7bb227ebeea03b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81293366"
---
# <a name="sqlrowcount-function"></a>Função SQLRowCount
**Conformidade**  
 Versão introduzida: ODBC 1.0 Standards Compliance: ISO 92  
  
 **Resumo**  
 **O SQLRowCount** retorna o número de linhas afetadas por uma instrução **UPDATE,** **INSERT**ou **DELETE;** uma operação SQL_ADD, SQL_UPDATE_BY_BOOKMARK ou SQL_DELETE_BY_BOOKMARK em **SQLBulkOperations;** ou uma operação SQL_UPDATE ou SQL_DELETE em **SQLSetPos**.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLRowCount(  
      SQLHSTMT   StatementHandle,  
      SQLLEN *   RowCountPtr);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Alça de declaração.  
  
 *RowCountPtr*  
 [Saída] Aponta para um buffer no qual retornar uma contagem de linhas. Para **as**instruções UPDATE , **INSERT**e **DELETE,** para as operações de SQL_ADD, SQL_UPDATE_BY_BOOKMARK e SQL_DELETE_BY_BOOKMARK em **SQLBulkOperations,** e para as operações de SQL_UPDATE ou SQL_DELETE em **SQLSetPos,** o valor retornado em **RowCountPtr* é o número de linhas afetadas pela solicitação ou -1 se o número de linhas afetadas não estiver disponível.  
  
 Quando **sQLExecute,** **SQLExecDirect,** **SQLBulkOperations,** **SQLSetPos ou SQLMoreResults** são chamados, o campo SQL_DIAG_ROW_COUNT da estrutura de dados de diagnóstico é definido para a contagem de linhas e a contagem de linhas é armazenada em cache de forma dependente da implementação. **SQLRowCount** retorna o valor da contagem de linhas armazenada em cache. O valor da contagem de linhas em cache é válido até que a alça da declaração seja definida para o estado preparado ou alocado, a declaração é reexecutada ou **o SQLCloseCursor** é chamado. Observe que se uma função foi chamada desde que o campo SQL_DIAG_ROW_COUNT foi definido, o valor retornado pelo **SQLRowCount** pode ser diferente do valor no campo SQL_DIAG_ROW_COUNT porque o campo SQL_DIAG_ROW_COUNT é redefinido para 0 por qualquer chamada de função.  
  
 Para outras instruções e funções, o \*driver pode definir o valor retornado em *RowCountPtr*. Por exemplo, algumas fontes de dados podem ser capazes de retornar o número de linhas retornadas por uma declaração **SELECT** ou uma função de catálogo antes de buscar as linhas.  
  
> [!NOTE]  
>  Muitas fontes de dados não podem retornar o número de linhas em um conjunto de resultados antes de buscá-las; para a interoperabilidade máxima, as aplicações não devem confiar nesse comportamento.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **o SQLRowCount** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido ligando para **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_STMT e uma *alça* de *statementHandle*. A tabela a seguir lista os valores SQLSTATE comumente retornados pelo **SQLRowCount** e explica cada um no contexto desta função; a notação "(DM)" precede as descrições de SQLSTATEs devolvidas pelo Driver Manager. O código de devolução associado a cada valor SQLSTATE é SQL_ERROR, a menos que seja observado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informacional específica do motorista. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia SQLSTATE específico e para o qual não foi definido sqlSTATE específico para a implementação. A mensagem de erro retornada pelo **SQLGetDiagRec** no * \** buffer MessageText descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não conseguiu alocar a memória necessária para suportar a execução ou a conclusão da função.|  
|HY010|Erro de seqüência de função|(DM) Uma função de execução assíncrona foi chamada para o cabo de conexão associado ao *StatementHandle*. Esta função assíncrona ainda estava sendo executada quando a função **SQLRowCount** foi chamada.<br /><br /> (DM) **SQLExecute,** **SQLExecDirect**ou **SQLMoreResults** foram chamados para o *StatementHandle* e retornaram SQL_PARAM_DATA_AVAILABLE. Esta função foi chamada antes de os dados serem recuperados para todos os parâmetros transmitidos.<br /><br /> (DM) A função foi chamada antes de chamar **SQLExecute,** **SQLExecDirect,** **SQLBulkOperations**ou **SQLSetPos** para o *StatementHandle*.<br /><br /> (DM) Uma função de execução assíncrona foi chamada para o *StatementHandle* e ainda estava sendo executada quando esta função foi chamada.<br /><br /> (DM) **SQLExecute,** **SQLExecDirect,** **SQLBulkOperations**ou **SQLSetPos** foram chamados para o *StatementHandle* e retornaram SQL_NEED_DATA. Essa função foi chamada antes de os dados serem enviados para todos os parâmetros ou colunas de execução de dados.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não podiam ser acessados, possivelmente devido às baixas condições de memória.|  
|HY117|A conexão está suspensa devido ao estado de transação desconhecido. Somente funções desconectadas e somente leitura são permitidas.|(DM) Para obter mais informações sobre o estado suspenso, consulte [a função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tempo de tempo de conexão expirado|O período de tempo de tempo de conexão expirou antes que a fonte de dados respondesse à solicitação. O período de tempo de tempo de conexão é definido através **de SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não suporta esta função|(DM) O driver associado ao *StatementHandle* não suporta a função.|  
  
## <a name="comments"></a>Comentários  
 Se a última instrução SQL executada no cabo de instrução não fosse uma instrução **UPDATE**, **INSERT**ou **DELETE** ou se o argumento *operação* na chamada anterior à **SQLBulkOperations** não estivesse SQL_ADD, SQL_UPDATE_BY_BOOKMARK ou SQL_DELETE_BY_BOOKMARK, ou se o argumento *operação* na chamada anterior ao **SQLSetPos** não fosse SQL_UPDATE ou SQL_DELETE, o valor de **RowCountPtr* é definido pelo driver. Para obter mais informações, consulte [Determinar o número de linhas afetadas](../../../odbc/reference/develop-app/determining-the-number-of-affected-rows.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Executando uma declaração SQL|[Função SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Executando uma declaração SQL preparada|[Função SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API oDBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
