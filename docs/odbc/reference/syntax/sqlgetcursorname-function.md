---
title: Função SQLGetCursorName | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d3ac65dc07897ddc789ee03b06b1bc1f71d37c3c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81285544"
---
# <a name="sqlgetcursorname-function"></a>Função SQLGetCursorName
**Conformidade**  
 Versão introduzida: conformidade de padrões do ODBC 1,0: ISO 92  
  
 **Resumo**  
 **SQLGetCursorName** retorna o nome do cursor associado a uma instrução especificada.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLGetCursorName(  
     SQLHSTMT        StatementHandle,  
     SQLCHAR *       CursorName,  
     SQLSMALLINT     BufferLength,  
     SQLSMALLINT *   NameLengthPtr);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 Entrada Identificador de instrução.  
  
 *Cursorname*  
 Der Ponteiro para um buffer no qual retornar o nome do cursor.  
  
 Se *cursorname* for nulo, *NameLengthPtr* ainda retornará o número total de caracteres (excluindo o caractere de terminação nula para dados de caractere) disponível para retornar no buffer apontado pelo *cursorname*.  
  
 *BufferLength*  
 Entrada Comprimento de \* *cursorname*, em caracteres. Se o valor em * \*cursorname* for uma cadeia de caracteres Unicode (ao chamar **SQLGetCursorNameW**), o argumento *BufferLength* deverá ser um número par.  
  
 *NameLengthPtr*  
 Der Ponteiro para memória na qual retornar o número total de caracteres (excluindo o caractere de terminação nula) disponível para retornar \*em *cursorname*. Se o número de caracteres disponíveis para retornar for maior ou igual a *BufferLength*, o nome do cursor em \* *cursorname* será truncado para *BufferLength* menos o comprimento de um caractere de terminação nula.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLGetCursorName** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido chamando **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_STMT e um *identificador* de *StatementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLGetCursorName** e explica cada um no contexto dessa função; a notação "(DM)" precede as descrições de sqlstates retornadas pelo Gerenciador de driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa específica do driver. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|01004|Dados de cadeia de caracteres, truncados à direita|O \* *cursorname* do buffer não era grande o suficiente para retornar o nome do cursor inteiro, portanto, o nome do cursor estava truncado. O comprimento do nome do cursor não truncado é retornado em **NameLengthPtr*. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia um SQLSTATE específico e para o qual nenhum SQLSTATE específico de implementação foi definido. A mensagem de erro retornada por **SQLGetDiagRec** no buffer * \*MessageText* descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar memória necessária para dar suporte à execução ou à conclusão da função.|  
|HY010|Erro de sequência de função|(DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado ao *StatementHandle*. Esta função assíncrona ainda estava em execução quando a função **SQLGetCursorName** foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**ou **SQLMoreResults** foi chamado para *StatementHandle* e retornou SQL_PARAM_DATA_AVAILABLE. Esta função foi chamada antes de os dados serem recuperados para todos os parâmetros transmitidos.<br /><br /> (DM) uma função de execução assíncrona foi chamada para o *StatementHandle* e ainda estava em execução quando essa função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**ou **SQLSetPos** foi chamado para o *StatementHandle* e retornou SQL_NEED_DATA. Esta função foi chamada antes de os dados serem enviados para todos os parâmetros de dados em execução ou colunas.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não puderam ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY015|Nenhum nome de cursor disponível|(DM) o driver era um driver ODBC 2 *. x* , não havia um cursor aberto na instrução e nenhum nome de cursor foi definido com **SQLSetCursorName**.|  
|HY090|Comprimento de cadeia de caracteres ou buffer inválido|(DM) o valor especificado no argumento *BufferLength* era menor que 0.|  
|HY117|A conexão foi suspensa devido a um estado de transação desconhecido. Somente funções de desconexão e somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tempo limite de conexão expirado|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|O driver não oferece suporte a essa função|(DM) o driver associado ao *StatementHandle* não oferece suporte à função.|  
  
## <a name="comments"></a>Comentários  
 Os nomes de cursor são usados somente em instruções UPDATE e DELETE posicionadas (por exemplo, **Update** _-Name de tabela_ ... **Em que Current of** _cursor-Name_). Para obter mais informações, consulte as [instruções UPDATE e DELETE posicionadas](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md). Se o aplicativo não chamar **SQLSetCursorName** para definir um nome de cursor, o driver gerará um nome. Esse nome começa com as letras SQL_CUR.  
  
> [!NOTE]
>  No ODBC 2 *. x*, quando não havia nenhum cursor aberto e nenhum nome foi definido por uma chamada para **SQLSetCursorName**, uma chamada para **SQLGetCursorName** retornou SQLSTATE HY015 (nenhum nome de cursor disponível). No ODBC 3 *. x*, isso não é mais verdadeiro; independentemente de quando **SQLGetCursorName** é chamado, o driver retorna o nome do cursor.  
  
 **SQLGetCursorName** retorna o nome de um cursor, independentemente de o nome ter sido ou não criado de forma explícita ou implícita. Um nome de cursor é gerado implicitamente se **SQLSetCursorName** não é chamado. **SQLSetCursorName** pode ser chamado para renomear um cursor em uma instrução desde que o cursor esteja em um estado alocado ou preparado.  
  
 Um nome de cursor que é definido explicitamente ou implicitamente permanece definido até que o *StatementHandle* ao qual ele está associado seja descartado, usando **SQLFreeHandle** com um *HandleType* de SQL_HANDLE_STMT.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Executando uma instrução SQL|[Função SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Executando uma instrução SQL preparada|[Função SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Preparando uma instrução para execução|[Função SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|  
|Definindo um nome de cursor|[Função SQLSetCursorName](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
