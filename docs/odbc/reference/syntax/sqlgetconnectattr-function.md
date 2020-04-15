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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285626"
---
# <a name="sqlgetconnectattr-function"></a>Função SQLGetConnectAttr
**Conformidade**  
 Versão introduzida: ODBC 3.0 Standards Compliance: ISO 92  
  
 **Resumo**  
 **SQLGetConnectAttr** retorna a configuração atual de um atributo de conexão.  
  
> [!NOTE]
>  Para obter mais informações sobre o que o Driver Manager mapeia essa função para quando um aplicativo ODBC 3 *.x* estiver trabalhando com um driver ODBC*2.x,* consulte [Funções de substituição de mapeamento para compatibilidade retrógrada de aplicativos](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md).  
  
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
 *ConexãoHandle*  
 [Entrada] Identificador de conexão.  
  
 *Atributo*  
 [Entrada] Atributo para recuperar.  
  
 *ValuePtr*  
 [Saída] Um ponteiro para a memória no qual retornar o valor atual do atributo especificado por *Atributo*. Para atributos do tipo inteiro, alguns drivers podem apenas gravar o buffer de 32 bits ou 16 bits inferiores e deixar o bit de ordem superior inalterado. Portanto, os aplicativos devem usar um buffer de SQLULEN e inicializar o valor para 0 antes de chamar essa função.  
  
 Se *o ValuePtr* for NULL, *stringLengthLengthr* ainda retornará o número total de bytes (excluindo o caractere de rescisão nula para dados de caracteres) disponível para retornar no buffer apontado pelo *ValuePtr*.  
  
 *BufferLength*  
 [Entrada] Se *Atributo* for um atributo definido pelo ODBC e *o ValuePtr* aponta para \*uma seqüência de caracteres ou um buffer binário, esse argumento deve ser o comprimento do *ValuePtr*. Se *Atributo* for um atributo \*definido pelo ODBC e *o ValuePtr* for um inteiro, *bufferLength* será ignorado. Se o valor no * \*ValuePtr* for uma seqüência unicode (ao chamar **SQLGetConnectAttrW),** o argumento *BufferLength* deve ser um número uniforme.  
  
 Se *Atributo* for um atributo definido pelo driver, o aplicativo indicará a natureza do atributo ao Gerenciador de driver, definindo o argumento *BufferLength.* *BufferLength* pode ter os seguintes valores:  
  
-   Se * \*ValuePtr* é um ponteiro para uma seqüência de caracteres, *BufferLength* é o comprimento da seqüência.  
  
-   Se * \*ValuePtr* for um ponteiro para um buffer binário, o aplicativo coloca o resultado da macro SQL_LEN_BINARY_ATTR *(comprimento)* em *BufferLength*. Isso coloca um valor negativo em *BufferLength*.  
  
-   Se * \*ValuePtr* for um ponteiro para um valor diferente de uma seqüência de caracteres ou string binária, *BufferLength* deve ter o valor SQL_IS_POINTER.  
  
-   Se * \*o ValuePtr* contiver um tipo de dados de comprimento fixo, *bufferLength* será SQL_IS_INTEGER ou SQL_IS_UINTEGER, conforme apropriado.  
  
 *StringLengthPtr*  
 [Saída] Um ponteiro para um buffer no qual retornar o número total de bytes (excluindo o caractere de rescisão nula) disponível para retornar em \* *ValuePtr*. Se \* *ValuePtr* for um ponteiro nulo, nenhum comprimento será retornado. Se o valor do atributo for uma seqüência de caracteres e o número de bytes disponíveis para retornar for maior que *bufferLength* menos o comprimento do caractere de rescisão nula, os dados no * \*ValuePtr* são truncados para *BufferLength* menos o comprimento do caractere de rescisão nula e são nulos pelo driver.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **o SQLGetConnectAttr** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido a partir da estrutura de dados de diagnóstico ligando para **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_DBC e uma *alça* de *ConnectionHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLGetConnectAttr** e explica cada um no contexto desta função; a notação "(DM)" precede as descrições de SQLSTATEs devolvidas pelo Driver Manager. O código de devolução associado a cada valor SQLSTATE é SQL_ERROR, a menos que seja observado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informacional específica do motorista. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|01004|Dados de cordas, truncados direito|Os dados retornados no \* *ValuePtr* foram truncados para serem *BufferLength* menos o comprimento de um caractere de rescisão nula. O comprimento do valor da seqüência não truncado é devolvido em **StringLengthLengthPtr*. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|08003|Conexão não aberta|(DM) Um valor *de atributo* que exigia uma conexão aberta foi especificado.|  
