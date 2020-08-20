---
description: Função SQLRowCount
title: Função SQLRowCount | Microsoft Docs
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
ms.openlocfilehash: 666351fcd4758170baaf62fbd80cd45a554ab92a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499589"
---
# <a name="sqlrowcount-function"></a>Função SQLRowCount
**Conformidade**  
 Versão introduzida: conformidade de padrões do ODBC 1,0: ISO 92  
  
 **Resumo**  
 **SQLRowCount** retorna o número de linhas afetadas por uma instrução **Update**, **Insert**ou **delete** ; uma operação SQL_ADD, SQL_UPDATE_BY_BOOKMARK ou SQL_DELETE_BY_BOOKMARK em **SQLBulkOperations**; ou uma operação SQL_UPDATE ou SQL_DELETE em **SQLSetPos**.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLRowCount(  
      SQLHSTMT   StatementHandle,  
      SQLLEN *   RowCountPtr);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 Entrada Identificador de instrução.  
  
 *RowCountPtr*  
 Der Aponta para um buffer no qual retornar uma contagem de linhas. Para as instruções **Update**, **Insert**e **DELETE** , para as operações SQL_ADD, SQL_UPDATE_BY_BOOKMARK e SQL_DELETE_BY_BOOKMARK em **SQLBulkOperations**e para as operações SQL_UPDATE ou SQL_DELETE em **SQLSetPos**, o valor retornado em **RowCountPtr* será o número de linhas afetadas pela solicitação ou-1 se o número de linhas afetadas não estiver disponível.  
  
 Quando **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, **SQLSetPos ou SQLMoreResults** é chamado, o campo SQL_DIAG_ROW_COUNT da estrutura de dados de diagnóstico é definido como a contagem de linhas e a contagem de linhas é armazenada em cache de forma dependente da implementação. **SQLRowCount** retorna o valor de contagem de linhas em cache. O valor de contagem de linhas em cache é válido até que o identificador de instrução seja definido de volta para o estado preparado ou alocado, a instrução é reexecutada ou **SQLCloseCursor** é chamado. Observe que, se uma função for chamada desde que o campo SQL_DIAG_ROW_COUNT foi definido, o valor retornado por **SQLRowCount** poderá ser diferente do valor no campo SQL_DIAG_ROW_COUNT porque o campo SQL_DIAG_ROW_COUNT é redefinido como 0 por qualquer chamada de função.  
  
 Para outras instruções e funções, o driver pode definir o valor retornado em \* *RowCountPtr*. Por exemplo, algumas fontes de dados podem ser capazes de retornar o número de linhas retornadas por uma instrução **Select** ou uma função de catálogo antes de buscar as linhas.  
  
> [!NOTE]  
>  Muitas fontes de dados não podem retornar o número de linhas em um conjunto de resultados antes de obtê-las; para obter a interoperabilidade máxima, os aplicativos não devem depender desse comportamento.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **SQLRowCount** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido chamando **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_STMT e um *identificador* de *StatementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLRowCount** e explica cada um no contexto dessa função; a notação "(DM)" precede as descrições de sqlstates retornadas pelo Gerenciador de driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa específica do driver. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia um SQLSTATE específico e para o qual nenhum SQLSTATE específico de implementação foi definido. A mensagem de erro retornada por **SQLGetDiagRec** no buffer * \* MessageText* descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar memória necessária para dar suporte à execução ou à conclusão da função.|  
|HY010|Erro de sequência de função|(DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado ao *StatementHandle*. Esta função assíncrona ainda estava em execução quando a função **SQLRowCount** foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**ou **SQLMoreResults** foi chamado para *StatementHandle* e retornou SQL_PARAM_DATA_AVAILABLE. Esta função foi chamada antes de os dados serem recuperados para todos os parâmetros transmitidos.<br /><br /> (DM) a função foi chamada antes de chamar **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**ou **SQLSetPos** para *StatementHandle*.<br /><br /> (DM) uma função de execução assíncrona foi chamada para o *StatementHandle* e ainda estava em execução quando essa função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**ou **SQLSetPos** foi chamado para o *StatementHandle* e retornou SQL_NEED_DATA. Esta função foi chamada antes de os dados serem enviados para todos os parâmetros de dados em execução ou colunas.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não puderam ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY117|A conexão foi suspensa devido a um estado de transação desconhecido. Somente funções de desconexão e somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tempo limite de conexão expirado|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|O driver não oferece suporte a essa função|(DM) o driver associado ao *StatementHandle* não oferece suporte à função.|  
  
## <a name="comments"></a>Comentários  
 Se a última instrução SQL executada no identificador de instrução não for uma instrução **Update**, **Insert**ou **delete** ou se o argumento *Operation* na chamada anterior para **SQLBulkOperations** não tiver sido SQL_ADD, SQL_UPDATE_BY_BOOKMARK ou SQL_DELETE_BY_BOOKMARK, ou se o argumento *Operation* na chamada anterior para **SQLSetPos** não fosse SQL_UPDATE ou SQL_DELETE, o valor de **RowCountPtr* será definido pelo driver. Para obter mais informações, consulte [determinando o número de linhas afetadas](../../../odbc/reference/develop-app/determining-the-number-of-affected-rows.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Executando uma instrução SQL|[Função SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Executando uma instrução SQL preparada|[Função SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
