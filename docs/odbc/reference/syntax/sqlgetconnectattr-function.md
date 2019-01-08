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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4a24ccf58a1cd0f6d0f4fb2fd32dbee79feb896b
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53204435"
---
# <a name="sqlgetconnectattr-function"></a>Função SQLGetConnectAttr
**Conformidade com**  
 Versão introduzida: Conformidade com padrões 3.0 ODBC: ISO 92  
  
 **Resumo**  
 **SQLGetConnectAttr** retorna a configuração atual de um atributo de conexão.  
  
> [!NOTE]
>  Para obter mais informações sobre o que o Gerenciador de Driver mapeia essa função quando um ODBC 3 *. x* aplicativo está funcionando com um ODBC 2 *. x* driver, consulte [funções de mapeamento de substituição para trás Compatibilidade de aplicativos](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md).  
  
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
 [Entrada] Atributo a ser recuperado.  
  
 *ValuePtr*  
 [Saída] Um ponteiro de memória no qual retornar o valor atual do atributo especificado por *atributo*. Para atributos de tipo de inteiro, alguns drivers podem apenas gravar inferior 32 bits ou o bit de ordem superior de 16 bits de um buffer e deixar inalterado. Portanto, os aplicativos devem usar um buffer de SQLULEN e inicializar o valor para 0 antes de chamar essa função.  
  
 Se *ValuePtr* for NULL, *StringLengthPtr* ainda retornará o número total de bytes (exceto o caractere nulo de terminação para dados de caracteres) disponíveis para retornar no buffer apontado por  *ValuePtr*.  
  
 *BufferLength*  
 [Entrada] Se *atributo* é um atributo definido pelo ODBC e *ValuePtr* aponta para uma cadeia de caracteres ou um buffer de binário, este argumento deve ser o comprimento da \* *ValuePtr*. Se *atributo* é um atributo definido pelo ODBC e \* *ValuePtr* é um inteiro, *BufferLength* será ignorado. Se o valor em  *\*ValuePtr* é uma cadeia de caracteres Unicode (ao chamar **SQLGetConnectAttrW**), o *BufferLength* argumento deve ser um número par.  
  
 Se *atributo* é um atributo definido pelo driver, o aplicativo indica a natureza do atributo para o Gerenciador de Driver, definindo o *BufferLength* argumento. *BufferLength* pode ter os seguintes valores:  
  
-   Se  *\*ValuePtr* é um ponteiro para uma cadeia de caracteres *BufferLength* é o comprimento da cadeia de caracteres.  
  
-   Se  *\*ValuePtr* é um ponteiro para um buffer de binário, o aplicativo coloca o resultado do SQL_LEN_BINARY_ATTR (*comprimento*) macro na *BufferLength*. Isso coloca um valor negativo em *BufferLength*.  
  
-   Se  *\*ValuePtr* é um ponteiro para um valor diferente de uma cadeia de caracteres ou cadeia de caracteres binária *BufferLength* deve ter o valor SQL_IS_POINTER.  
  
-   Se  *\*ValuePtr* contém um tipo de dados de comprimento fixo *BufferLength* é SQL_IS_INTEGER ou SQL_IS_UINTEGER, conforme apropriado.  
  
 *StringLengthPtr*  
 [Saída] Um ponteiro para um buffer no qual retornar o número total de bytes (exceto o caractere nulo de terminação) disponíveis para retornar na \* *ValuePtr*. Se \* *ValuePtr* for um ponteiro nulo, nenhum tamanho é retornado. Se o valor do atributo é uma cadeia de caracteres e o número de bytes disponíveis para retornar é maior que *BufferLength* menos o comprimento do caractere nulo de terminação, os dados no  *\*ValuePtr*será truncado com *BufferLength* menos o comprimento do caractere nulo de terminação e é terminada em nulo pelo driver.  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLGetConnectAttr** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtida da estrutura de dados de diagnóstico chamando **SQLGetDiagRec** com um *HandleType* SQL_HANDLE_DBC e uma *tratar* de *ConnectionHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLGetConnectAttr** e explica cada uma no contexto dessa função; a notação "(DM)" precede as descrições das SQLSTATEs retornados pelo Gerenciador de Driver . O código de retorno associado com cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa de específicos do driver. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|01004|Dados de cadeia de caracteres truncados à direita|Os dados retornados \* *ValuePtr* foi truncado para ser *BufferLength* menos o comprimento de um caractere nulo de terminação. O comprimento do valor completo da cadeia de caracteres é retornado no **StringLengthPtr*. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|08003|Conexão não aberta|(DM) uma *atributo* valor que é necessária uma conexão aberta foi especificado.|  
