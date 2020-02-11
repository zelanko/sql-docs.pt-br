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
ms.openlocfilehash: 31ddab7291807222882050233715d3ad61e25124
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68061459"
---
# <a name="sqlgetstmtattr-function"></a>Função SQLGetStmtAttr
**Conformidade**  
 Versão introduzida: conformidade de padrões do ODBC 3,0: ISO 92  
  
 **Resumo**  
 **SQLGetStmtAttr** retorna a configuração atual de um atributo de instrução.  
  
> [!NOTE]  
>  Para obter mais informações sobre como o Gerenciador de driver mapeia essa função quando um ODBC 3. o aplicativo *x* está funcionando com um ODBC 2. Driver *x* , consulte [mapeando funções de substituição para compatibilidade com versões anteriores de aplicativos](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md).  
  
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
 Entrada Identificador de instrução.  
  
 *Attribute*  
 Entrada Atributo a ser recuperado.  
  
 *ValuePtr*  
 Der Ponteiro para um buffer no qual retornar o valor do atributo especificado em *atributo*.  
  
 Se *ValuePtr* for NULL, *StringLengthPtr* ainda retornará o número total de bytes (excluindo o caractere de terminação nula para dados de caracteres) disponíveis para retornar no buffer apontado por *ValuePtr*.  
  
 *BufferLength*  
 Entrada Se o *atributo* for um atributo definido pelo ODBC e *ValuePtr* apontar para uma cadeia de caracteres ou um buffer binário, esse argumento deverá ter o \*comprimento de *ValuePtr*. Se o *atributo* for um atributo definido pelo ODBC \*e *ValuePtr* for um inteiro, *BufferLength* será ignorado. Se o valor retornado em * \*ValuePtr* for uma cadeia de caracteres Unicode (ao chamar **SQLGetStmtAttrW**), o argumento *BufferLength* deverá ser um número par.  
  
 Se o *atributo* for um atributo definido por Driver, o aplicativo indicará a natureza do atributo para o Gerenciador de driver, definindo o argumento *BufferLength* . *BufferLength* pode ter os seguintes valores:  
  
-   Se * \*ValuePtr* for um ponteiro para uma cadeia de caracteres, *BufferLength* será o comprimento da cadeia de caracteres ou SQL_NTS.  
  
-   Se * \*ValuePtr* for um ponteiro para um buffer binário, o aplicativo colocará o resultado da macro SQL_LEN_BINARY_ATTR (*Length*) em *BufferLength*. Isso coloca um valor negativo em *BufferLength*.  
  
-   Se * \*ValuePtr* for um ponteiro para um valor diferente de uma cadeia de caracteres ou uma cadeia de caracteres binária, *BufferLength* deverá ter o valor SQL_IS_POINTER.  
  
-   Se * \*ValuePtr* contiver um tipo de dados de comprimento fixo, o *BufferLength* será SQL_IS_INTEGER ou SQL_IS_UINTEGER, conforme apropriado.  
  
 *StringLengthPtr*  
 Der Um ponteiro para um buffer no qual retornar o número total de bytes (excluindo o caractere de terminação nula) disponível para retornar em * \*ValuePtr*. Se *ValuePtr* for um ponteiro nulo, nenhum comprimento será retornado. Se o valor do atributo for uma cadeia de caracteres e o número de bytes disponíveis para retornar for maior ou igual a *BufferLength*, os dados em * \*ValuePtr* serão truncados para *BufferLength* menos o comprimento de um caractere de terminação nula e serão terminados em nulo pelo driver.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **SQLGetStmtAttr** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido chamando **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_STMT e um *identificador* de *StatementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLGetStmtAttr** e explica cada um no contexto dessa função; a notação "(DM)" precede as descrições de sqlstates retornadas pelo Gerenciador de driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
