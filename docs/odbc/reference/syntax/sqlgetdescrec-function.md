---
title: Função SQLGetDescRec | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetDescRec
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetDescRec
helpviewer_keywords:
- SQLGetDescRec function [ODBC]
ms.assetid: 325e0907-8e87-44e8-a111-f39e636a9cbc
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 87d7b971b379f19f8451e924932a5e699e9b9983
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285481"
---
# <a name="sqlgetdescrec-function"></a>Função SQLGetDescRec
**Conformidade**  
 Versão introduzida: ODBC 3.0 Standards Compliance: ISO 92  
  
 **Resumo**  
 **SQLGetDescRec** retorna as configurações ou valores atuais de vários campos de um registro descritor. Os campos retornados descrevem o nome, o tipo de dados e o armazenamento de dados de coluna ou parâmetro.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLGetDescRec(  
      SQLHDESC        DescriptorHandle,  
      SQLSMALLINT     RecNumber,  
      SQLCHAR *       Name,  
      SQLSMALLINT     BufferLength,  
      SQLSMALLINT *   StringLengthPtr,  
      SQLSMALLINT *   TypePtr,  
      SQLSMALLINT *   SubTypePtr,  
      SQLLEN *        LengthPtr,  
      SQLSMALLINT *   PrecisionPtr,  
      SQLSMALLINT *   ScalePtr,  
      SQLSMALLINT *   NullablePtr);  
