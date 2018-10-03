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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cca18bef15d57aa9d2cf97999939994a6c8c7934
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47662124"
---
# <a name="sqlsetcursorname-function"></a>Função SQLSetCursorName
**Conformidade com**  
 Versão introduziu: Conformidade de padrões 1.0 ODBC: ISO 92  
  
 **Resumo**  
 **SQLSetCursorName** associa um nome de cursor com uma instrução ativa. Se um aplicativo chamar **SQLSetCursorName**, o driver vai gerar nomes de cursor, conforme necessário para processamento de uma instrução SQL.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SQLRETURN SQLSetCursorName(  
     SQLHSTMT      StatementHandle,  
     SQLCHAR *     CursorName,  
     SQLSMALLINT   NameLength);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Identificador de instrução.  
  
 *cursorName*  
 [Entrada] Nome de cursor. Para o processamento eficiente, o nome de cursor não deve incluir espaços à esquerda ou à direita no nome do cursor e, se o nome do cursor inclui um identificador delimitado, o delimitador deve ser posicionado como o primeiro caractere no nome do cursor.  
  
 *NameLength*  
 [Entrada] Comprimento em caracteres de **CursorName*.  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLSetCursorName** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtida chamando **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_STMT e uma *manipular* dos *StatementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLSetCursorName** e explica cada uma no contexto dessa função; a notação "(DM)" precede as descrições das SQLSTATEs retornados pelo Gerenciador de Driver. O código de retorno associado com cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
|SQLSTATE|Erro|Description|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa de específicos do driver. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|01004|Dados de cadeia de caracteres truncados à direita|O nome do cursor excedeu o limite máximo, portanto, apenas o número máximo permitido de caracteres foi usado.|  
|24000|Estado de cursor inválido|A instrução correspondente a *StatementHandle* já estava em estado executado ou o cursor posicionado.|  
|34000|Nome de cursor inválido|O nome de cursor especificado no **CursorName* era inválido porque ele excedeu o comprimento máximo, conforme definido pelo driver, ou ela iniciada com "SQLCUR" ou "SQL_CUR".|  
|3C000|Nome de cursor duplicado|O nome de cursor especificado no **CursorName* já existe.|  
|HY000|Erro geral|Ocorreu um erro para o qual não houve nenhum SQLSTATE específico e para o qual não foi definida nenhuma SQLSTATE específicos de implementação. A mensagem de erro retornada por **SQLGetDiagRec** na  *\*MessageText* buffer descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar a memória necessária para dar suporte à execução ou a conclusão da função.|  
|HY009|Uso inválido de ponteiro nulo|(DM) o argumento *CursorName* é um ponteiro nulo.|  
|HY010|Erro de sequência de função|(DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado a *StatementHandle*. Essa função assíncrono ainda estava em execução quando o **SQLSetCursorName** função foi chamada.<br /><br /> (DM) uma função de execução assíncrona foi chamada para o *StatementHandle* e ainda estava em execução quando essa função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, ou **SQLSetPos** foi chamado para o  *StatementHandle* e retornados de SQL_NEED_DATA. Essa função foi chamada antes de dados foi enviados para todos os parâmetros de dados em execução ou colunas.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacente não pôde ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY090|Comprimento de buffer ou cadeia de caracteres inválido|(DM) o argumento *NameLength* era menor que 0, mas não é igual a SQL_NTS.|  
|HY117|Conexão está suspenso devido ao estado de transação desconhecida. Somente se desconectar e funções de somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tempo limite da Conexão expirado|O período de tempo limite de conexão expirado antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não oferece suporte a essa função|O driver em (DM) associado a *StatementHandle* não suporta a função.|  
  
## <a name="comments"></a>Comentários  
 Nomes de cursor são usados apenas na atualização posicionadas e instruções delete (por exemplo, **atualize** *nome da tabela* ... **WHERE CURRENT OF** *nome de cursor*). Para obter mais informações, consulte [posicionado instruções Update e excluir](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md). Se o aplicativo não chama **SQLSetCursorName** para definir um nome de cursor na execução de uma instrução de consulta, o driver gerará um nome que começa com as letras SQL_CUR e não excede 18 caracteres de comprimento.  
  
 Todos os nomes de cursor dentro a conexão devem ser exclusivos. O comprimento máximo de um nome de cursor é definido pelo driver. Para interoperabilidade máxima, recomenda-se que os aplicativos limitam os nomes de cursor para não mais de 18 caracteres. Em ODBC 3 *. x*, se um nome de cursor é um identificador entre aspas, ele será tratado de maneira diferencia maiusculas de minúsculas e pode conter caracteres que a sintaxe do SQL não permitiria ou trataria especialmente, como espaços em branco ou palavras-chave reservadas. Se um nome de cursor deve ser tratado de maneira diferencia maiusculas de minúsculas, ele deverá ser passado como um identificador entre aspas.  
  
 Um nome de cursor que é definido explicitamente ou implicitamente permanece definido até que a instrução ao qual ele está associado é descartada, usando **SQLFreeHandle**. **SQLSetCursorName** pode ser chamado para renomear um cursor em uma instrução, contanto que o cursor estiver em um estado preparado ou alocado.  
  
## <a name="code-example"></a>Exemplo de código  
 O exemplo a seguir, um aplicativo usa **SQLSetCursorName** para definir um nome de cursor para uma instrução. Ele usa essa instrução para recuperar os resultados da tabela CUSTOMERS. Por fim, ele executa uma atualização posicionada para alterar o número de telefone de John Smith. Observe que o aplicativo usa identificadores de instrução diferente para o **selecionar** e **atualização** instruções.  
  
 Para obter outro exemplo de código, consulte [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
```  
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
|Executar uma instrução SQL|[Função SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Executar uma instrução SQL preparada|[Função SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Retornando um nome de cursor|[Função SQLGetCursorName](../../../odbc/reference/syntax/sqlgetcursorname-function.md)|  
|Definindo opções de rolagem do cursor|[Função SQLSetScrollOptions](../../../odbc/reference/syntax/sqlsetscrolloptions-function.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
