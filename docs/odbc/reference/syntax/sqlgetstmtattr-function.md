---
title: "Função SQLGetStmtAttr | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLGetStmtAttr
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetStmtAttr
helpviewer_keywords:
- SQLGetStmtAttr function [ODBC]
ms.assetid: e321d460-e997-4527-aee6-207cf5a498e9
caps.latest.revision: 25
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 478d69a608740a0c8886336ca567ebc8ec75d6eb
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="sqlgetstmtattr-function"></a>Função SQLGetStmtAttr
**Conformidade**  
 Versão introduzidas: Conformidade de padrões 3.0 ODBC: 92 ISO  
  
 **Resumo**  
 **SQLGetStmtAttr** retorna a configuração atual de um atributo de instrução.  
  
> [!NOTE]  
>  Para obter mais informações sobre o que o Gerenciador de Driver mapeia essa função quando um ODBC 3. *x* aplicativo estiver trabalhando com um ODBC 2. *x* driver, consulte [mapeamento de funções de substituição para compatibilidade com versões anteriores de aplicativos](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SQLRETURN SQLGetStmtAttr(  
     SQLHSTMT        StatementHandle,  
     SQLINTEGER      Attribute,  
     SQLPOINTER      ValuePtr,  
     SQLINTEGER      BufferLength,  
     SQLINTEGER *    StringLengthPtr);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Identificador de instrução.  
  
 *Atributo*  
 [Entrada] Atributo para recuperar.  
  
 *ValuePtr*  
 [Saída] Ponteiro para um buffer no qual retornar o valor do atributo especificado no *atributo*.  
  
 Se *ValuePtr* for NULL, *StringLengthPtr* ainda retornará o número total de bytes (excluindo o caractere null de terminação para dados de caractere) disponíveis para retornar o buffer apontado pelo  *ValuePtr*.  
  
 *BufferLength*  
 [Entrada] Se *atributo* é um atributo definido pelo ODBC e *ValuePtr* aponta para uma cadeia de caracteres ou um buffer binário, este argumento deve ser o comprimento de \* *ValuePtr*. Se *atributo* é um atributo definido pelo ODBC e \* *ValuePtr* é um inteiro, *BufferLength* será ignorado. Se o valor retornado em  *\*ValuePtr* é uma cadeia de caracteres Unicode (ao chamar **SQLGetStmtAttrW**), o *BufferLength* argumento deve ser um número par.  
  
 Se *atributo* é um atributo definido pelo driver, o aplicativo indica a natureza do atributo para o Gerenciador de Driver, definindo o *BufferLength* argumento. *BufferLength* pode ter os seguintes valores:  
  
-   Se  *\*ValuePtr* é um ponteiro para uma cadeia de caracteres, em seguida, *BufferLength* é o comprimento da cadeia de caracteres ou SQL_NTS.  
  
-   Se  *\*ValuePtr* é um ponteiro para um buffer de binário, em seguida, o aplicativo coloca o resultado da SQL_LEN_BINARY_ATTR (*comprimento*) macro em *BufferLength*. Isso coloca um valor negativo em *BufferLength*.  
  
-   Se  *\*ValuePtr* é um ponteiro para um valor diferente de uma cadeia de caracteres ou cadeia de caracteres binária, em seguida, *BufferLength* devem ter o valor SQL_IS_POINTER.  
  
-   Se  *\*ValuePtr* é contém um tipo de dados de comprimento fixo, em seguida, *BufferLength* é SQL_IS_INTEGER ou SQL_IS_UINTEGER, conforme apropriado.  
  
 *StringLengthPtr*  
 [Saída] Um ponteiro para um buffer no qual retornar o número total de bytes (excluindo o caractere null de terminação) disponíveis para retornar em  *\*ValuePtr*. Se *ValuePtr* é um ponteiro nulo, nenhum comprimento é retornado. Se o valor do atributo é uma cadeia de caracteres e o número de bytes disponíveis para retornar é maior que ou igual a *BufferLength*, os dados em  *\*ValuePtr* será truncado para *BufferLength* menos o comprimento de um caractere null de terminação e é terminada em nulo pelo driver.  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>diagnóstico  
 Quando **SQLGetStmtAttr** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtida chamando **SQLGetDiagRec** com um *HandleType* do SQL _HANDLE_STMT e um *tratar* de *StatementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLGetStmtAttr** e explica cada uma no contexto dessa função; a notação "(DM)" precede as descrições de SQLSTATEs retornados pelo Gerenciador de Driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado em contrário.  
  
|SQLSTATE|Erro|Description|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem de informação específica do driver. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|01004|Dados de cadeia de caracteres truncados à direita|Os dados retornados em  *\*ValuePtr* foi truncado para ser *BufferLength* menos o comprimento de um caractere null de terminação. O comprimento do valor completo da cadeia de caracteres é retornado em **StringLengthPtr*. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|24000|Estado de cursor inválido|O argumento *atributo* foi SQL_ATTR_ROW_NUMBER e o cursor não foi aberto ou o cursor é posicionado antes do início do conjunto de resultados ou após o final do conjunto de resultados.|  
|HY000|Erro geral|Ocorreu um erro para o qual não houve nenhuma SQLSTATE específico e para o qual nenhuma SQLSTATE específicos de implementação foi definida. A mensagem de erro retornada pelo **SQLGetDiagRec** no argumento *MessageText* descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar a memória necessária para dar suporte a execução ou a conclusão da função.|  
|HY010|Erro de sequência de função|(DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado a *StatementHandle*. Essa função assíncrona ainda estava em execução quando o **SQLGetStmtAttr** função foi chamada.<br /><br /> (DM) uma função de execução assíncrona foi chamada para o *StatementHandle* e ainda estava em execução quando esta função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, ou **SQLSetPos** foi chamado para o  *StatementHandle* e retorna SQL_NEED_DATA. Essa função foi chamada antes de dados foi enviados para todas as colunas ou parâmetros de dados em execução.|  
|HY013|Erro de gerenciamento de memória|Não foi possível processar a chamada de função porque os objetos de memória subjacente não podem ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY090|Comprimento de buffer ou cadeia de caracteres inválido|*(DM) \*ValuePtr* é uma cadeia de caracteres e BufferLength era menor que zero, mas não igual a SQL_NTS.|  
|HY092|Identificador de atributo/opção inválido|O valor especificado para o argumento *atributo* não era válido para a versão do ODBC com suporte pelo driver.|  
|HY109|Posição de cursor inválido|O *atributo* argumento era SQL_ATTR_ROW_NUMBER e a linha tivesse sido excluída ou não pôde ser obtida.|  
|HY117|Conexão está suspenso devido ao estado de transação desconhecido. Somente Desconecte e funções de somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Recurso opcional não implementado|O valor especificado para o argumento *atributo* era um atributo de instrução ODBC válido para a versão do ODBC com suporte pelo driver, mas não era compatível com o driver.|  
|HYT01|Tempo limite de Conexão expirou|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não dá suporte a esta função|(DM) o driver correspondente a *StatementHandle* não oferece suporte para a função.|  
  
## <a name="comments"></a>Comentários  
 Para obter informações gerais sobre os atributos de instrução, consulte [atributos de instrução](../../../odbc/reference/develop-app/statement-attributes.md).  
  
 Uma chamada para **SQLGetStmtAttr** retorna  *\*ValuePtr* o valor do atributo de declaração especificado no *atributo*. Esse valor pode ser um valor SQLULEN ou uma cadeia de caracteres terminada em nulo. Se o valor for um valor SQLULEN, alguns drivers podem gravar somente inferior 32 bits ou 16 bits de um buffer e deixe o bit de ordem superior inalterado. Portanto, os aplicativos devem usar um buffer de SQLULEN e inicializar o valor para 0 antes de chamar essa função. Além disso, o *BufferLength* e *StringLengthPtr* argumentos não são usados. Se o valor for uma cadeia de caracteres terminada em nulo, o aplicativo especifica o tamanho máximo dessa cadeia de caracteres no *BufferLength* argumento e o driver retorna o comprimento dessa cadeia de caracteres no  *\* StringLengthPtr* buffer.  
  
 Para permitir que aplicativos que chamam **SQLGetStmtAttr** para trabalhar com ODBC 2. *x* drivers, uma chamada para **SQLGetStmtAttr** está mapeado no Gerenciador de Driver para **SQLGetStmtOption**.  
  
 Os seguintes atributos de instrução são somente leitura, portanto pode ser recuperada por **SQLGetStmtAttr**, mas não definido por **SQLSetStmtAttr**:  
  
-   SQL_ATTR_IMP_PARAM_DESC  
  
-   SQL_ATTR_IMP_ROW_DESC  
  
-   SQL_ATTR_ROW_NUMBER  
  
 Para obter uma lista de atributos que podem ser definidas e recuperadas, consulte [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Retornando a configuração de um atributo de conexão|[Função SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|Definir um atributo de conexão|[Função SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|Definir um atributo de instrução|[Função SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Referência de API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)

