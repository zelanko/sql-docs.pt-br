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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a1316ad29a31872d149201f31d60ede14a8a9051
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47855074"
---
# <a name="sqlgetcursorname-function"></a>Função SQLGetCursorName
**Conformidade com**  
 Versão introduziu: Conformidade de padrões 1.0 ODBC: ISO 92  
  
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
  
 Se *CursorName* for NULL, *NameLengthPtr* ainda retornará o número total de caracteres (exceto o caractere nulo de terminação para dados de caracteres) disponíveis para retornar no buffer apontado por *CursorName*.  
  
 *BufferLength*  
 [Entrada] Comprimento da \* *CursorName*, em caracteres. Se o valor em  *\*CursorName* é uma cadeia de caracteres Unicode (ao chamar **SQLGetCursorNameW**), o *BufferLength* argumento deve ser um número par.  
  
 *NameLengthPtr*  
 [Saída] Ponteiro de memória no qual retornar o número total de caracteres (exceto o caractere nulo de terminação) disponíveis para retornar na \* *CursorName*. Se o número de caracteres disponíveis para retornar for maior que ou igual a *BufferLength*, o nome do cursor na \* *CursorName* será truncado para *BufferLength*menos o comprimento de um caractere nulo de terminação.  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLGetCursorName** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido chamando **SQLGetDiagRec** com um *HandleType*sql_handle_stmt e uma *manipular* dos *StatementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLGetCursorName** e explica cada uma no contexto dessa função; a notação "(DM)" precede as descrições das SQLSTATEs retornados pelo Gerenciador de Driver. O código de retorno associado com cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
|SQLSTATE|Erro|Description|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa de específicos do driver. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|01004|Dados de cadeia de caracteres truncados à direita|O buffer \* *CursorName* não era grande o suficiente para retornar o nome de cursor inteiro, portanto, o nome de cursor foi truncado. O comprimento do nome completo do cursor é retornado no **NameLengthPtr*. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|HY000|Erro geral|Ocorreu um erro para o qual não houve nenhum SQLSTATE específico e para o qual não foi definida nenhuma SQLSTATE específicos de implementação. A mensagem de erro retornada por **SQLGetDiagRec** na  *\*MessageText* buffer descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar a memória necessária para dar suporte à execução ou a conclusão da função.|  
|HY010|Erro de sequência de função|(DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado a *StatementHandle*. Essa função assíncrona ainda estava em execução quando o **SQLGetCursorName** função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, ou **SQLMoreResults** foi chamado para o *StatementHandle* e retornado SQL_PARAM_DATA_ DISPONÍVEL. Essa função foi chamada antes de dados foram recuperados para todos os parâmetros transmitidos.<br /><br /> (DM) uma função de execução assíncrona foi chamada para o *StatementHandle* e ainda estava em execução quando essa função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, ou **SQLSetPos** foi chamado para o  *StatementHandle* e retornados de SQL_NEED_DATA. Essa função foi chamada antes de dados foi enviados para todos os parâmetros de dados em execução ou colunas.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacente não pôde ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY015|Nenhum nome de cursor disponível|(DM) o driver foi um ODBC 2 *. x* driver, não havia nenhum cursor aberto na instrução, e nenhum nome de cursor foi definido com **SQLSetCursorName**.|  
|HY090|Comprimento de buffer ou cadeia de caracteres inválido|(DM) o valor especificado no argumento *BufferLength* foi menor que 0.|  
|HY117|Conexão está suspenso devido ao estado de transação desconhecida. Somente se desconectar e funções de somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tempo limite da Conexão expirado|O período de tempo limite de conexão expirado antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não oferece suporte a essa função|O driver em (DM) associado a *StatementHandle* não suporta a função.|  
  
## <a name="comments"></a>Comentários  
 Nomes de cursor são usados apenas na atualização posicionadas e instruções delete (por exemplo, **atualize** *nome da tabela* ... **WHERE CURRENT OF** *nome de cursor*). Para obter mais informações, consulte [posicionado instruções Update e excluir](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md). Se o aplicativo não chama **SQLSetCursorName** para definir um nome de cursor, o driver gerará um nome. Esse nome começa com as letras SQL_CUR.  
  
> [!NOTE]  
>  No ODBC 2 *. x*, quando não havia nenhum cursor aberto e nenhum nome foi definido por uma chamada para **SQLSetCursorName**, uma chamada para **SQLGetCursorName** retornado SQLSTATE HY015 (nenhum nome de cursor disponível). Em ODBC 3 *. x*, isso não é mais verdadeiro, independentemente de quando **SQLGetCursorName** é chamado, o driver retorna o nome do cursor.  
  
 **SQLGetCursorName** retorna o nome de um cursor ou não o nome foi criado explicitamente ou implicitamente. Um nome de cursor implicitamente será gerado se **SQLSetCursorName** não é chamado. **SQLSetCursorName** pode ser chamado para renomear um cursor em uma instrução, contanto que o cursor estiver em um estado preparado ou alocado.  
  
 Um nome de cursor que é definido explicitamente ou implicitamente permanece definido até que o *StatementHandle* ao qual ele está associado é descartado, usando **SQLFreeHandle** com um *HandleType* sql_handle_stmt.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Executar uma instrução SQL|[Função SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Executar uma instrução SQL preparada|[Função SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Como preparar uma instrução para execução|[Função SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|  
|Configuração de um nome de cursor|[Função SQLSetCursorName](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
