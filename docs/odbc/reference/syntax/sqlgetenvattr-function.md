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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 77cd24386a8eea6769aee59f3674b681c516d9ed
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285306"
---
# <a name="sqlgetenvattr-function"></a>Função SQLGetEnvAttr
**Conformidade**  
 Versão introduzida: ODBC 3.0 Standards Compliance: ISO 92  
  
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
 [Entrada] Alça do meio ambiente.  
  
 *Atributo*  
 [Entrada] Atributo para recuperar.  
  
 *ValuePtr*  
 [Saída] Ponteiro para um buffer no qual para retornar o valor atual do atributo especificado por *Atributo*.  
  
 Se *o ValuePtr* for NULL, *stringLengthLengthr* ainda retornará o número total de bytes (excluindo o caractere de rescisão nula para dados de caracteres) disponível para retornar no buffer apontado pelo *ValuePtr*.  
  
 *BufferLength*  
 [Entrada] Se *ValuePtr* aponta para uma seqüência de \*caracteres, este argumento deve ser o comprimento do *ValuePtr*. Se \* *ValuePtr* for um inteiro, *bufferLength* será ignorado. Se * \*ValuePtr* for uma seqüência unicode (ao chamar **SQLGetEnvAttrW),** o argumento *BufferLength* deve ser um número uniforme. Se o valor do atributo não for uma seqüência de caracteres, *BufferLength* não será usado.  
  
 *StringLengthPtr*  
 [Saída] Um ponteiro para um buffer no qual retornar o número total de bytes (excluindo o caractere de rescisão nula) disponível para retornar em * \*ValuePtr*. Se *ValuePtr* for um ponteiro nulo, nenhum comprimento será retornado. Se o valor do atributo for uma seqüência de caracteres e o número \*de bytes disponíveis para retornar for maior ou igual a *BufferLength,* os dados no *ValuePtr* são truncados para *BufferLength* menos o comprimento de um caractere de rescisão nula e são nulos pelo driver.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **o SQLGetEnvAttr** retornar SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido ligando para **sqlGetDiagRec** com um *HandleType* de SQL_HANDLE_ENV e uma *alça* de *EnvironmentHandle*. A tabela a seguir lista os valores SQLSTATE comumente retornados por **SQLGetEnvAttr** e explica cada um no contexto desta função; a notação "(DM)" precede as descrições de SQLSTATEs devolvidas pelo Driver Manager. O código de devolução associado a cada valor SQLSTATE é SQL_ERROR, a menos que seja observado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informacional específica do motorista. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|01004|Dados de cordas, truncados direito|Os dados retornados no \* *ValuePtr* foram truncados para serem *BufferLength* menos o caractere de rescisão nula. O comprimento do valor da seqüência não truncado é devolvido em **StringLengthLengthPtr*. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia SQLSTATE específico e para o qual não foi definido sqlSTATE específico para a implementação. A mensagem de erro retornada pelo **SQLGetDiagRec** no * \** buffer MessageText descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não conseguiu alocar a memória necessária para suportar a execução ou a conclusão da função.|  
|HY010|Erro de seqüência de função|(DM) **SQL_ATTR_ODBC_VERSION** ainda não foi definido via **SQLSetEnvAttr**. Você não precisa definir **SQL_ATTR_ODBC_VERSION** explicitamente se estiver usando **SQLAllocHandleStd**.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não podiam ser acessados, possivelmente devido às baixas condições de memória.|  
|HY092|Identificador de atributo/opção inválido|O valor especificado para o *atributo argumentdo* não era válido para a versão do ODBC suportada pelo driver.|  
|HY117|A conexão está suspensa devido ao estado de transação desconhecido. Somente funções desconectadas e somente leitura são permitidas.|(DM) Para obter mais informações sobre o estado suspenso, consulte [a função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Recurso opcional não implementado|O valor especificado para o *atributo de* argumento foi um atributo de ambiente ODBC válido para a versão do ODBC suportado pelo driver, mas não foi suportado pelo driver.|  
|IM001|Driver não suporta esta função|(DM) O driver correspondente ao *EnvironmentHandle* não suporta a função.|  
  
## <a name="comments"></a>Comentários  
 Para obter uma lista de atributos, consulte [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md). Não há atributos de ambiente específicos para o motorista. Se *Atributo* especificar um atributo que retorna uma seqüência de string, *ValuePtr* deve ser um ponteiro para um buffer no qual para retornar a seqüência. O comprimento máximo da seqüência, incluindo o byte de rescisão nula, será *bufferLength* bytes.  
  
 **SQLGetEnvAttr** pode ser chamado a qualquer momento entre a alocação e a liberação de uma alça de ambiente. Todos os atributos do ambiente definidos com sucesso pelo aplicativo para o ambiente persistem até que o **SQLFreeHandle** seja chamado no *EnvironmentHandle* com um *HandleType* de SQL_HANDLE_ENV. Mais de uma alça de ambiente pode ser alocada simultaneamente em ODBC 3 *.x*. Um atributo ambiental em um ambiente não é afetado quando outro ambiente foi alocado.  
  
> [!NOTE]
>  O SQL_ATTR_OUTPUT_NTS atributo ambiente é suportado por aplicativos compatíveis com padrões. Quando **o SQLGetEnvAttr** é chamado, o ODBC 3 *.x* Driver Manager sempre retorna SQL_TRUE para esse atributo. SQL_ATTR_OUTPUT_NTS pode ser definido como SQL_TRUE apenas por uma chamada para **SQLSetEnvAttr**.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Retornando a configuração de um atributo de conexão|[Função SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|Retornando a configuração de um atributo de declaração|[Função SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|  
|Definindo um atributo de conexão|[Função SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|Definindo um atributo de ambiente|[Função SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)|  
|Definindo um atributo de declaração|[Função SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API oDBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
