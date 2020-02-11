---
title: Função SQLGetEnvAttr | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetEnvAttr
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLGetEnvAttr
helpviewer_keywords:
- SQLGetEnvAttr function [ODBC]
ms.assetid: 01f4590f-427a-4280-a1c3-18de9f7d86c1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0940a5a2c70a7b670ca6a81521759fd08e60461e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68345631"
---
# <a name="sqlgetenvattr-function"></a>Função SQLGetEnvAttr
**Conformidade**  
 Versão introduzida: conformidade de padrões do ODBC 3,0: ISO 92  
  
 **Resumo**  
 **SQLGetEnvAttr** retorna a configuração atual de um atributo de ambiente.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLGetEnvAttr(  
     SQLHENV        EnvironmentHandle,  
     SQLINTEGER     Attribute,  
     SQLPOINTER     ValuePtr,  
     SQLINTEGER     BufferLength,  
     SQLINTEGER *   StringLengthPtr);  
```  
  
## <a name="arguments"></a>Argumentos  
 *EnvironmentHandle*  
 Entrada Identificador de ambiente.  
  
 *Attribute*  
 Entrada Atributo a ser recuperado.  
  
 *ValuePtr*  
 Der Ponteiro para um buffer no qual retornar o valor atual do atributo especificado pelo *atributo*.  
  
 Se *ValuePtr* for NULL, *StringLengthPtr* ainda retornará o número total de bytes (excluindo o caractere de terminação nula para dados de caracteres) disponíveis para retornar no buffer apontado por *ValuePtr*.  
  
 *BufferLength*  
 Entrada Se *ValuePtr* apontar para uma cadeia de caracteres, esse argumento deverá ser o comprimento \*de *ValuePtr*. Se \* *ValuePtr* for um inteiro, *BufferLength* será ignorado. Se * \*ValuePtr* for uma cadeia de caracteres Unicode (ao chamar **SQLGetEnvAttrW**), o argumento *BufferLength* deverá ser um número par. Se o valor do atributo não for uma cadeia de caracteres, *BufferLength* não será usado.  
  
 *StringLengthPtr*  
 Der Um ponteiro para um buffer no qual retornar o número total de bytes (excluindo o caractere de terminação nula) disponível para retornar em * \*ValuePtr*. Se *ValuePtr* for um ponteiro nulo, nenhum comprimento será retornado. Se o valor do atributo for uma cadeia de caracteres e o número de bytes disponíveis para retornar for maior ou igual a *BufferLength*, os dados \*em *ValuePtr* serão truncados para *BufferLength* menos o comprimento de um caractere de terminação nula e serão terminados em nulo pelo driver.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **SQLGetEnvAttr** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido chamando **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_ENV e um *identificador* de *EnvironmentHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLGetEnvAttr** e explica cada um no contexto dessa função; a notação "(DM)" precede as descrições de sqlstates retornadas pelo Gerenciador de driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
|SQLSTATE|Erro|DESCRIÇÃO|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa específica do driver. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|01004|Dados de cadeia de caracteres, truncados à direita|Os dados retornados em \* *ValuePtr* foram truncados para serem *BufferLength* menos o caractere de terminação nula. O comprimento do valor de cadeia de caracteres não truncado é retornado em **StringLengthPtr*. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia um SQLSTATE específico e para o qual nenhum SQLSTATE específico de implementação foi definido. A mensagem de erro retornada por **SQLGetDiagRec** no buffer * \*MessageText* descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar memória necessária para dar suporte à execução ou à conclusão da função.|  
|HY010|Erro de sequência de função|(DM) **SQL_ATTR_ODBC_VERSION** ainda não foi definido via **SQLSetEnvAttr**. Você não precisará definir **SQL_ATTR_ODBC_VERSION** explicitamente se estiver usando **SQLAllocHandleStd**.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não puderam ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY092|Identificador de atributo/opção inválido|O valor especificado para o *atributo* de argumento não era válido para a versão do ODBC com suporte do driver.|  
|HY117|A conexão foi suspensa devido a um estado de transação desconhecido. Somente funções de desconexão e somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Recurso opcional não implementado|O valor especificado para o *atributo* de argumento era um atributo de ambiente ODBC válido para a versão do ODBC com suporte do driver, mas não era suportado pelo driver.|  
|IM001|O driver não oferece suporte a essa função|(DM) o driver correspondente ao *EnvironmentHandle* não oferece suporte à função.|  
  
## <a name="comments"></a>Comentários  
 Para obter uma lista de atributos, consulte [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md). Não há atributos de ambiente específicos do driver. Se o *atributo* especificar um atributo que retorne uma cadeia de caracteres, *ValuePtr* deverá ser um ponteiro para um buffer no qual retornar a cadeia de caracteres. O comprimento máximo da cadeia de caracteres, incluindo o byte de terminação nula, será de *BufferLength* bytes.  
  
 **SQLGetEnvAttr** pode ser chamado a qualquer momento entre a alocação e a liberação de um identificador de ambiente. Todos os atributos de ambiente definidos com êxito pelo aplicativo para o ambiente persistem até que **SQLFreeHandle** seja chamado no *EnvironmentHandle* com um *HandleType* de SQL_HANDLE_ENV. Mais de um identificador de ambiente pode ser alocado simultaneamente no ODBC 3 *. x*. Um atributo de ambiente em um ambiente não é afetado quando outro ambiente foi alocado.  
  
> [!NOTE]
>  O atributo de ambiente SQL_ATTR_OUTPUT_NTS é compatível com aplicativos compatíveis com padrões. Quando **SQLGetEnvAttr** é chamado, o Gerenciador de driver ODBC 3 *. x* sempre retorna SQL_TRUE para esse atributo. SQL_ATTR_OUTPUT_NTS pode ser definido para SQL_TRUE apenas por uma chamada para **SQLSetEnvAttr**.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Retornando a configuração de um atributo de conexão|[Função SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|Retornando a configuração de um atributo de instrução|[Função SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|  
|Definindo um atributo de conexão|[Função SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|Configurando um atributo de ambiente|[Função SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)|  
|Definindo um atributo de instrução|[Função SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
