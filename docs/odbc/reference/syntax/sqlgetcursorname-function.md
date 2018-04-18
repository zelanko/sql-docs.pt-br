---
title: Função SQLGetCursorName | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
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
- SQLGetCursorName
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetCursorName
helpviewer_keywords:
- SQLGetCursorName function [ODBC]
ms.assetid: e6e92199-7bb6-447c-8987-049a4c6ce05d
caps.latest.revision: 24
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 28220550d868976aded368a88bdc8268cfad490c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="sqlgetcursorname-function"></a>Função SQLGetCursorName
**Conformidade**  
 Versão introduzidas: Conformidade de padrões 1.0 ODBC: 92 ISO  
  
 **Resumo**  
 **SQLGetCursorName** retorna o nome de cursor associado a uma instrução especificada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SQLRETURN SQLGetCursorName(  
     SQLHSTMT        StatementHandle,  
     SQLCHAR *       CursorName,  
     SQLSMALLINT     BufferLength,  
     SQLSMALLINT *   NameLengthPtr);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Identificador de instrução.  
  
 *cursorName*  
 [Saída] Ponteiro para um buffer no qual retornar o nome do cursor.  
  
 Se *CursorName* for NULL, *NameLengthPtr* ainda retornará o número total de caracteres (excluindo o caractere null de terminação para dados de caractere) disponíveis para retornar o buffer apontado pelo *CursorName*.  
  
 *BufferLength*  
 [Entrada] Comprimento de \* *CursorName*, em caracteres. Se o valor em  *\*CursorName* é uma cadeia de caracteres Unicode (ao chamar **SQLGetCursorNameW**), o *BufferLength* argumento deve ser um número par.  
  
 *NameLengthPtr*  
 [Saída] Ponteiro de memória no qual retornar o número total de caracteres (excluindo o caractere null de terminação) disponíveis para retornar em \* *CursorName*. Se o número de caracteres disponíveis para retornar for maior que ou igual a *BufferLength*, o nome do cursor no \* *CursorName* será truncado para *BufferLength*menos o comprimento de um caractere null de terminação.  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>diagnóstico  
 Quando **SQLGetCursorName** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido chamando **SQLGetDiagRec** com um *HandleType*sql_handle_stmt e um *tratar* de *StatementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLGetCursorName** e explica cada uma no contexto dessa função; a notação "(DM)" precede as descrições de SQLSTATEs retornados pelo Gerenciador de Driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado em contrário.  
  
|SQLSTATE|Erro|Description|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem de informação específica do driver. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|01004|Dados de cadeia de caracteres truncados à direita|O buffer \* *CursorName* não era grande o suficiente para retornar o nome de cursor inteiro, e o nome de cursor foi truncado. O comprimento do nome completo do cursor é retornado em **NameLengthPtr*. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|HY000|Erro geral|Ocorreu um erro para o qual não houve nenhuma SQLSTATE específico e para o qual nenhuma SQLSTATE específicos de implementação foi definida. A mensagem de erro retornada pelo **SQLGetDiagRec** no  *\*MessageText* buffer descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar a memória necessária para dar suporte a execução ou a conclusão da função.|  
|HY010|Erro de sequência de função|(DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado a *StatementHandle*. Essa função assíncrona ainda estava em execução quando o **SQLGetCursorName** função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, ou **SQLMoreResults** foi chamado para o *StatementHandle* e retornado SQL_PARAM_DATA_ DISPONÍVEL. Essa função foi chamada antes de recuperação para todos os parâmetros de fluxo de dados.<br /><br /> (DM) uma função de execução assíncrona foi chamada para o *StatementHandle* e ainda estava em execução quando esta função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, ou **SQLSetPos** foi chamado para o  *StatementHandle* e retorna SQL_NEED_DATA. Essa função foi chamada antes de dados foi enviados para todas as colunas ou parâmetros de dados em execução.|  
|HY013|Erro de gerenciamento de memória|Não foi possível processar a chamada de função porque os objetos de memória subjacente não podem ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY015|Nenhum nome de cursor disponível|(DM) o driver foi um ODBC 2*. x* driver, não havia nenhum cursor aberto na instrução, e nenhum nome de cursor foi definido com **SQLSetCursorName**.|  
|HY090|Comprimento de buffer ou cadeia de caracteres inválido|(DM) o valor especificado no argumento *BufferLength* era menor do que 0.|  
|HY117|Conexão está suspenso devido ao estado de transação desconhecido. Somente Desconecte e funções de somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tempo limite de Conexão expirou|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não dá suporte a esta função|O driver em (DM) associado a *StatementHandle* não oferece suporte para a função.|  
  
## <a name="comments"></a>Comentários  
 Nomes de cursor são usados somente em atualização posicionada e instruções delete (por exemplo, **atualizar** *nome de tabela* ... **WHERE CURRENT OF** *nome de cursor*). Para obter mais informações, consulte [posicionado instruções Update e excluir](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md). Se o aplicativo não chamar **SQLSetCursorName** para definir um nome de cursor, o driver gerará um nome. Esse nome começa com as letras SQL_CUR.  
  
> [!NOTE]  
>  No ODBC 2*. x*, quando não havia nenhum cursor aberto e nenhum nome foi definido por uma chamada para **SQLSetCursorName**, uma chamada para **SQLGetCursorName** retornado SQLSTATE HY015 (nenhum nome de cursor disponível). Em ODBC 3*. x*, isso não é mais true; independentemente de quando **SQLGetCursorName** é chamado, o driver retorna o nome do cursor.  
  
 **SQLGetCursorName** retorna o nome de um cursor ou não o nome foi criado implicitamente ou explicitamente. Um nome de cursor implicitamente será gerado se **SQLSetCursorName** não é chamado. **SQLSetCursorName** pode ser chamado para renomear um cursor em uma instrução, enquanto o cursor estiver em um estado preparado ou alocado.  
  
 Um nome de cursor que é definido explicitamente ou implicitamente permanece definido até que o *StatementHandle* à qual ele está associado é descartado, usando **SQLFreeHandle** com um *HandleType* sql_handle_stmt.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Executar uma instrução SQL|[Função SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Executar uma instrução preparada do SQL|[Função SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Preparar uma instrução para execução|[Função SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|  
|Definir um nome de cursor|[Função SQLSetCursorName](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Referência de API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
