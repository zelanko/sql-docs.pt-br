---
title: Função SQLSetCursorName | Microsoft Docs
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
- SQLSetCursorName
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSetCursorName
helpviewer_keywords:
- SQLSetCursorName function [ODBC]
ms.assetid: 4e055946-12d4-4589-9891-41617a50f34e
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2501a747df22295cd42b9820e7b80b1ee9716333
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="sqlsetcursorname-function"></a>Função SQLSetCursorName
**Conformidade**  
 Versão introduzidas: Conformidade de padrões 1.0 ODBC: 92 ISO  
  
 **Resumo**  
 **SQLSetCursorName** associa um nome de cursor com uma instrução ativa. Se um aplicativo não chamar **SQLSetCursorName**, o driver gera nomes de cursor conforme necessário para o processamento de uma instrução SQL.  
  
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
 [Entrada] Nome de cursor. Para processamento eficiente, o nome de cursor não deve conter espaços à esquerda ou à direita no nome do cursor e, se o nome de cursor inclui um identificador delimitado, o delimitador deve ser tratado como o primeiro caractere no nome do cursor.  
  
 *NameLength*  
 [Entrada] Comprimento em caracteres de **CursorName*.  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>diagnóstico  
 Quando **SQLSetCursorName** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtida chamando **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_STMT e um *tratar* de *StatementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLSetCursorName** e explica cada uma no contexto dessa função; a notação "(DM)" precede as descrições de SQLSTATEs retornados pelo Gerenciador de Driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado em contrário.  
  
|SQLSTATE|Erro|Description|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem de informação específica do driver. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|01004|Dados de cadeia de caracteres truncados à direita|O nome de cursor excedeu o limite máximo, portanto apenas o número máximo permitido de caracteres foi usado.|  
|24000|Estado de cursor inválido|A instrução correspondente a *StatementHandle* já estava em um estado executado ou cursor posicionado.|  
|34000|Nome de cursor inválido|O nome de cursor especificado em **CursorName* era inválido porque ele excedeu o comprimento máximo, conforme definido pelo driver, com ou "SQLCUR" ou "SQL_CUR".|  
|3C000|Nome de cursor duplicado|O nome de cursor especificado em **CursorName* já existe.|  
|HY000|Erro geral|Ocorreu um erro para o qual não houve nenhuma SQLSTATE específico e para o qual nenhuma SQLSTATE específicos de implementação foi definida. A mensagem de erro retornada pelo **SQLGetDiagRec** no  *\*MessageText* buffer descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar a memória necessária para dar suporte a execução ou a conclusão da função.|  
|HY009|Uso inválido de ponteiro nulo|(DM) o argumento *CursorName* foi um ponteiro nulo.|  
|HY010|Erro de sequência de função|(DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado a *StatementHandle*. Essa função assíncrono ainda estava em execução quando o **SQLSetCursorName** função foi chamada.<br /><br /> (DM) uma função de execução assíncrona foi chamada para o *StatementHandle* e ainda estava em execução quando esta função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, ou **SQLSetPos** foi chamado para o  *StatementHandle* e retorna SQL_NEED_DATA. Essa função foi chamada antes de dados foi enviados para todas as colunas ou parâmetros de dados em execução.|  
|HY013|Erro de gerenciamento de memória|Não foi possível processar a chamada de função porque os objetos de memória subjacente não podem ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY090|Comprimento de buffer ou cadeia de caracteres inválido|(DM) o argumento *NameLength* era menor que 0 mas não igual a SQL_NTS.|  
|HY117|Conexão está suspenso devido ao estado de transação desconhecido. Somente Desconecte e funções de somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tempo limite de Conexão expirou|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não dá suporte a esta função|O driver em (DM) associado a *StatementHandle* não oferece suporte para a função.|  
  
## <a name="comments"></a>Comentários  
 Nomes de cursor são usados somente em atualização posicionada e instruções delete (por exemplo, **atualizar** *nome de tabela* ... **WHERE CURRENT OF** *nome de cursor*). Para obter mais informações, consulte [posicionado instruções Update e excluir](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md). Se o aplicativo não chamar **SQLSetCursorName** para definir um nome de cursor na execução de uma instrução de consulta, o driver gerará um nome que começa com as letras SQL_CUR e não excede 18 caracteres de comprimento.  
  
 Todos os nomes de cursor dentro de conexão devem ser exclusivos. O comprimento máximo de um nome de cursor é definido pelo driver. Para interoperabilidade máxima, recomenda-se que os aplicativos limitam nomes de cursor para não mais de 18 caracteres. Em ODBC 3*. x*, se um nome de cursor é um identificador entre aspas, ele será tratado de maiusculas e minúsculas e pode conter caracteres que a sintaxe de SQL não permitiria trataria especialmente, como espaços em branco ou palavras-chave reservadas. Se um nome de cursor deve ser tratado em maiusculas e minúsculas, ele deve ser passado como um identificador entre aspas.  
  
 Um nome de cursor que é definido explicitamente ou implicitamente permanece definido até que a instrução com o qual ele está associado é removida, usando **SQLFreeHandle**. **SQLSetCursorName** pode ser chamado para renomear um cursor em uma instrução, enquanto o cursor estiver em um estado preparado ou alocado.  
  
## <a name="code-example"></a>Exemplo de código  
 O exemplo a seguir, um aplicativo usa **SQLSetCursorName** para definir um nome de cursor para uma instrução. Ele então usa essa instrução para recuperar os resultados da tabela CUSTOMERS. Finalmente, ele executa uma atualização posicionada para alterar o número de telefone de John Smith. Observe que o aplicativo usa identificadores de instrução diferente para o **selecione** e **atualização** instruções.  
  
 Outro exemplo de código, consulte [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
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
|Executar uma instrução preparada do SQL|[Função SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Retornando um nome de cursor|[Função SQLGetCursorName](../../../odbc/reference/syntax/sqlgetcursorname-function.md)|  
|Definindo opções de rolagem do cursor|[Função SQLSetScrollOptions](../../../odbc/reference/syntax/sqlsetscrolloptions-function.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Referência de API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
