---
description: Função SQLSetCursorName
title: Função SQLSetCursorName | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetCursorName
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSetCursorName
helpviewer_keywords:
- SQLSetCursorName function [ODBC]
ms.assetid: 4e055946-12d4-4589-9891-41617a50f34e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1a7deee4ecb37225260f011d4944e992f16d94e1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499485"
---
# <a name="sqlsetcursorname-function"></a>Função SQLSetCursorName
**Conformidade**  
 Versão introduzida: conformidade de padrões do ODBC 1,0: ISO 92  
  
 **Resumo**  
 **SQLSetCursorName** associa um nome de cursor a uma instrução ativa. Se um aplicativo não chamar **SQLSetCursorName**, o driver gerará nomes de cursor conforme necessário para o processamento da instrução SQL.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLSetCursorName(  
     SQLHSTMT      StatementHandle,  
     SQLCHAR *     CursorName,  
     SQLSMALLINT   NameLength);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 Entrada Identificador de instrução.  
  
 *Cursorname*  
 Entrada Nome do cursor. Para um processamento eficiente, o nome do cursor não deve incluir espaços à esquerda ou à direita no nome do cursor e, se o nome do cursor incluir um identificador delimitado, o delimitador deverá ser posicionado como o primeiro caractere no nome do cursor.  
  
 *NameLength*  
 Entrada Comprimento em caracteres de **cursorname*.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **SQLSetCursorName** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido chamando **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_STMT e um *identificador* de *StatementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLSetCursorName** e explica cada um no contexto dessa função; a notação "(DM)" precede as descrições de sqlstates retornadas pelo Gerenciador de driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa específica do driver. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|01004|Dados de cadeia de caracteres, truncados à direita|O nome do cursor excedeu o limite máximo, portanto, somente o número máximo permitido de caracteres foi usado.|  
|24.000|Estado de cursor inválido|A instrução correspondente a *StatementHandle* já estava em um estado executado ou posicionado no cursor.|  
|34000|Nome de cursor inválido|O nome do cursor especificado em **cursorname* era inválido porque excedeu o comprimento máximo definido pelo driver ou começou com "SQLCUR" ou "SQL_CUR".|  
|3C000|Nome de cursor duplicado|O nome do cursor especificado em **cursorname* já existe.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia um SQLSTATE específico e para o qual nenhum SQLSTATE específico de implementação foi definido. A mensagem de erro retornada por **SQLGetDiagRec** no buffer * \* MessageText* descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar memória necessária para dar suporte à execução ou à conclusão da função.|  
|HY009|Uso inválido de ponteiro nulo|(DM) o argumento *cursorname* era um ponteiro nulo.|  
|HY010|Erro de sequência de função|(DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado ao *StatementHandle*. Esta função aynchronous ainda estava em execução quando a função **SQLSetCursorName** foi chamada.<br /><br /> (DM) uma função de execução assíncrona foi chamada para o *StatementHandle* e ainda estava em execução quando essa função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**ou **SQLSetPos** foi chamado para o *StatementHandle* e retornou SQL_NEED_DATA. Esta função foi chamada antes de os dados serem enviados para todos os parâmetros de dados em execução ou colunas.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não puderam ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY090|Comprimento de cadeia de caracteres ou buffer inválido|(DM) o argumento *NameLength* era menor que 0, mas não é igual a SQL_NTS.|  
|HY117|A conexão foi suspensa devido a um estado de transação desconhecido. Somente funções de desconexão e somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tempo limite de conexão expirado|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|O driver não oferece suporte a essa função|(DM) o driver associado ao *StatementHandle* não oferece suporte à função.|  
  
## <a name="comments"></a>Comentários  
 Os nomes de cursor são usados somente em instruções UPDATE e DELETE posicionadas (por exemplo, **Update** _-Name de tabela_ ... **Em que Current of** _cursor-Name_). Para obter mais informações, consulte as [instruções UPDATE e DELETE posicionadas](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md). Se o aplicativo não chamar **SQLSetCursorName** para definir um nome de cursor, na execução de uma instrução de consulta, o driver gerará um nome que começa com as letras SQL_CUR e não excederá 18 caracteres de comprimento.  
  
 Todos os nomes de cursor dentro da conexão devem ser exclusivos. O comprimento máximo de um nome de cursor é definido pelo driver. Para obter a interoperabilidade máxima, é recomendável que os aplicativos limitem os nomes de cursor a até 18 caracteres. No ODBC 3 *. x*, se um nome de cursor for um identificador entre aspas, ele será tratado de forma sensível a maiúsculas e minúsculas e poderá conter caracteres que a sintaxe do SQL não permitiria ou trataria especialmente, como espaços em branco ou palavras-chave reservadas. Se um nome de cursor precisar ser tratado de forma sensível a maiúsculas e minúsculas, ele deverá ser passado como um identificador entre aspas.  
  
 Um nome de cursor que é definido explicitamente ou implicitamente permanece definido até que a instrução com a qual ele está associado seja descartada, usando **SQLFreeHandle**. **SQLSetCursorName** pode ser chamado para renomear um cursor em uma instrução desde que o cursor esteja em um estado alocado ou preparado.  
  
## <a name="code-example"></a>Exemplo de código  
 No exemplo a seguir, um aplicativo usa **SQLSetCursorName** para definir um nome de cursor para uma instrução. Em seguida, ele usa essa instrução para recuperar os resultados da tabela CUSTOMers. Por fim, ele executa uma atualização posicionada para alterar o número de telefone de João Silva. Observe que o aplicativo usa identificadores de instrução diferentes para as instruções **Select** e **Update** .  
  
 Para obter outro exemplo de código, consulte [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
```cpp  
#define NAME_LEN 50  
#define PHONE_LEN 10  
  
SQLHSTMT     hstmtSelect,  
SQLHSTMT     hstmtUpdate;  
SQLRETURN    retcode;  
SQLHDBC      hdbc;  
SQLCHAR      szName[NAME_LEN], szPhone[PHONE_LEN];  
SQLINTEGER   cbName, cbPhone;  
  
/* Allocate the statements and set the cursor name. */  
  
SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmtSelect);  
SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmtUpdate);  
SQLSetCursorName(hstmtSelect, "C1", SQL_NTS);  
  
/* SELECT the result set and bind its columns to local buffers. */  
  
SQLExecDirect(hstmtSelect,  
      "SELECT NAME, PHONE FROM CUSTOMERS",  
      SQL_NTS);  
SQLBindCol(hstmtSelect, 1, SQL_C_CHAR, szName, NAME_LEN, &cbName);  
SQLBindCol(hstmtSelect, 2, SQL_C_CHAR, szPhone, PHONE_LEN, &cbPhone);  
  
/* Read through the result set until the cursor is */  
/* positioned on the row for John Smith. */  
  
do  
 retcode = SQLFetch(hstmtSelect);  
while ((retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) &&  
   (strcmp(szName, "Smith, John") != 0));  
  
/* Perform a positioned update of John Smith's name. */  
  
if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
   SQLExecDirect(hstmtUpdate,  
   "UPDATE EMPLOYEE SET PHONE=\"2064890154\" WHERE CURRENT OF C1",  
   SQL_NTS);  
}  
```  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Executando uma instrução SQL|[Função SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Executando uma instrução SQL preparada|[Função SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Retornando um nome de cursor|[Função SQLGetCursorName](../../../odbc/reference/syntax/sqlgetcursorname-function.md)|  
|Definindo opções de rolagem do cursor|[Função SQLSetScrollOptions](../../../odbc/reference/syntax/sqlsetscrolloptions-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