|08S01|Falha de link de comunicação|Falha do link de comunicação entre o driver e a fonte de dados ao qual o driver foi conectado antes do processamento da função foi concluída.|  
|HY000|Erro geral|Ocorreu um erro para o qual não houve nenhum SQLSTATE específico e para o qual não foi definida nenhuma SQLSTATE específicos de implementação. A mensagem de erro retornado da estrutura de dados de diagnóstico pelo argumento *MessageText* na **SQLGetDiagField** descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar memória necessária para dar suporte à execução ou a conclusão da função.|  
|HY010|Erro de sequência de função|(DM) **SQLBrowseConnect** foi chamado para o *ConnectionHandle* e retornados de SQL_NEED_DATA. Essa função foi chamada antes de **SQLBrowseConnect** retornado SQL_SUCCESS_WITH_INFO ou SQL_SUCCESS.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, ou **SQLMoreResults** foi chamado para o *ConnectionHandle* e retornado SQL_PARAM_DATA_ DISPONÍVEL. Essa função foi chamada antes de dados foram recuperados para todos os parâmetros transmitidos.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacente não pôde ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY090|Comprimento de buffer ou cadeia de caracteres inválido|(DM)  *\*ValuePtr* é uma cadeia de caracteres e BufferLength era menor que zero, mas não é igual a SQL_NTS.|  
|HY092|Identificador de atributo/opção inválido|O valor especificado para o argumento *atributo* não era válido para a versão do ODBC com suporte pelo driver.|  
|HY114|Driver não oferece suporte à execução de função de nível de conexão assíncrona|Tentativa de um aplicativo (DM) habilitar a execução de função assíncrona com SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE um driver que não dá suporte a operações de conexão assíncrona.|  
|HY117|Conexão está suspenso devido ao estado de transação desconhecida. Somente se desconectar e funções de somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Recurso opcional não implementado|O valor especificado para o argumento *atributo* foi um atributo de conexão ODBC válido para a versão do ODBC com suporte pelo driver, mas não tinha suporte pelo driver.|  
|HYT01|Tempo limite da Conexão expirado|O período de tempo limite de conexão expirado antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não oferece suporte a essa função|(DM) o driver que corresponde do *ConnectionHandle* não suporta a função.|  
  
## <a name="comments"></a>Comentários  
 Para obter informações gerais sobre os atributos de conexão, consulte [atributos de Conexão](../../../odbc/reference/develop-app/connection-attributes.md).  
  
 Para obter uma lista de atributos que podem ser definidas, consulte [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md). Observe que, se *atributo* Especifica um atributo que retorna uma cadeia de caracteres *ValuePtr* deve ser um ponteiro para um buffer para a cadeia de caracteres. O comprimento máximo da cadeia de caracteres retornada, incluindo o caractere de terminação null, serão *BufferLength* bytes.  
  
 Dependendo do atributo, um aplicativo não precisa estabelecer uma conexão antes de chamar **SQLGetConnectAttr**. No entanto, se **SQLGetConnectAttr** é chamado e o atributo especificado não tem um padrão e não tiver sido definido por uma chamada anterior a **SQLSetConnectAttr**, **SQLGetConnectAttr**irá retornar SQL_NO_DATA.  
  
 Se *atributo* é sql_attr TRACEFILE, ou rastreamento sql_attr *ConnectionHandle* não precisa ser válido, e **SQLGetConnectAttr** não retornará SQL_ERROR ou SQL _ INVALID_HANDLE se *ConnectionHandle* é inválido. Esses atributos se aplicam a todas as conexões. **SQLGetConnectAttr** retornará SQL_ERROR ou SQL_INVALID_HANDLE se outro argumento é inválido.  
  
 Embora um aplicativo pode definir atributos de instrução usando **SQLSetConnectAttr**, um aplicativo não é possível usar **SQLGetConnectAttr** recuperar o atributo de instrução valores; ele deve chamar  **SQLGetStmtAttr** para recuperar a configuração de atributos de instrução.  
  
 Atributos de conexão SQL_ATTR_AUTO_IPD e SQL_ATTR_CONNECTION_DEAD podem ser retornados por uma chamada para **SQLGetConnectAttr** , mas não pode ser definido por uma chamada para **SQLSetConnectAttr**.  
  
> [!NOTE]  
>  Não há suporte assíncrono para **SQLGetConnectAttr**. Ao implementar **SQLGetConnectAttr**, um driver pode melhorar o desempenho, minimizando o número de vezes que a informação é enviada ou solicitada do servidor.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Retornando a configuração de um atributo de instrução|[Função SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|  
|Definir um atributo de conexão|[Função SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|Definindo um atributo de ambiente|[Função SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)|  
|Definir um atributo de instrução|[Função SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