|08S01|Falha no link de comunicação|O link de comunicação entre o driver e a fonte de dados à qual o driver estava conectado falhou antes da função ser concluída.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia SQLSTATE específico e para o qual não foi definido sqlSTATE específico para a implementação. A mensagem de erro retornada da estrutura de dados de diagnóstico pelo argumento *MessageText* no **SQLGetDiagField** descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não conseguiu alocar memória necessária para suportar a execução ou a conclusão da função.|  
|HY010|Erro de seqüência de função|(DM) **O SQLBrowseConnect** foi chamado para o *ConnectionHandle* e retornou SQL_NEED_DATA. Esta função foi chamada antes **do SQLBrowseConnect** retornar SQL_SUCCESS_WITH_INFO ou SQL_SUCCESS.<br /><br /> (DM) **SQLExecute,** **SQLExecDirect**ou **SQLMoreResults** foram chamados para o *ConnectionHandle* e retornaram SQL_PARAM_DATA_AVAILABLE. Esta função foi chamada antes de os dados serem recuperados para todos os parâmetros transmitidos.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não podiam ser acessados, possivelmente devido às baixas condições de memória.|  
|HY090|Comprimento de seqüência ou buffer inválido|(DM) * \*ValuePtr* é uma seqüência de caracteres, e BufferLength era menor que zero, mas não igual a SQL_NTS.|  
|HY092|Identificador de atributo/opção inválido|O valor especificado para o *atributo argumentdo* não era válido para a versão do ODBC suportada pelo driver.|  
|HY114|O driver não suporta a execução de função assíncrona em nível de conexão|(DM) Um aplicativo tentou habilitar a execução de funções assíncronas com SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE para um driver que não suporta operações de conexão assíncronas.|  
|HY117|A conexão está suspensa devido ao estado de transação desconhecido. Somente funções desconectadas e somente leitura são permitidas.|(DM) Para obter mais informações sobre o estado suspenso, consulte [a função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Recurso opcional não implementado|O valor especificado para o *atributo argumental* era um atributo de conexão ODBC válido para a versão do ODBC suportado pelo driver, mas não foi suportado pelo driver.|  
|HYT01|Tempo de tempo de conexão expirado|O período de tempo de tempo de conexão expirou antes que a fonte de dados respondesse à solicitação. O período de tempo de tempo de conexão é definido através **de SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não suporta esta função|(DM) O driver que corresponde ao *ConnectionHandle* não suporta a função.|  
  
## <a name="comments"></a>Comentários  
 Para obter informações gerais sobre atributos de conexão, consulte [Atributos de conexão](../../../odbc/reference/develop-app/connection-attributes.md).  
  
 Para obter uma lista de atributos que podem ser definidos, consulte [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md). Observe que se *Atributo* especificar um atributo que retorna uma seqüência de string, *ValuePtr* deve ser um ponteiro para um buffer para a seqüência de string. O comprimento máximo da seqüência retornada, incluindo o caractere de rescisão nula, será *bufferLength* bytes.  
  
 Dependendo do atributo, um aplicativo não precisa estabelecer uma conexão antes de ligar para **o SQLGetConnectAttr**. No entanto, se **SQLGetConnectAttr** for chamado e o atributo especificado não tiver um padrão e não tiver sido definido por uma chamada anterior ao **SQLSetConnectAttr,** **o SQLGetConnectAttr** retornará SQL_NO_DATA.  
  
 Se *o Atributo* estiver SQL_ATTR_ TRACE ou SQL_ATTR_ TRACEFILE, *o ConnectionHandle* não precisa ser válido e **o SQLGetConnectAttr** não retornará SQL_ERROR ou SQL_INVALID_HANDLE se *o ConnectionHandle* for inválido. Esses atributos se aplicam a todas as conexões. **O SQLGetConnectAttr** retornará SQL_ERROR ou SQL_INVALID_HANDLE se outro argumento for inválido.  
  
 Embora um aplicativo possa definir atributos de declaração usando **SQLSetConnectAttr,** um aplicativo não pode usar **SQLGetConnectAttr** para recuperar valores de atributos de declaração; ele deve chamar **SQLGetStmtAttr** para recuperar a configuração dos atributos de declaração.  
  
 Tanto SQL_ATTR_AUTO_IPD quanto SQL_ATTR_CONNECTION_DEAD atributos de conexão podem ser retornados por uma chamada para **SQLGetConnectAttr,** mas não podem ser definidos por uma chamada para **SQLSetConnectAttr**.  
  
> [!NOTE]  
>  Não há suporte assíncrono para **SQLGetConnectAttr**. Ao implementar **o SQLGetConnectAttr,** um driver pode melhorar o desempenho minimizando o número de vezes que as informações são enviadas ou solicitadas do servidor.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Retornando a configuração de um atributo de declaração|[Função SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|  
|Definindo um atributo de conexão|[Função SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|Definindo um atributo de ambiente|[Função SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)|  
|Definindo um atributo de declaração|[Função SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API oDBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
