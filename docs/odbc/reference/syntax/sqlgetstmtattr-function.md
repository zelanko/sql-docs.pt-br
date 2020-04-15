---
title: Função SQLGetStsttAttr | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 89e7c75b412a6358806017102915989a8370dd43
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303300"
---
# <a name="sqlgetstmtattr-function"></a>Função SQLGetStmtAttr
**Conformidade**  
 Versão introduzida: ODBC 3.0 Standards Compliance: ISO 92  
  
 **Resumo**  
 **SQLGetStmtAttr** retorna a configuração atual de um atributo de declaração.  
  
> [!NOTE]  
>  Para obter mais informações sobre o que o Driver Manager mapeia essa função para quando um ODBC 3. *x* aplicativo está trabalhando com um ODBC 2. *x* driver, consulte [Funções de substituição de mapeamento para compatibilidade retrógrada de aplicativos](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md).  
  
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
 [Entrada] Alça de declaração.  
  
 *Atributo*  
 [Entrada] Atributo para recuperar.  
  
 *ValuePtr*  
 [Saída] Ponteiro para um buffer no qual devolver o valor do atributo especificado em *Atributo*.  
  
 Se *o ValuePtr* for NULL, *stringLengthLengthr* ainda retornará o número total de bytes (excluindo o caractere de rescisão nula para dados de caracteres) disponível para retornar no buffer apontado pelo *ValuePtr*.  
  
 *BufferLength*  
 [Entrada] Se *Atributo* for um atributo definido pelo ODBC e *o ValuePtr* aponta para \*uma seqüência de caracteres ou um buffer binário, esse argumento deve ser o comprimento do *ValuePtr*. Se *Atributo* for um atributo \*definido pelo ODBC e *o ValuePtr* for um inteiro, *bufferLength* será ignorado. Se o valor retornado no * \*ValuePtr* for uma seqüência unicode (ao chamar **SQLGetStmtAttrW),** o argumento *BufferLength* deve ser um número uniforme.  
  
 Se *Atributo* for um atributo definido pelo driver, o aplicativo indicará a natureza do atributo ao Gerenciador de driver, definindo o argumento *BufferLength.* *BufferLength* pode ter os seguintes valores:  
  
-   Se * \*ValuePtr* é um ponteiro para uma seqüência de caracteres, então *BufferLength* é o comprimento da seqüência ou SQL_NTS.  
  
-   Se * \*ValuePtr* for um ponteiro para um buffer binário, o aplicativo coloca o resultado da macro SQL_LEN_BINARY_ATTR *(comprimento)* em *BufferLength*. Isso coloca um valor negativo em *BufferLength*.  
  
-   Se * \*ValuePtr* é um ponteiro para um valor diferente de uma seqüência de caracteres ou string binária, então *BufferLength* deve ter o valor SQL_IS_POINTER.  
  
-   Se * \*O ValuePtr* estiver contiver um tipo de dados de comprimento fixo, o *BufferLength* será SQL_IS_INTEGER ou SQL_IS_UINTEGER, conforme apropriado.  
  
 *StringLengthPtr*  
 [Saída] Um ponteiro para um buffer no qual retornar o número total de bytes (excluindo o caractere de rescisão nula) disponível para retornar em * \*ValuePtr*. Se *ValuePtr* for um ponteiro nulo, nenhum comprimento será retornado. Se o valor do atributo for uma seqüência de caracteres e o número de bytes disponíveis para retornar for maior ou igual a *BufferLength,* os dados no * \*ValuePtr* são truncados para *BufferLength* menos o comprimento de um caractere de rescisão nula e são nulos pelo driver.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **o SQLGetStmtAttr** retornar SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido ligando para **sqlGetDiagRec** com um *HandleType* de SQL_HANDLE_STMT e uma *alça* de *statementhandle*. A tabela a seguir lista os valores SQLSTATE comumente retornados por **SQLGetStmtAttr** e explica cada um no contexto desta função; a notação "(DM)" precede as descrições de SQLSTATEs devolvidas pelo Driver Manager. O código de devolução associado a cada valor SQLSTATE é SQL_ERROR, a menos que seja observado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informacional específica do motorista. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|01004|Dados de cordas, truncados direito|Os dados retornados no * \*ValuePtr* foram truncados para serem *BufferLength* menos o comprimento de um caractere de rescisão nula. O comprimento do valor da seqüência não truncado é devolvido em **StringLengthLengthPtr*. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|24.000|Estado de cursor inválido|O *atributo argumentário* foi SQL_ATTR_ROW_NUMBER e o cursor não estava aberto, ou o cursor foi posicionado antes do início do conjunto de resultados ou após o término do conjunto de resultados.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia SQLSTATE específico e para o qual não foi definido sqlSTATE específico para a implementação. A mensagem de erro retornada pelo **SQLGetDiagRec** no argumento *MessageText* descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não conseguiu alocar a memória necessária para suportar a execução ou a conclusão da função.|  
