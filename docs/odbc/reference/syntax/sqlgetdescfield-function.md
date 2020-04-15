---
title: Função SQLGetDescField | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetDescField
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetDescField
helpviewer_keywords:
- SQLGetDescField function [ODBC]
ms.assetid: f09ff660-1e4a-4370-be85-90d4da0487d3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 89972d7f36b436868cc8e243b03827f095b90492
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285470"
---
# <a name="sqlgetdescfield-function"></a>Função SQLGetDescField
**Conformidade**  
 Versão introduzida: ODBC 3.0 Standards Compliance: ISO 92  
  
 **Resumo**  
 **SQLGetDescField** retorna a configuração atual ou o valor de um único campo de um registro descritor.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLGetDescField(  
     SQLHDESC        DescriptorHandle,  
     SQLSMALLINT     RecNumber,  
     SQLSMALLINT     FieldIdentifier,  
     SQLPOINTER      ValuePtr,  
     SQLINTEGER      BufferLength,  
     SQLINTEGER *    StringLengthPtr);  
```  
  
## <a name="arguments"></a>Argumentos  
 *DescriptorHandle*  
 [Entrada] Alça do descritor.  
  
 *RecNumber*  
 [Entrada] Indica o registro do descritor a partir do qual o aplicativo busca informações. Os registros do descritor são numerados de 0, com o número recorde 0 sendo o recorde do marcador. Se o argumento *FieldIdentifier* indicar um campo de cabeçalho, *O Número de Redoe* será ignorado. Se *RecNumber* for menor ou igual a SQL_DESC_COUNT mas a linha não contiver dados para uma coluna ou parâmetro, uma chamada para **SQLGetDescField** retornará os valores padrão dos campos. (Para obter mais informações, consulte "Inicialização de campos de descritores" em [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).)  
  
 *FieldIdentifier*  
 [Entrada] Indica o campo do descritor cujo valor deve ser devolvido. Para obter mais informações, consulte a seção *"FieldIdentifier* Argument" no [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).  
  
 *ValuePtr*  
 [Saída] Ponteiro para um buffer no qual para retornar as informações do descritor. O tipo de dados depende do valor do *FieldIdentifier*.  
  
 Se *o ValuePtr* for do tipo inteiro, os aplicativos devem usar um buffer de SQLULEN e inicializar o valor para 0 antes de chamar essa função, pois alguns drivers só podem gravar o buffer de 32 bits ou 16 bits inferiores e deixar o bit de ordem superior inalterado.  
  
 Se *o ValuePtr* for NULL, *stringLengthLengthr* ainda retornará o número total de bytes (excluindo o caractere de rescisão nula para dados de caracteres) disponível para retornar no buffer apontado pelo *ValuePtr*.  
  
 *BufferLength*  
 [Entrada] Se *fieldIdentifier* é um campo definido pelo ODBC e *ValuePtr* aponta para uma seqüência de caracteres ou um buffer binário, esse argumento deve ser o comprimento do \* *ValuePtr*. Se *FieldIdentifier* é um campo definido \*pelo ODBC e *o ValuePtr* é um inteiro, *bufferLength* será ignorado. Se o valor no * \*ValuePtr* for de um tipo de dados Unicode (ao chamar **SQLGetDescFieldW),** o argumento *BufferLength* deve ser um número uniforme.  
  
 Se *fieldIdentifier* for um campo definido pelo driver, o aplicativo indicará a natureza do campo para o Gerenciador de driver, definindo o argumento *BufferLength.* *BufferLength* pode ter os seguintes valores:  
  
-   Se * \*ValuePtr* é um ponteiro para uma seqüência de caracteres, então *BufferLength* é o comprimento da seqüência ou SQL_NTS.  
  
-   Se * \*ValuePtr* for um ponteiro para um buffer binário, o aplicativo coloca o resultado da macro SQL_LEN_BINARY_ATTR *(comprimento)* em *BufferLength*. Isso coloca um valor negativo em *BufferLength*.  
  
-   Se * \*ValuePtr* é um ponteiro para um valor diferente de uma seqüência de caracteres ou string binária, então *BufferLength* deve ter o valor SQL_IS_POINTER.  
  
-   Se * \*o ValuePtr* estiver contiver um tipo de dados de comprimento fixo, o *BufferLength* será SQL_IS_INTEGER, SQL_IS_UINTEGER, SQL_IS_SMALLINT ou SQL_IS_USMALLINT, conforme apropriado.  
  
 *StringLengthPtr*  
 [Saída] Ponteiro para o buffer no qual retornar o número total de bytes (excluindo o número de bytes necessários para o caractere de rescisão nula) disponível para retornar em **ValuePtr*.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_NO_DATA ou SQL_INVALID_HANDLE.  
  
 SQL_NO_DATA é devolvido se *RecNumber* for maior do que o número atual de registros de descritores.  
  
 SQL_NO_DATA é devolvido se *DscriptorHandle* for uma alça IRD e a declaração estiver no estado preparado ou executado, mas não houve cursor aberto associado a ele.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **o SQLGetDescField** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido ligando para **sqlGetDiagRec** com um *HandleType* de SQL_HANDLE_STMT e uma *alça* de *statementHandle*. A tabela a seguir lista os valores SQLSTATE comumente retornados pelo **SQLGetDescField** e explica cada um no contexto desta função; a notação "(DM)" precede as descrições de SQLSTATEs devolvidas pelo Driver Manager. O código de devolução associado a cada valor SQLSTATE é SQL_ERROR, a menos que seja observado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informacional específica do motorista. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|01004|Dados de cordas, truncados direito|O \* *buffer ValuePtr* não era grande o suficiente para retornar todo o campo descritor, de modo que o campo foi truncado. O comprimento do campo descritor não truncado é devolvido em **StringLengthPtr*. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|07009|Índice de descritor inválido|(DM) O argumento *RecNumber* era igual a 0, o atributo de declaração SQL_ATTR_USE_BOOKMARK era SQL_UB_OFF, e o argumento *DscriptorHandle* era uma alça IRD. (Este erro só pode ser retornado para um descritor explicitamente alocado se o descritor estiver associado a uma alça de instrução.)<br /><br /> O argumento *FieldIdentifier* era um campo de registro, o argumento *RecNumber* era 0, e o argumento *DscriptorHandle* era uma alça IPD.<br /><br /> O argumento *RecNumber* foi menor que 0.|  
|08S01|Falha no link de comunicação|O link de comunicação entre o driver e a fonte de dados à qual o driver estava conectado falhou antes da função ser concluída.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia SQLSTATE específico e para o qual não foi definido sqlSTATE específico para a implementação. A mensagem de erro retornada pelo **SQLGetDiagRec** no * \** buffer MessageText descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não conseguiu alocar a memória necessária para suportar a execução ou a conclusão da função.|  
|HY007|A declaração associada não está preparada|*O DscriptorHandle* foi associado a um *StatementHandle* como um IRD, e a alça de declaração associada não havia sido preparada ou executada.|  
|HY010|Erro de seqüência de função|(DM) *DscriptorHandle* foi associado a uma *função Dessincronizadamente* executante (não esta) foi chamada e ainda estava sendo executada quando esta função foi chamada.<br /><br /> (DM) *O DscriptorHandle* foi associado a um *StatementHandle* para o qual **SQLExecute,** **SQLExecDirect,** **SQLBulkOperations**ou **SQLSetPos** foram chamados e devolvidos SQL_NEED_DATA. Essa função foi chamada antes de os dados serem enviados para todos os parâmetros ou colunas de execução de dados.<br /><br /> (DM) Uma função de execução assíncrona foi chamada para o cabo de conexão associado ao *DscriptorHandle*. Esta função assíncrona ainda estava sendo executada quando a função **SQLGetDescField** foi chamada.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não podiam ser acessados, possivelmente devido às baixas condições de memória.|  
|HY021|Informações dedescritores inconsistentes|Os campos SQL_DESC_TYPE e SQL_DESC_DATETIME_INTERVAL_CODE não formam um tipo De SQL ODBC válido, um tipo SQL específico para driver válido (para IPDs) ou um tipo C ODBC válido (para APDs ou ARDs).|  
|HY090|Comprimento de seqüência ou buffer inválido|(DM) * \*ValuePtr* era uma seqüência de caracteres, e *BufferLength* era menor que zero.|  
|HY091|Identificador de campo de descritor inválido|*FieldIdentifier* não era um campo definido pelo ODBC e não era um valor definido pela implementação.<br /><br /> *FieldIdentifier* foi indefinido para o *DscriptorHandle*.|  
|HY117|A conexão está suspensa devido ao estado de transação desconhecido. Somente funções desconectadas e somente leitura são permitidas.|(DM) Para obter mais informações sobre o estado suspenso, consulte [A função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tempo de tempo de conexão expirado|O período de tempo de tempo de conexão expirou antes que a fonte de dados respondesse à solicitação. O período de tempo de tempo de conexão é definido através **de SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não suporta esta função|(DM) O driver associado ao *DescritorHandle* não suporta a função.|  
  
## <a name="comments"></a>Comentários  
 Um aplicativo pode chamar **SQLGetDescField** para devolver o valor de um único campo de um registro descritor. Uma chamada para **SQLGetDescField** pode retornar a configuração de qualquer campo em qualquer tipo de descritor, incluindo campos de cabeçalho, campos de registro e campos de marcação. Um aplicativo pode obter as configurações de vários campos nos mesmos ou diferentes descritores, em ordem arbitrária, fazendo chamadas repetidas para **SQLGetDescField**. **O SQLGetDescField** também pode ser chamado para retornar campos descritores definidos pelo driver.  
  
 Por razões de desempenho, um aplicativo não deve chamar **SQLGetDescField** para um IRD antes de executar uma declaração.  
  
 As configurações de vários campos que descrevem o nome, o tipo de dados e o armazenamento de dados de coluna ou parâmetro também podem ser recuperadas em uma única chamada para **SQLGetDescRec**. **SQLGetStmtAttr** pode ser chamado para retornar a configuração de um único campo no cabeçalho do descritor que também é um atributo de declaração. **SQLColAttribute,** **SQLDescribeCol**e **SQLDescribeParam** return record ou bookmark.  
  
 Quando um aplicativo chama **SQLGetDescField** para recuperar o valor de um campo indefinido para um determinado tipo de descritor, a função retorna SQL_SUCCESS mas o valor retornado para o campo é indefinido. Por exemplo, chamar **SQLGetDescField** para o campo SQL_DESC_NAME ou SQL_DESC_NULLABLE de um APD ou ARD retornará SQL_SUCCESS mas um valor indefinido para o campo.  
  
 Quando um aplicativo chama **SQLGetDescField** para recuperar o valor de um campo definido para um determinado tipo de descritor, mas que não tem valor padrão e ainda não foi definido, a função retorna SQL_SUCCESS mas o valor retornado para o campo é indefinido. Para obter mais informações sobre a inicialização dos campos e descrições dos campos, consulte "Inicialização de Campos de Descritores" em [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md). Para obter mais informações sobre descritores, consulte [Descritores](../../../odbc/reference/develop-app/descriptors.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Obtendo vários campos de descritores|[Função SQLGetDescRec](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|Definindo um único campo descritor|[Função SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|Configuração de vários campos de descritor|[Função SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API oDBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
