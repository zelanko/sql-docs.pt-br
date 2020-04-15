---
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
ms.openlocfilehash: 6a3bcd07a39401d49be04d141e50c671179efb16
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287336"
---
# <a name="sqlsetcursorname-function"></a>Função SQLSetCursorName
**Conformidade**  
 Versão introduzida: ODBC 1.0 Standards Compliance: ISO 92  
  
 **Resumo**  
 **SQLSetCursorName** associa um nome de cursor a uma declaração ativa. Se um aplicativo não chamar **SQLSetCursorName,** o driver gerará nomes de cursor conforme necessário para o processamento da declaração SQL.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLSetCursorName(  
     SQLHSTMT      StatementHandle,  
     SQLCHAR *     CursorName,  
     SQLSMALLINT   NameLength);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Alça de declaração.  
  
 *CursorNome*  
 [Entrada] Nome do cursor. Para um processamento eficiente, o nome do cursor não deve incluir nenhum espaço de liderança ou de arrasto no nome do cursor, e se o nome do cursor incluir um identificador delimitado, o delimitador deve ser posicionado como o primeiro caractere no nome do cursor.  
  
 *NameLength*  
 [Entrada] Comprimento em caracteres de **CursorName*.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **o SQLSetCursorName** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido ligando para **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_STMT e uma *alça* de controle de *declaração*. A tabela a seguir lista os valores SQLSTATE comumente retornados por **SQLSetCursorName** e explica cada um no contexto desta função; a notação "(DM)" precede as descrições de SQLSTATEs devolvidas pelo Driver Manager. O código de devolução associado a cada valor SQLSTATE é SQL_ERROR, a menos que seja observado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informacional específica do motorista. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|01004|Dados de cordas, truncados direito|O nome cursor excedeu o limite máximo, de modo que apenas o número máximo permitido de caracteres foi usado.|  
|24.000|Estado de cursor inválido|A declaração correspondente ao *StatementHandle* já estava em um estado executado ou posicionado pelo cursor.|  
|34000|Nome de cursor inválido|O nome do cursor especificado em **CursorName* era inválido porque excedia o comprimento máximo definido pelo driver, ou começou com "SQLCUR" ou "SQL_CUR".|  
|3C000|Nome do cursor duplicado|O nome do cursor especificado em **CursorName* já existe.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia SQLSTATE específico e para o qual não foi definido sqlSTATE específico para a implementação. A mensagem de erro retornada pelo **SQLGetDiagRec** no * \** buffer MessageText descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não conseguiu alocar a memória necessária para suportar a execução ou a conclusão da função.|  
|HY009|Uso inválido do ponteiro nulo|(DM) O argumento *CursorName* era um ponteiro nulo.|  
|HY010|Erro de seqüência de função|(DM) Uma função de execução assíncrona foi chamada para o cabo de conexão associado ao *StatementHandle*. Esta função ayncrona ainda estava sendo executada quando a função **SQLSetCursorName** foi chamada.<br /><br /> (DM) Uma função de execução assíncrona foi chamada para o *StatementHandle* e ainda estava sendo executada quando esta função foi chamada.<br /><br /> (DM) **SQLExecute,** **SQLExecDirect,** **SQLBulkOperations**ou **SQLSetPos** foram chamados para o *StatementHandle* e retornaram SQL_NEED_DATA. Essa função foi chamada antes de os dados serem enviados para todos os parâmetros ou colunas de execução de dados.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não podiam ser acessados, possivelmente devido às baixas condições de memória.|  
|HY090|Comprimento de seqüência ou buffer inválido|(DM) O argumento *NameLength* era menor que 0, mas não igual a SQL_NTS.|  
|HY117|A conexão está suspensa devido ao estado de transação desconhecido. Somente funções desconectadas e somente leitura são permitidas.|(DM) Para obter mais informações sobre o estado suspenso, consulte [a função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tempo de tempo de conexão expirado|O período de tempo de tempo de conexão expirou antes que a fonte de dados respondesse à solicitação. O período de tempo de tempo de conexão é definido através **de SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não suporta esta função|(DM) O driver associado ao *StatementHandle* não suporta a função.|  
  
## <a name="comments"></a>Comentários  
 Os nomes do cursor são usados apenas em instruções de atualização e exclusão posicionadas (por **exemplo,** _UPDATE-name_ ... **ONDE CORRENTE DE** _cursor-nome_). Para obter mais informações, consulte [Instruções de atualização posicionada e exclusão](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md). Se o aplicativo não chamar **SQLSetCursorName** para definir um nome de cursor, na execução de uma declaração de consulta o driver gera um nome que começa com as letras SQL_CUR e não excede 18 caracteres no comprimento.  
  
 Todos os nomes do cursor dentro da conexão devem ser únicos. O comprimento máximo de um nome do cursor é definido pelo driver. Para interoperabilidade máxima, recomenda-se que os aplicativos limitem os nomes do cursor a no máximo 18 caracteres. Em ODBC 3 *.x*, se um nome de cursor é um identificador citado, ele é tratado de forma sensível a maiúsculas e pode conter caracteres que a sintaxe de SQL não permitiria ou trataria especialmente, como espaços em branco ou palavras-chave reservadas. Se um nome cursor deve ser tratado de forma sensível ao caso, ele deve ser passado como um identificador citado.  
  
 Um nome do cursor definido explicitamente ou implicitamente permanece definido até que a instrução com a qual está associada seja descartada, usando **SQLFreeHandle**. **SQLSetCursorName** pode ser chamado para renomear um cursor em uma declaração, desde que o cursor esteja em um estado alocado ou preparado.  
  
## <a name="code-example"></a>Exemplo de código  
 No exemplo a seguir, um aplicativo usa **SQLSetCursorName** para definir um nome de cursor para uma declaração. Em seguida, ele usa essa declaração para recuperar resultados da tabela CLIENTES. Finalmente, ele realiza uma atualização posicionada para alterar o número de telefone de John Smith. Observe que o aplicativo usa diferentes alças de instrução para as instruções **SELECT** e **UPDATE.**  
  
 Para outro exemplo de código, consulte [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
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
|Executando uma declaração SQL|[Função SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Executando uma declaração SQL preparada|[Função SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Retornando um nome de cursor|[Função SQLGetCursorName](../../../odbc/reference/syntax/sqlgetcursorname-function.md)|  
|Definindo opções de rolagem do cursor|[Função SQLSetScrollOptions](../../../odbc/reference/syntax/sqlsetscrolloptions-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API oDBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
