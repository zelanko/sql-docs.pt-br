---
title: Função SQLGetConnectAttr | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e6076f14ff0c33fec38b99e9c43b8a688970a7a9
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81285626"
---
# <a name="sqlgetconnectattr-function"></a>Função SQLGetConnectAttr
**Conformidade**  
 Versão introduzida: conformidade de padrões do ODBC 3,0: ISO 92  
  
 **Resumo**  
 **SQLGetConnectAttr** retorna a configuração atual de um atributo de conexão.  
  
> [!NOTE]
>  Para obter mais informações sobre como o Gerenciador de driver mapeia essa função quando um aplicativo ODBC 3 *. x* está trabalhando com um driver ODBC 2 *. x* , consulte [mapeando funções de substituição para compatibilidade com versões anteriores de aplicativos](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLGetConnectAttr(  
     SQLHDBC        ConnectionHandle,  
     SQLINTEGER     Attribute,  
     SQLPOINTER     ValuePtr,  
     SQLINTEGER     BufferLength,  
     SQLINTEGER *   StringLengthPtr);  
```  
  
## <a name="arguments"></a>Argumentos  
 *ConnectionHandle*  
 [Entrada] Identificador de conexão.  
  
 *Atributo*  
 Entrada Atributo a ser recuperado.  
  
 *ValuePtr*  
 Der Um ponteiro para a memória na qual retornar o valor atual do atributo especificado pelo *atributo*. Para atributos de tipo inteiro, alguns drivers só podem gravar o menor 32 ou 16 bits de um buffer e deixar o bit de ordem superior inalterado. Portanto, os aplicativos devem usar um buffer de SQLULEN e inicializar o valor para 0 antes de chamar essa função.  
  
 Se *ValuePtr* for NULL, *StringLengthPtr* ainda retornará o número total de bytes (excluindo o caractere de terminação nula para dados de caracteres) disponíveis para retornar no buffer apontado por *ValuePtr*.  
  
 *BufferLength*  
 Entrada Se o *atributo* for um atributo definido pelo ODBC e *ValuePtr* apontar para uma cadeia de caracteres ou um buffer binário, esse argumento deverá ter o \*comprimento de *ValuePtr*. Se o *atributo* for um atributo definido pelo ODBC \*e *ValuePtr* for um inteiro, *BufferLength* será ignorado. Se o valor em * \*ValuePtr* for uma cadeia de caracteres Unicode (ao chamar **SQLGetConnectAttrW**), o argumento *BufferLength* deverá ser um número par.  
  
 Se o *atributo* for um atributo definido por Driver, o aplicativo indicará a natureza do atributo para o Gerenciador de driver, definindo o argumento *BufferLength* . *BufferLength* pode ter os seguintes valores:  
  
-   Se * \*ValuePtr* for um ponteiro para uma cadeia de caracteres, *BufferLength* será o comprimento da cadeia de caracteres.  
  
-   Se * \*ValuePtr* for um ponteiro para um buffer binário, o aplicativo colocará o resultado da macro SQL_LEN_BINARY_ATTR (*Length*) em *BufferLength*. Isso coloca um valor negativo em *BufferLength*.  
  
-   Se * \*ValuePtr* for um ponteiro para um valor diferente de uma cadeia de caracteres ou uma cadeia de caracteres binária, *BufferLength* deverá ter o valor SQL_IS_POINTER.  
  
-   Se * \*ValuePtr* contiver um tipo de dados de comprimento fixo, o *BufferLength* será SQL_IS_INTEGER ou SQL_IS_UINTEGER, conforme apropriado.  
  
 *StringLengthPtr*  
 Der Um ponteiro para um buffer no qual retornar o número total de bytes (excluindo o caractere de terminação nula) disponível para retornar \*em *ValuePtr*. Se \* *ValuePtr* for um ponteiro nulo, nenhum comprimento será retornado. Se o valor do atributo for uma cadeia de caracteres e o número de bytes disponíveis para retornar for maior que *BufferLength* menos o comprimento do caractere de terminação de nulo, os dados em * \*ValuePtr* serão truncados para *BufferLength* menos o comprimento do caractere de terminação nula e serão terminados em nulo pelo driver.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLGetConnectAttr** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido na estrutura de dados de diagnóstico chamando **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_DBC e um *identificador* de *ConnectionHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLGetConnectAttr** e explica cada um no contexto dessa função; a notação "(DM)" precede as descrições de sqlstates retornadas pelo Gerenciador de driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa específica do driver. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|01004|Dados de cadeia de caracteres, truncados à direita|Os dados retornados em \* *ValuePtr* foram truncados para serem *BufferLength* menos o comprimento de um caractere de terminação nula. O comprimento do valor de cadeia de caracteres não truncado é retornado em **StringLengthPtr*. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|08003|Conexão não aberta|(DM) um valor de *atributo* que exigia uma conexão aberta foi especificado.|  
|08S01|Falha no link de comunicação|O link de comunicação entre o driver e a fonte de dados ao qual o driver foi conectado falhou antes da função concluir o processamento.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia um SQLSTATE específico e para o qual nenhum SQLSTATE específico de implementação foi definido. A mensagem de erro retornada da estrutura de dados de diagnóstico pelo argumento *MessageText* em **SQLGetDiagField** descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar memória necessária para dar suporte à execução ou à conclusão da função.|  
|HY010|Erro de sequência de função|(DM) **SQLBrowseConnect** foi chamado para o *ConnectionHandle* e retornou SQL_NEED_DATA. Essa função foi chamada antes de **SQLBrowseConnect** retornar SQL_SUCCESS_WITH_INFO ou SQL_SUCCESS.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**ou **SQLMoreResults** foi chamado para *ConnectionHandle* e retornou SQL_PARAM_DATA_AVAILABLE. Esta função foi chamada antes de os dados serem recuperados para todos os parâmetros transmitidos.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não puderam ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY090|Comprimento de cadeia de caracteres ou buffer inválido|(DM) * \*ValuePtr* é uma cadeia de caracteres e BufferLength era menor que zero, mas não igual a SQL_NTS.|  
|HY092|Identificador de atributo/opção inválido|O valor especificado para o *atributo* de argumento não era válido para a versão do ODBC com suporte do driver.|  
|HY114|O driver não dá suporte à execução de função assíncrona no nível de conexão|(DM) um aplicativo tentou habilitar a execução de função assíncrona com SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE para um driver que não oferece suporte a operações de conexão assíncronas.|  
|HY117|A conexão foi suspensa devido a um estado de transação desconhecido. Somente funções de desconexão e somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Recurso opcional não implementado|O valor especificado para o *atributo* de argumento era um atributo de conexão ODBC válido para a versão do ODBC com suporte do driver, mas não foi suportado pelo driver.|  
|HYT01|Tempo limite de conexão expirado|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|O driver não oferece suporte a essa função|(DM) o driver que corresponde ao *ConnectionHandle* não oferece suporte à função.|  
  
## <a name="comments"></a>Comentários  
 Para obter informações gerais sobre atributos de conexão, consulte [atributos de conexão](../../../odbc/reference/develop-app/connection-attributes.md).  
  
 Para obter uma lista de atributos que podem ser definidos, consulte [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md). Observe que, se o *atributo* especificar um atributo que retorne uma cadeia de caracteres, *ValuePtr* deverá ser um ponteiro para um buffer para a cadeia de caracteres. O comprimento máximo da cadeia de caracteres retornada, incluindo o caractere de terminação nula, será de *BufferLength* bytes.  
  
 Dependendo do atributo, um aplicativo não precisa estabelecer uma conexão antes de chamar **SQLGetConnectAttr**. No entanto, se **SQLGetConnectAttr** for chamado e o atributo especificado não tiver um padrão e não tiver sido definido por uma chamada anterior para **SQLSetConnectAttr**, **SQLGetConnectAttr** retornará SQL_NO_DATA.  
  
 Se o *atributo* for SQL_ATTR_ trace ou SQL_ATTR_ TraceFile, *ConnectionHandle* não precisará ser válido e **SQLGetConnectAttr** não retornará SQL_ERROR ou SQL_INVALID_HANDLE se *ConnectionHandle* for inválido. Esses atributos se aplicam a todas as conexões. **SQLGetConnectAttr** retornará SQL_ERROR ou SQL_INVALID_HANDLE se outro argumento for inválido.  
  
 Embora um aplicativo possa definir atributos de instrução usando **SQLSetConnectAttr**, um aplicativo não pode usar **SQLGetConnectAttr** para recuperar valores de atributo de instrução; Ele deve chamar **SQLGetStmtAttr** para recuperar a configuração de atributos de instrução.  
  
 Os atributos de conexão SQL_ATTR_AUTO_IPD e SQL_ATTR_CONNECTION_DEAD podem ser retornados por uma chamada para **SQLGetConnectAttr** , mas não podem ser definidos por uma chamada para **SQLSetConnectAttr**.  
  
> [!NOTE]  
>  Não há suporte assíncrono para **SQLGetConnectAttr**. Ao implementar o **SQLGetConnectAttr**, um driver pode melhorar o desempenho, minimizando o número de vezes que as informações são enviadas ou solicitadas do servidor.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Retornando a configuração de um atributo de instrução|[Função SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|  
|Definindo um atributo de conexão|[Função SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|Configurando um atributo de ambiente|[Função SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)|  
|Definindo um atributo de instrução|[Função SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
