---
title: Função SQLRowCount | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cc2ab4b2e97b9e1a83e0b00404010195b08f0dc0
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47654910"
---
# <a name="sqlrowcount-function"></a>Função SQLRowCount
**Conformidade com**  
 Versão introduziu: Conformidade de padrões 1.0 ODBC: ISO 92  
  
 **Resumo**  
 **SQLRowCount** retorna o número de linhas afetadas por um **UPDATE**, **inserir**, ou **excluir** instrução; um SQL_ADD SQL_UPDATE_BY_BOOKMARK ou SQL _ A operação DELETE_BY_BOOKMARK na **SQLBulkOperations**; ou uma operação de SQL_UPDATE ou SQL_DELETE na **SQLSetPos**.  
  
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
 [Saída] Aponta para um buffer no qual retornar uma contagem de linhas. Para **atualização**, **inserir**, e **excluir** instruções para as operações SQL_ADD, SQL_UPDATE_BY_BOOKMARK e SQL_DELETE_BY_BOOKMARK no  **SQLBulkOperations**e para as operações SQL_UPDATE ou SQL_DELETE **SQLSetPos**, o valor retornado em **RowCountPtr* é o número de linhas afetadas pela solicitação ou -1 se o número de linhas afetadas não está disponível.  
  
 Quando **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, **SQLSetPos ou SQLMoreResults** é chamado, o SQL_DIAG_ROW_COUNT campo da estrutura de dados de diagnóstico é definido como a contagem de linhas e a contagem de linhas é armazenada em cache de uma forma dependente da implementação. **SQLRowCount** retorna o valor de contagem de linha em cache. O valor da contagem de linha em cache é válido até que o identificador de instrução é definido de volta para o estado preparado ou alocado, a instrução é executado novamente, ou **SQLCloseCursor** é chamado. Observe que, se uma função tiver sido chamada uma vez que o campo SQL_DIAG_ROW_COUNT foi definido, o valor retornado por **SQLRowCount** pode ser diferente do valor no campo SQL_DIAG_ROW_COUNT porque o campo SQL_DIAG_ROW_COUNT é redefinido como 0 por qualquer chamada de função.  
  
 Para outras instruções e funções, o driver pode definir o valor retornado em \* *RowCountPtr*. Por exemplo, algumas fontes de dados podem ser capazes de retornar o número de linhas retornadas por uma **selecionar** instrução ou uma função de catálogo antes de buscar as linhas.  
  
> [!NOTE]  
>  Muitas fontes de dados não podem retornar o número de linhas em um conjunto de resultados antes buscando-los; para interoperabilidade máxima, os aplicativos não devem confiar nesse comportamento.  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLRowCount** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtida chamando **SQLGetDiagRec** com um *HandleType* de SQL _ HANDLE_STMT e uma *manipular* dos *StatementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLRowCount** e explica cada uma no contexto dessa função; a notação "(DM)" precede as descrições das SQLSTATEs retornados pelo Gerenciador de Driver. O código de retorno associado com cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
|SQLSTATE|Erro|Description|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa de específicos do driver. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|HY000|Erro geral|Ocorreu um erro para o qual não houve nenhum SQLSTATE específico e para o qual não foi definida nenhuma SQLSTATE específicos de implementação. A mensagem de erro retornada por **SQLGetDiagRec** na  *\*MessageText* buffer descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar a memória necessária para dar suporte à execução ou a conclusão da função.|  
|HY010|Erro de sequência de função|(DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado a *StatementHandle*. Essa função assíncrona ainda estava em execução quando o **SQLRowCount** função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, ou **SQLMoreResults** foi chamado para o *StatementHandle* e retornado SQL_PARAM_DATA_ DISPONÍVEL. Essa função foi chamada antes de dados foram recuperados para todos os parâmetros transmitidos.<br /><br /> (DM), a função foi chamada antes de chamar **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, ou **SQLSetPos** para o  *StatementHandle*.<br /><br /> (DM) uma função de execução assíncrona foi chamada para o *StatementHandle* e ainda estava em execução quando essa função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, ou **SQLSetPos** foi chamado para o  *StatementHandle* e retornados de SQL_NEED_DATA. Essa função foi chamada antes de dados foi enviados para todos os parâmetros de dados em execução ou colunas.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacente não pôde ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY117|Conexão está suspenso devido ao estado de transação desconhecida. Somente se desconectar e funções de somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tempo limite da Conexão expirado|O período de tempo limite de conexão expirado antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não oferece suporte a essa função|O driver em (DM) associado a *StatementHandle* não suporta a função.|  
  
## <a name="comments"></a>Comentários  
 Se a última instrução SQL executada no identificador da instrução não era um **atualização**, **inserir**, ou **excluir** declaração ou se o *operação* argumento na chamada anterior a **SQLBulkOperations** não era SQL_ADD, SQL_UPDATE_BY_BOOKMARK ou SQL_DELETE_BY_BOOKMARK, ou se o *operação* argumento na chamada anterior para  **SQLSetPos** não era SQL_UPDATE ou SQL_DELETE, o valor de **RowCountPtr* é definido pelo driver. Para obter mais informações, consulte [determinando o número de linhas afetadas](../../../odbc/reference/develop-app/determining-the-number-of-affected-rows.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Executar uma instrução SQL|[Função SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Executar uma instrução SQL preparada|[Função SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
