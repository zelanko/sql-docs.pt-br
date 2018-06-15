---
title: Função SQLGetEnvAttr | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLGetEnvAttr
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetEnvAttr
helpviewer_keywords:
- SQLGetEnvAttr function [ODBC]
ms.assetid: 01f4590f-427a-4280-a1c3-18de9f7d86c1
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b1a31f7d374a06a4e9cfe963c92b73fa681a41d9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32921741"
---
# <a name="sqlgetenvattr-function"></a>Função SQLGetEnvAttr
**Conformidade**  
 Versão introduzidas: Conformidade de padrões 3.0 ODBC: 92 ISO  
  
 **Resumo**  
 **SQLGetEnvAttr** retorna a configuração atual de um atributo de ambiente.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SQLRETURN SQLGetEnvAttr(  
     SQLHENV        EnvironmentHandle,  
     SQLINTEGER     Attribute,  
     SQLPOINTER     ValuePtr,  
     SQLINTEGER     BufferLength,  
     SQLINTEGER *   StringLengthPtr);  
```  
  
## <a name="arguments"></a>Argumentos  
 *EnvironmentHandle*  
 [Entrada] Identificador de ambiente.  
  
 *Atributo*  
 [Entrada] Atributo para recuperar.  
  
 *ValuePtr*  
 [Saída] Ponteiro para um buffer no qual retornar o valor atual do atributo especificado por *atributo*.  
  
 Se *ValuePtr* for NULL, *StringLengthPtr* ainda retornará o número total de bytes (excluindo o caractere null de terminação para dados de caractere) disponíveis para retornar o buffer apontado pelo  *ValuePtr*.  
  
 *BufferLength*  
 [Entrada] Se *ValuePtr* aponta para uma cadeia de caracteres, esse argumento deve ser o comprimento de \* *ValuePtr*. Se \* *ValuePtr* é um inteiro, *BufferLength* será ignorado. Se  *\*ValuePtr* é uma cadeia de caracteres Unicode (ao chamar **SQLGetEnvAttrW**), o *BufferLength* argumento deve ser um número par. Se o valor do atributo não é uma cadeia de caracteres, *BufferLength* é usado.  
  
 *StringLengthPtr*  
 [Saída] Um ponteiro para um buffer no qual retornar o número total de bytes (excluindo o caractere null de terminação) disponíveis para retornar em  *\*ValuePtr*. Se *ValuePtr* é um ponteiro nulo, nenhum comprimento é retornado. Se o valor do atributo é uma cadeia de caracteres e o número de bytes disponíveis para retornar é maior que ou igual a *BufferLength*, os dados em \* *ValuePtr* será truncado para  *BufferLength* menos o comprimento de um caractere null de terminação e é terminada em nulo pelo driver.  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>diagnóstico  
 Quando **SQLGetEnvAttr** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtida chamando **SQLGetDiagRec** com um *HandleType* de SQL _ HANDLE_ENV e um *tratar* de *EnvironmentHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLGetEnvAttr** e explica cada uma no contexto dessa função; a notação "(DM)" precede as descrições de SQLSTATEs retornados pelo Gerenciador de Driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado em contrário.  
  
|SQLSTATE|Erro|Description|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem de informação específica do driver. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|01004|Dados de cadeia de caracteres truncados à direita|Os dados retornados em \* *ValuePtr* foi truncado para ser *BufferLength* menos o caractere null de terminação. O comprimento do valor completo da cadeia de caracteres é retornado em **StringLengthPtr*. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|HY000|Erro geral|Ocorreu um erro para o qual não houve nenhuma SQLSTATE específico e para o qual nenhuma SQLSTATE específicos de implementação foi definida. A mensagem de erro retornada pelo **SQLGetDiagRec** no  *\*MessageText* buffer descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar a memória necessária para dar suporte a execução ou a conclusão da função.|  
|HY010|Erro de sequência de função|(DM) **SQL_ATTR_ODBC_VERSION** ainda não foi definido por meio de **SQLSetEnvAttr**. Você não precisa definir **SQL_ATTR_ODBC_VERSION** explicitamente se você estiver usando **SQLAllocHandleStd**.|  
|HY013|Erro de gerenciamento de memória|Não foi possível processar a chamada de função porque os objetos de memória subjacente não podem ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY092|Identificador de atributo/opção inválido|O valor especificado para o argumento *atributo* não era válido para a versão do ODBC com suporte pelo driver.|  
|HY117|Conexão está suspenso devido ao estado de transação desconhecido. Somente Desconecte e funções de somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Recurso opcional não implementado|O valor especificado para o argumento *atributo* era um atributo de ambiente ODBC válido para a versão do ODBC com suporte pelo driver, mas não era compatível com o driver.|  
|IM001|Driver não dá suporte a esta função|(DM) o driver correspondente a *EnvironmentHandle* não oferece suporte para a função.|  
  
## <a name="comments"></a>Comentários  
 Para obter uma lista de atributos, consulte [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md). Não há nenhum atributo de ambiente específicas do driver. Se *atributo* Especifica um atributo que retorna uma cadeia de caracteres, *ValuePtr* deve ser um ponteiro para um buffer no qual retornar a cadeia de caracteres. O comprimento máximo da cadeia de caracteres, incluindo o byte de terminação null, será *BufferLength* bytes.  
  
 **SQLGetEnvAttr** pode ser chamado a qualquer momento entre a alocação e a liberação de um identificador de ambiente. Todos os atributos de ambiente definidos com êxito pelo aplicativo para o ambiente persistem até **SQLFreeHandle** é chamado no *EnvironmentHandle* com um *HandleType*SQL_HANDLE_ENV. Mais de um identificador de ambiente pode ser alocado simultaneamente em ODBC 3 *. x*. Um atributo de ambiente em um ambiente não é afetado quando outro ambiente foi alocado.  
  
> [!NOTE]  
>  O atributo de ambiente SQL_ATTR_OUTPUT_NTS é suportado por aplicativos compatíveis com os padrões. Quando **SQLGetEnvAttr** é chamado, o ODBC 3 *. x* Gerenciador de Driver sempre retornará SQL_TRUE para esse atributo. SQL_ATTR_OUTPUT_NTS pode ser definido como SQL_TRUE apenas por uma chamada para **SQLSetEnvAttr**.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Retornando a configuração de um atributo de conexão|[Função SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|Retornando a configuração de um atributo de instrução|[Função SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|  
|Definir um atributo de conexão|[Função SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|Definindo um atributo de ambiente|[Função SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)|  
|Definir um atributo de instrução|[Função SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Referência de API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