```  
  
## <a name="arguments"></a>Argumentos  
 *DescriptorHandle*  
 [Entrada] Alça do descritor.  
  
 *RecNumber*  
 [Entrada] Indica o registro do descritor a partir do qual o aplicativo busca informações. Os registros do descritor são numerados a partir de 1, com o número recorde 0 sendo o recorde de marcadores. O argumento *RecNumber* deve ser menor ou igual ao valor de SQL_DESC_COUNT. Se *RecNumber* for menor ou igual a SQL_DESC_COUNT mas a linha não contiver dados para uma coluna ou parâmetro, uma chamada para **SQLGetDescRec** retornará os valores padrão dos campos. (Para obter mais informações, consulte "Inicialização de campos de descritores" em [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).)  
  
 *Nome*  
 [Saída] Um ponteiro para um buffer no qual retornar o campo SQL_DESC_NAME para o registro do descritor.  
  
 Se *O Nome* for NULO, *stringLengthPtr* ainda retornará o número total de caracteres (excluindo o caractere de rescisão nula para dados de caracteres) disponível para retornar no buffer apontado por *Name*.  
  
 *BufferLength*  
 [Entrada] Comprimento do buffer **Nome,* em caracteres.  
  
 *StringLengthPtr*  
 [Saída] Um ponteiro para um buffer no qual retornar o número \*de caracteres de dados disponíveis para retornar no buffer *Nome,* excluindo o caractere de rescisão nula. Se o número de caracteres for maior ou \*igual a *BufferLength,* os dados em *Name* são truncados para *BufferLength* menos o comprimento de um caractere de rescisão nula, e é nulo pelo driver.  
  
 *TypePtr*  
 [Saída] Um ponteiro para um buffer no qual devolver o valor do campo SQL_DESC_TYPE para o registro do descritor.  
  
 *SubTypePtr*  
 [Saída] Para registros cujo tipo é SQL_DATETIME ou SQL_INTERVAL, este é um ponteiro para um buffer no qual devolver o valor do campo SQL_DESC_DATETIME_INTERVAL_CODE.  
  
 *ComprimentoPtr*  
 [Saída] Um ponteiro para um buffer no qual devolver o valor do campo SQL_DESC_OCTET_LENGTH para o registro do descritor.  
  
 *PrecisionPtr*  
 [Saída] Um ponteiro para um buffer no qual devolver o valor do campo SQL_DESC_PRECISION para o registro do descritor.  
  
 *ScalePtr*  
 [Saída] Um ponteiro para um buffer no qual devolver o valor do campo SQL_DESC_SCALE para o registro do descritor.  
  
 *AnuladoPtr*  
 [Saída] Um ponteiro para um buffer no qual devolver o valor do campo SQL_DESC_NULLABLE para o registro do descritor.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_NO_DATA ou SQL_INVALID_HANDLE.  
  
 SQL_NO_DATA é devolvido se *RecNumber* for maior do que o número atual de registros de descritores.  
  
 SQL_NO_DATA é devolvido se *DscriptorHandle* for uma alça IRD e a declaração estiver no estado preparado ou executado, mas não houve cursor aberto associado a ele.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **o SQLGetDescRec** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido ligando para **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_DESC e uma *alça* de *DscriptorHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados pelo **SQLGetDescRec** e explica cada um no contexto desta função; a notação "(DM)" precede as descrições de SQLSTATEs devolvidas pelo Driver Manager. O código de devolução associado a cada valor SQLSTATE é SQL_ERROR, a menos que seja observado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informacional específica do motorista. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|01004|Dados de cordas, truncados direito|O \* *buffer Name* não era grande o suficiente para retornar todo o campo descritor. Portanto, o campo foi truncado. O comprimento do campo descritor não truncado é devolvido em **StringLengthPtr*. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|07009|Índice de descritor inválido|O argumento *FieldIdentifier* era um campo de registro, o argumento *RecNumber* foi definido como 0, e o argumento *DscriptorHandle* era uma alça IPD.<br /><br /> (DM) O argumento *RecNumber* foi definido como 0, e o atributo de declaração SQL_ATTR_USE_BOOKMARKS foi definido como SQL_UB_OFF, e o argumento *DscriptorHandle* era uma alça IRD.<br /><br /> O argumento *RecNumber* foi menor que 0.|  
|08S01|Falha no link de comunicação|O link de comunicação entre o driver e a fonte de dados à qual o driver estava conectado falhou antes da função ser concluída.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia SQLSTATE específico e para o qual não foi definido sqlSTATE específico para a implementação. A mensagem de erro retornada pelo **SQLGetDiagRec** no * \** buffer MessageText descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não conseguiu alocar a memória necessária para suportar a execução ou a conclusão da função.|  
|HY007|A declaração associada não está preparada|*DscriptorHandle* foi associado a um IRD, e a alça de declaração associada não estava no estado preparado ou executado.|  
|HY010|Erro de seqüência de função|(DM) *DscriptorHandle* foi associado a uma *função Dessincronizadamente* executante (não esta) foi chamada e ainda estava sendo executada quando esta função foi chamada.<br /><br /> (DM) *O DscriptorHandle* foi associado a um *StatementHandle* para o qual **SQLExecute,** **SQLExecDirect,** **SQLBulkOperations**ou **SQLSetPos** foram chamados e devolvidos SQL_NEED_DATA. Essa função foi chamada antes de os dados serem enviados para todos os parâmetros ou colunas de execução de dados.<br /><br /> (DM) Uma função de execução assíncrona foi chamada para o cabo de conexão associado ao *DscriptorHandle*. Esta função assíncrona ainda estava sendo executada quando **o SQLGetDescRec** foi chamado.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não podiam ser acessados, possivelmente devido às baixas condições de memória.|  
|HY117|A conexão está suspensa devido ao estado de transação desconhecido. Somente funções desconectadas e somente leitura são permitidas.|(DM) Para obter mais informações sobre o estado suspenso, consulte [a função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tempo de tempo de conexão expirado|O período de tempo de tempo de conexão expirou antes que a fonte de dados respondesse à solicitação. O período de tempo de tempo de conexão é definido através **de SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não suporta esta função|(DM) O driver associado ao *DscriptorHandle* não suporta a função.|  
  
## <a name="comments"></a>Comentários  
 Um aplicativo pode chamar **SQLGetDescRec** para recuperar os valores dos seguintes campos de descritor para uma única coluna ou parâmetro:  
  
-   SQL_DESC_NAME  
  
-   SQL_DESC_TYPE  
  
-   SQL_DESC_DATETIME_INTERVAL_CODE (para registros cujo tipo seja SQL_DATETIME ou SQL_INTERVAL)  
  
-   SQL_DESC_OCTET_LENGTH  
  
-   SQL_DESC_PRECISION  
  
-   SQL_DESC_SCALE  
  
-   SQL_DESC_NULLABLE  
  
 **O SQLGetDescRec** não recupera os valores para campos de cabeçalho.  
  
 Um aplicativo pode impedir o retorno da configuração de um campo definindo o argumento que corresponde ao campo a um ponteiro nulo.  
  
 Quando um aplicativo chama **SQLGetDescRec** para recuperar o valor de um campo indefinido para um determinado tipo de descritor, a função retorna SQL_SUCCESS mas o valor retornado para o campo é indefinido. Por exemplo, chamar **sqlGetDescRec** para o campo SQL_DESC_NAME ou SQL_DESC_NULLABLE de um APD ou ARD retornará SQL_SUCCESS mas um valor indefinido para o campo.  
  
 Quando um aplicativo chama **SQLGetDescRec** para recuperar o valor de um campo definido para um determinado tipo de descritor, mas que não tem valor padrão e ainda não foi definido, a função retorna SQL_SUCCESS mas o valor retornado para o campo é indefinido. Para obter mais informações, consulte "Inicialização de campos de descritores" em [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).  
  
 Os valores dos campos também podem ser recuperados individualmente por uma chamada para **SQLGetDescField**. Para obter uma descrição dos campos em um cabeçalho ou registro de descritor, consulte [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md). Para obter mais informações sobre descritores, consulte [Descritores](../../../odbc/reference/develop-app/descriptors.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Vinculando uma coluna|[Função SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Vinculando um parâmetro|[Função SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|Obtendo um campo descritor|[Função SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|Configuração de vários campos de descritor|[Função SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API oDBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