|SQLSTATE|Erro|DESCRIÇÃO|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa específica do driver. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|01004|Dados de cadeia de caracteres, truncados à direita|Os dados retornados em * \*ValuePtr* foram truncados para serem *BufferLength* menos o comprimento de um caractere de terminação nula. O comprimento do valor de cadeia de caracteres não truncado é retornado em **StringLengthPtr*. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|24.000|Estado de cursor inválido|O *atributo* de argumento foi SQL_ATTR_ROW_NUMBER e o cursor não estava aberto, ou o cursor foi posicionado antes do início do conjunto de resultados ou após o final do conjunto de resultados.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia um SQLSTATE específico e para o qual nenhum SQLSTATE específico de implementação foi definido. A mensagem de erro retornada por **SQLGetDiagRec** no argumento *MessageText* descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar memória necessária para dar suporte à execução ou à conclusão da função.|  
|HY010|Erro de sequência de função|(DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado ao *StatementHandle*. Esta função assíncrona ainda estava em execução quando a função **SQLGetStmtAttr** foi chamada.<br /><br /> (DM) uma função de execução assíncrona foi chamada para o *StatementHandle* e ainda estava em execução quando essa função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**ou **SQLSetPos** foi chamado para o *StatementHandle* e retornou SQL_NEED_DATA. Esta função foi chamada antes de os dados serem enviados para todos os parâmetros de dados em execução ou colunas.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não puderam ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY090|Comprimento de cadeia de caracteres ou buffer inválido|*(DM) \*ValuePtr* é uma cadeia de caracteres e BufferLength era menor que zero, mas não é igual a SQL_NTS.|  
|HY092|Identificador de atributo/opção inválido|O valor especificado para o *atributo* de argumento não era válido para a versão do ODBC com suporte do driver.|  
|HY109|Posição do cursor inválida|O argumento de *atributo* foi SQL_ATTR_ROW_NUMBER e a linha tinha sido excluída ou não pôde ser buscada.|  
|HY117|A conexão foi suspensa devido a um estado de transação desconhecido. Somente funções de desconexão e somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Recurso opcional não implementado|O valor especificado para o *atributo* de argumento era um atributo de instrução ODBC válido para a versão do ODBC com suporte do driver, mas não foi suportado pelo driver.|  
|HYT01|Tempo limite de conexão expirado|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|O driver não oferece suporte a essa função|(DM) o driver correspondente ao *StatementHandle* não oferece suporte à função.|  
  
## <a name="comments"></a>Comentários  
 Para obter informações gerais sobre atributos de instrução, consulte [atributos de instrução](../../../odbc/reference/develop-app/statement-attributes.md).  
  
 Uma chamada para **SQLGetStmtAttr** retorna em * \*ValuePtr* o valor do atributo de instrução especificado no *atributo*. Esse valor pode ser um valor SQLULEN ou uma cadeia de caracteres terminada em nulo. Se o valor for um valor SQLULEN, alguns drivers só poderão gravar o menor 32 ou 16 bits de um buffer e deixar o bit de ordem superior inalterado. Portanto, os aplicativos devem usar um buffer de SQLULEN e inicializar o valor para 0 antes de chamar essa função. Além disso, os argumentos *BufferLength* e *StringLengthPtr* não são usados. Se o valor for uma cadeia de caracteres terminada em nulo, o aplicativo especificará o comprimento máximo dessa cadeia de caracteres no argumento *BufferLength* e o driver retornará o comprimento dessa cadeia de caracteres no buffer * \*StringLengthPtr* .  
  
 Para permitir que aplicativos que chamam o **SQLGetStmtAttr** funcionem com o ODBC 2. drivers *x* , uma chamada para **SQLGetStmtAttr** é mapeada no Gerenciador de driver para **SQLGetStmtOption**.  
  
 Os seguintes atributos de instrução são somente leitura, portanto, podem ser recuperados por **SQLGetStmtAttr**, mas não definidos por **SQLSetStmtAttr**:  
  
-   SQL_ATTR_IMP_PARAM_DESC  
  
-   SQL_ATTR_IMP_ROW_DESC  
  
-   SQL_ATTR_ROW_NUMBER  
  
 Para obter uma lista de atributos que podem ser definidos e recuperados, consulte [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Retornando a configuração de um atributo de conexão|[Função SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|Definindo um atributo de conexão|[Função SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|Definindo um atributo de instrução|[Função SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
