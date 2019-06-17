---
title: Função SQLGetStmtAttr | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f6edec1b341855154e6df6ef24abb7da3d93ffc2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65538012"
---
# <a name="sqlgetstmtattr-function"></a>Função SQLGetStmtAttr
**Conformidade com**  
 Versão introduzida: Conformidade com padrões 3.0 ODBC: ISO 92  
  
 **Resumo**  
 **SQLGetStmtAttr** retorna a configuração atual de um atributo de instrução.  
  
> [!NOTE]  
>  Para obter mais informações sobre o que o Gerenciador de Driver mapeia essa função quando um ODBC 3. *x* aplicativo está funcionando com um ODBC 2. *x* driver, consulte [mapeamento de funções de substituição para compatibilidade com versões anteriores de aplicativos](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
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
 [Entrada] Atributo a ser recuperado.  
  
 *ValuePtr*  
 [Saída] Ponteiro para um buffer no qual retornar o valor do atributo especificado na *atributo*.  
  
 Se *ValuePtr* for NULL, *StringLengthPtr* ainda retornará o número total de bytes (exceto o caractere nulo de terminação para dados de caracteres) disponíveis para retornar no buffer apontado por  *ValuePtr*.  
  
 *BufferLength*  
 [Entrada] Se *atributo* é um atributo definido pelo ODBC e *ValuePtr* aponta para uma cadeia de caracteres ou um buffer de binário, este argumento deve ser o comprimento da \* *ValuePtr*. Se *atributo* é um atributo definido pelo ODBC e \* *ValuePtr* é um inteiro, *BufferLength* será ignorado. Se o valor retornado em  *\*ValuePtr* é uma cadeia de caracteres Unicode (ao chamar **SQLGetStmtAttrW**), o *BufferLength* argumento deve ser um número par.  
  
 Se *atributo* é um atributo definido pelo driver, o aplicativo indica a natureza do atributo para o Gerenciador de Driver, definindo o *BufferLength* argumento. *BufferLength* pode ter os seguintes valores:  
  
-   Se  *\*ValuePtr* é um ponteiro para uma cadeia de caracteres, em seguida, *BufferLength* é o comprimento da cadeia de caracteres ou SQL_NTS.  
  
-   Se  *\*ValuePtr* é um ponteiro para um buffer de binário, em seguida, o aplicativo coloca o resultado do SQL_LEN_BINARY_ATTR (*comprimento*) macro na *BufferLength*. Isso coloca um valor negativo em *BufferLength*.  
  
-   Se  *\*ValuePtr* é um ponteiro para um valor diferente de uma cadeia de caracteres ou cadeia de caracteres binária, então *BufferLength* deve ter o valor SQL_IS_POINTER.  
  
-   Se  *\*ValuePtr* é contiver um tipo de dados de comprimento fixo, então *BufferLength* é SQL_IS_INTEGER ou SQL_IS_UINTEGER, conforme apropriado.  
  
 *StringLengthPtr*  
 [Saída] Um ponteiro para um buffer no qual retornar o número total de bytes (exceto o caractere nulo de terminação) disponíveis para retornar na  *\*ValuePtr*. Se *ValuePtr* for um ponteiro nulo, nenhum tamanho é retornado. Se o valor do atributo é uma cadeia de caracteres e o número de bytes disponíveis para retornar é maior que ou igual a *BufferLength*, os dados no  *\*ValuePtr* será truncado com *BufferLength* menos o comprimento de um caractere de finalização null e é terminada em nulo pelo driver.  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLGetStmtAttr** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtida chamando **SQLGetDiagRec** com um *HandleType* do SQL _HANDLE_STMT e uma *manipular* dos *StatementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLGetStmtAttr** e explica cada uma no contexto dessa função; a notação "(DM)" precede as descrições das SQLSTATEs retornados pelo Gerenciador de Driver. O código de retorno associado com cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa de específicos do driver. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|01004|Dados de cadeia de caracteres truncados à direita|Os dados retornados  *\*ValuePtr* foi truncado para ser *BufferLength* menos o comprimento de um caractere nulo de terminação. O comprimento do valor completo da cadeia de caracteres é retornado no **StringLengthPtr*. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|24000|Estado de cursor inválido|O argumento *atributo* foi SQL_ATTR_ROW_NUMBER e o cursor não foi aberto ou o cursor é posicionado antes do início do conjunto de resultados ou após o final do conjunto de resultados.|  
|HY000|Erro geral|Ocorreu um erro para o qual não houve nenhum SQLSTATE específico e para o qual não foi definida nenhuma SQLSTATE específicos de implementação. A mensagem de erro retornada por **SQLGetDiagRec** no argumento *MessageText* descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar a memória necessária para dar suporte à execução ou a conclusão da função.|  
|HY010|Erro de sequência de função|(DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado a *StatementHandle*. Essa função assíncrona ainda estava em execução quando o **SQLGetStmtAttr** função foi chamada.<br /><br /> (DM) uma função de execução assíncrona foi chamada para o *StatementHandle* e ainda estava em execução quando essa função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, ou **SQLSetPos** foi chamado para o  *StatementHandle* e retornados de SQL_NEED_DATA. Essa função foi chamada antes de dados foi enviados para todos os parâmetros de dados em execução ou colunas.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacente não pôde ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY090|Comprimento de buffer ou cadeia de caracteres inválido|*(DM) \*ValuePtr* é uma cadeia de caracteres e BufferLength era menor que zero, mas não é igual a SQL_NTS.|  
|HY092|Identificador de atributo/opção inválido|O valor especificado para o argumento *atributo* não era válido para a versão do ODBC com suporte pelo driver.|  
|HY109|Posição do cursor inválida|O *atributo* argumento era SQL_ATTR_ROW_NUMBER e a linha tivesse sido excluída ou não pôde ser buscada.|  
|HY117|Conexão está suspenso devido ao estado de transação desconhecida. Somente se desconectar e funções de somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Recurso opcional não implementado|O valor especificado para o argumento *atributo* foi um atributo de instrução ODBC válido para a versão do ODBC com suporte pelo driver, mas não tinha suporte pelo driver.|  
|HYT01|Tempo limite da Conexão expirado|O período de tempo limite de conexão expirado antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não oferece suporte a essa função|(DM) o driver correspondente a *StatementHandle* não suporta a função.|  
  
## <a name="comments"></a>Comentários  
 Para obter informações gerais sobre os atributos de instrução, consulte [atributos de instrução](../../../odbc/reference/develop-app/statement-attributes.md).  
  
 Uma chamada para **SQLGetStmtAttr** retorna  *\*ValuePtr* o valor do atributo de instrução especificado no *atributo*. Esse valor pode ser um valor SQLULEN ou uma cadeia de caracteres terminada em nulo. Se o valor é um valor SQLULEN, alguns drivers podem apenas gravar inferior 32 bits ou o bit de ordem superior de 16 bits de um buffer e deixar inalterado. Portanto, os aplicativos devem usar um buffer de SQLULEN e inicializar o valor para 0 antes de chamar essa função. Além disso, o *BufferLength* e *StringLengthPtr* argumentos não são usados. Se o valor for uma cadeia de caracteres terminada em nulo, o aplicativo especifica o comprimento máximo da cadeia de caracteres na *BufferLength* argumento e o driver retorna o comprimento da cadeia de caracteres na  *\* StringLengthPtr* buffer.  
  
 Para permitir que os aplicativos que chamam **SQLGetStmtAttr** para trabalhar com ODBC 2. *x* drivers, uma chamada para **SQLGetStmtAttr** é mapeada no Gerenciador de Driver para **SQLGetStmtOption**.  
  
 Os seguintes atributos de instrução são somente leitura, portanto, pode ser recuperada por **SQLGetStmtAttr**, mas não definido por **SQLSetStmtAttr**:  
  
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
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