|HY010|Erro de seqüência de função|(DM) Uma função de execução assíncrona foi chamada para o cabo de conexão associado ao *StatementHandle*. Esta função assíncrona ainda estava sendo executada quando a função **SQLGetStmtAttr** foi chamada.<br /><br /> (DM) Uma função de execução assíncrona foi chamada para o *StatementHandle* e ainda estava sendo executada quando esta função foi chamada.<br /><br /> (DM) **SQLExecute,** **SQLExecDirect,** **SQLBulkOperations**ou **SQLSetPos** foram chamados para o *StatementHandle* e retornaram SQL_NEED_DATA. Essa função foi chamada antes de os dados serem enviados para todos os parâmetros ou colunas de execução de dados.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não podiam ser acessados, possivelmente devido às baixas condições de memória.|  
|HY090|Comprimento de seqüência ou buffer inválido|*(DM) \*ValuePtr* é uma seqüência de caracteres, e BufferLength era menor que zero, mas não igual a SQL_NTS.|  
|HY092|Identificador de atributo/opção inválido|O valor especificado para o *atributo argumentdo* não era válido para a versão do ODBC suportada pelo driver.|  
|HY109|Posição do cursor inválido|O argumento *Atributo* foi SQL_ATTR_ROW_NUMBER e a linha foi excluída ou não pôde ser buscada.|  
|HY117|A conexão está suspensa devido ao estado de transação desconhecido. Somente funções desconectadas e somente leitura são permitidas.|(DM) Para obter mais informações sobre o estado suspenso, consulte [a função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Recurso opcional não implementado|O valor especificado para o *atributo de* argumento foi um atributo de declaração ODBC válido para a versão do ODBC suportado pelo driver, mas não foi suportado pelo driver.|  
|HYT01|Tempo de tempo de conexão expirado|O período de tempo de tempo de conexão expirou antes que a fonte de dados respondesse à solicitação. O período de tempo de tempo de conexão é definido através **de SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não suporta esta função|(DM) O driver correspondente ao *StatementHandle* não suporta a função.|  
  
## <a name="comments"></a>Comentários  
 Para obter informações gerais sobre atributos de declaração, consulte [Atributos de declaração](../../../odbc/reference/develop-app/statement-attributes.md).  
  
 Uma chamada para **SQLGetStmtAttr** retorna no * \*ValuePtr* o valor do atributo de declaração especificado em *Atributo*. Esse valor pode ser um valor SQLULEN ou uma seqüência de caracteres com término nulo. Se o valor for um valor SQLULEN, alguns drivers só podem gravar o buffer de 32 bits ou 16 bits inferiores e deixar o bit de ordem superior inalterado. Portanto, os aplicativos devem usar um buffer de SQLULEN e inicializar o valor para 0 antes de chamar essa função. Além disso, os argumentos *BufferLength* e *StringLengthPtr* não são usados. Se o valor for uma seqüência de seqüência de terminadas por nulo, o aplicativo especificará o comprimento máximo dessa string no argumento *BufferLength* e o driver retorna o comprimento dessa string no buffer * \*StringLengthPtr.*  
  
 Para permitir que aplicativos chamados **SQLGetStmtAttr** funcionem com o ODBC 2. *x* drivers, uma chamada para **SQLGetStmtAttr** é mapeada no Driver Manager para **SQLGetStmtOption**.  
  
 Os atributos de declaração a seguir são somente leitura, portanto podem ser recuperados por **SQLGetStmtAttr,** mas não definidos por **SQLSetStmtAttr**:  
  
-   SQL_ATTR_IMP_PARAM_DESC  
  
-   SQL_ATTR_IMP_ROW_DESC  
  
-   SQL_ATTR_ROW_NUMBER  
  
 Para obter uma lista de atributos que podem ser definidos e recuperados, consulte [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Retornando a configuração de um atributo de conexão|[Função SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|Definindo um atributo de conexão|[Função SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|Definindo um atributo de declaração|[Função SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API oDBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
