---
title: Função SQLGetConnectAttr | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
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
- SQLGetConnectOption
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetConnectAttr
helpviewer_keywords:
- SQLGetConnectAttr function [ODBC]
ms.assetid: 2cb4ffa8-19d3-4664-8c2f-6682cdcc3f33
caps.latest.revision: 32
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 11e1ae7c2dc3de4611687349295bdd3344c46d47
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="sqlgetconnectattr-function"></a>Função SQLGetConnectAttr
**Conformidade**  
 Versão introduzidas: Conformidade de padrões 3.0 ODBC: 92 ISO  
  
 **Resumo**  
 **SQLGetConnectAttr** retorna a configuração atual de um atributo de conexão.  
  
> [!NOTE]  
>  Para obter mais informações sobre o que o Gerenciador de Driver mapeia essa função quando um ODBC 3*. x* aplicativo estiver trabalhando com um ODBC 2*. x* driver, consulte [mapeamento de funções de substituição para recuar Compatibilidade de aplicativos](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SQLRETURN SQLGetConnectAttr(  
     SQLHDBC        ConnectionHandle,  
     SQLINTEGER     Attribute,  
     SQLPOINTER     ValuePtr,  
     SQLINTEGER     BufferLength,  
     SQLINTEGER *   StringLengthPtr);  
```  
  
## <a name="arguments"></a>Argumentos  
 *Identificador da conexão*  
 [Entrada] Identificador de Conexão.  
  
 *Atributo*  
 [Entrada] Atributo para recuperar.  
  
 *ValuePtr*  
 [Saída] Um ponteiro de memória no qual retornar o valor atual do atributo especificado por *atributo*. Para atributos de tipo inteiro, alguns drivers podem gravar somente inferior 32 bits ou 16 bits de um buffer e deixe o bit de ordem superior inalterado. Portanto, os aplicativos devem usar um buffer de SQLULEN e inicializar o valor para 0 antes de chamar essa função.  
  
 Se *ValuePtr* for NULL, *StringLengthPtr* ainda retornará o número total de bytes (excluindo o caractere null de terminação para dados de caractere) disponíveis para retornar o buffer apontado pelo  *ValuePtr*.  
  
 *BufferLength*  
 [Entrada] Se *atributo* é um atributo definido pelo ODBC e *ValuePtr* aponta para uma cadeia de caracteres ou um buffer binário, este argumento deve ser o comprimento de \* *ValuePtr*. Se *atributo* é um atributo definido pelo ODBC e \* *ValuePtr* é um inteiro, *BufferLength* será ignorado. Se o valor em  *\*ValuePtr* é uma cadeia de caracteres Unicode (ao chamar **SQLGetConnectAttrW**), o *BufferLength* argumento deve ser um número par.  
  
 Se *atributo* é um atributo definido pelo driver, o aplicativo indica a natureza do atributo para o Gerenciador de Driver, definindo o *BufferLength* argumento. *BufferLength* pode ter os seguintes valores:  
  
-   Se  *\*ValuePtr* é um ponteiro para uma cadeia de caracteres, *BufferLength* é o comprimento da cadeia de caracteres.  
  
-   Se  *\*ValuePtr* é um ponteiro para um buffer de binário, os locais de aplicativo o resultado da SQL_LEN_BINARY_ATTR (*comprimento*) macro em *BufferLength*. Isso coloca um valor negativo em *BufferLength*.  
  
-   Se  *\*ValuePtr* é um ponteiro para um valor diferente de uma cadeia de caracteres ou cadeia de caracteres binária, *BufferLength* devem ter o valor SQL_IS_POINTER.  
  
-   Se  *\*ValuePtr* contém um tipo de dados de comprimento fixo, *BufferLength* é SQL_IS_INTEGER ou SQL_IS_UINTEGER, conforme apropriado.  
  
 *StringLengthPtr*  
 [Saída] Um ponteiro para um buffer no qual retornar o número total de bytes (excluindo o caractere null de terminação) disponíveis para retornar em \* *ValuePtr*. Se \* *ValuePtr* é um ponteiro nulo, nenhum comprimento é retornado. Se o valor do atributo é uma cadeia de caracteres e o número de bytes disponíveis para retornar é maior do que *BufferLength* menos o comprimento do caractere null de terminação, os dados em  *\*ValuePtr*é truncado para *BufferLength* menos o comprimento do caractere null de terminação e é terminada em nulo pelo driver.  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>diagnóstico  
 Quando **SQLGetConnectAttr** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtida da estrutura de dados de diagnóstico chamando **SQLGetDiagRec** com um *HandleType* SQL_HANDLE_DBC e um *tratar* de *identificador da conexão*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLGetConnectAttr** e explica cada uma no contexto dessa função; a notação "(DM)" precede as descrições de SQLSTATEs retornados pelo Gerenciador de Driver . O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado em contrário.  
  
|SQLSTATE|Erro|Description|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem de informação específica do driver. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|01004|Dados de cadeia de caracteres truncados à direita|Os dados retornados em \* *ValuePtr* foi truncado para ser *BufferLength* menos o comprimento de um caractere null de terminação. O comprimento do valor completo da cadeia de caracteres é retornado em **StringLengthPtr*. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|08003|Conexão não aberta|(DM) um *atributo* foi especificado um valor que é necessária uma conexão aberta.|  
|08S01|Falha de link de comunicação|Falha do link de comunicação entre o driver e a fonte de dados ao qual o driver foi conectado antes do processamento da função foi concluída.|  
|HY000|Erro geral|Ocorreu um erro para o qual não houve nenhuma SQLSTATE específico e para o qual nenhuma SQLSTATE específicos de implementação foi definida. A mensagem de erro retornado da estrutura de dados de diagnóstico pelo argumento *MessageText* na **SQLGetDiagField** descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar a memória necessária para dar suporte a execução ou a conclusão da função.|  
|HY010|Erro de sequência de função|(DM) **SQLBrowseConnect** foi chamado para o *identificador da conexão* e retorna SQL_NEED_DATA. Essa função foi chamada antes de **SQLBrowseConnect** retornado SQL_SUCCESS_WITH_INFO ou SQL_SUCCESS.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, ou **SQLMoreResults** foi chamado para o *identificador da conexão* e retornado SQL_PARAM_DATA_ DISPONÍVEL. Essa função foi chamada antes de recuperação para todos os parâmetros de fluxo de dados.|  
|HY013|Erro de gerenciamento de memória|Não foi possível processar a chamada de função porque os objetos de memória subjacente não podem ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY090|Comprimento de buffer ou cadeia de caracteres inválido|(DM)  *\*ValuePtr* é uma cadeia de caracteres e BufferLength era menor que zero, mas não é igual a SQL_NTS.|  
|HY092|Identificador de atributo/opção inválido|O valor especificado para o argumento *atributo* não era válido para a versão do ODBC com suporte pelo driver.|  
|HY114|Driver não oferece suporte à execução de função assíncrona de nível de conexão|Tentativa de um aplicativo (DM) habilitar a execução de função assíncrona com SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE para um driver que não oferece suporte a operações de conexão assíncrona.|  
|HY117|Conexão está suspenso devido ao estado de transação desconhecido. Somente Desconecte e funções de somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Recurso opcional não implementado|O valor especificado para o argumento *atributo* era um atributo de conexão ODBC válido para a versão do ODBC com suporte pelo driver, mas não era compatível com o driver.|  
|HYT01|Tempo limite de Conexão expirou|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não dá suporte a esta função|(DM) o driver que corresponde do *identificador da conexão* não oferece suporte para a função.|  
  
## <a name="comments"></a>Comentários  
 Para obter informações gerais sobre os atributos de conexão, consulte [atributos de Conexão](../../../odbc/reference/develop-app/connection-attributes.md).  
  
 Para obter uma lista de atributos que podem ser definidas, consulte [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md). Observe que, se *atributo* Especifica um atributo que retorna uma cadeia de caracteres, *ValuePtr* deve ser um ponteiro para um buffer de cadeia de caracteres. O comprimento máximo da cadeia de caracteres retornada, incluindo o caractere de terminação null, será *BufferLength* bytes.  
  
 Dependendo do atributo, um aplicativo não precisa estabelecer uma conexão antes de chamar **SQLGetConnectAttr**. No entanto, se **SQLGetConnectAttr** é chamado e o atributo especificado não tem um padrão e não tiver sido definido por uma chamada anterior ao **SQLSetConnectAttr**, **SQLGetConnectAttr**retorna SQL_NO_DATA.  
  
 Se *atributo* é sql_attr rastreamento ou sql_attr TRACEFILE, *identificador da conexão* não precisa ser válido, e **SQLGetConnectAttr** não retornará SQL_ERROR ou SQL _ INVALID_HANDLE se *identificador da conexão* é inválido. Esses atributos se aplicam a todas as conexões. **SQLGetConnectAttr** retornará SQL_ERROR ou SQL_INVALID_HANDLE se outro argumento é inválido.  
  
 Embora um aplicativo pode definir atributos de instrução usando **SQLSetConnectAttr**, não é possível usar um aplicativo **SQLGetConnectAttr** para recuperar o atributo de instrução valores; ele deve chamar  **SQLGetStmtAttr** para recuperar a configuração de atributos de instrução.  
  
 Atributos de conexão SQL_ATTR_AUTO_IPD e SQL_ATTR_CONNECTION_DEAD podem ser retornados por uma chamada para **SQLGetConnectAttr** , mas não pode ser definida por uma chamada para **SQLSetConnectAttr**.  
  
> [!NOTE]  
>  Não há suporte assíncrono para **SQLGetConnectAttr**. Ao implementar **SQLGetConnectAttr**, um driver pode melhorar o desempenho, reduzindo o número de vezes que informações são enviadas ou solicitadas do servidor.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Retornando a configuração de um atributo de instrução|[Função SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|  
|Definir um atributo de conexão|[Função SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|Definindo um atributo de ambiente|[Função SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)|  
|Definir um atributo de instrução|[Função SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
