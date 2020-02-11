---
title: Função SQLSetDescRec | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetDescRec
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLSetDescRec
helpviewer_keywords:
- SQLSetDescRec function [ODBC]
ms.assetid: bf55256c-7eb7-4e3f-97ef-b0fee09ba829
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2b9940d55ca10292d6c90a241f47479a2178eff3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68343062"
---
# <a name="sqlsetdescrec-function"></a>Função SQLSetDescRec
**Conformidade**  
 Versão introduzida: conformidade de padrões do ODBC 3,0: ISO 92  
  
 **Resumo**  
 A função **SQLSetDescRec** define vários campos de descritores que afetam o tipo de dados e o buffer associado a uma coluna ou dados de parâmetro.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLSetDescRec(  
      SQLHDESC      DescriptorHandle,  
      SQLSMALLINT   RecNumber,  
      SQLSMALLINT   Type,  
      SQLSMALLINT   SubType,  
      SQLLEN        Length,  
      SQLSMALLINT   Precision,  
      SQLSMALLINT   Scale,  
      SQLPOINTER    DataPtr,  
      SQLLEN *      StringLengthPtr,  
      SQLLEN *      IndicatorPtr);  
```  
  
## <a name="arguments"></a>Argumentos  
 *DescriptorHandle*  
 Entrada Identificador do descritor. Isso não deve ser um identificador IRD.  
  
 *RecNumber*  
 Entrada Indica o registro de descritor que contém os campos a serem definidos. Os registros de descritores são numerados de 0, com o número de registro 0 sendo o registro de indicador. Esse argumento deve ser igual ou maior que 0. Se *RecNumber* for maior que o valor de SQL_DESC_COUNT, SQL_DESC_COUNTis alterado para o valor de *RecNumber*.  
  
 *Tipo*  
 Entrada O valor para o qual definir o campo de SQL_DESC_TYPE para o registro de descritor.  
  
 *Subtipo*  
 Entrada Para registros cujo tipo é SQL_DATETIME ou SQL_INTERVAL, esse é o valor para o qual definir o campo SQL_DESC_DATETIME_INTERVAL_CODE.  
  
 *Comprimento*  
 Entrada O valor para o qual definir o campo de SQL_DESC_OCTET_LENGTH para o registro de descritor.  
  
 *Precisão*  
 Entrada O valor para o qual definir o campo de SQL_DESC_PRECISION para o registro de descritor.  
  
 *Escala*  
 Entrada O valor para o qual definir o campo de SQL_DESC_SCALE para o registro de descritor.  
  
 *DataPtr*  
 [Entrada ou saída adiada] O valor para o qual definir o campo de SQL_DESC_DATA_PTR para o registro de descritor. *DataPtr* pode ser definido como um ponteiro nulo.  
  
 O argumento *DataPtr* pode ser definido como um ponteiro NULL para definir o campo SQL_DESC_DATA_PTR como um ponteiro nulo. Se o identificador no argumento *DescriptorHandle* estiver associado a um ARD, isso desassociará a coluna.  
  
 *StringLengthPtr*  
 [Entrada ou saída adiada] O valor para o qual definir o campo de SQL_DESC_OCTET_LENGTH_PTR para o registro de descritor. *StringLengthPtr* pode ser definido como um ponteiro nulo para definir o campo SQL_DESC_OCTET_LENGTH_PTR como um ponteiro nulo.  
  
 *IndicatorPtr*  
 [Entrada ou saída adiada] O valor para o qual definir o campo de SQL_DESC_INDICATOR_PTR para o registro de descritor. *IndicatorPtr* pode ser definido como um ponteiro nulo para definir o campo SQL_DESC_INDICATOR_PTR como um ponteiro nulo.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **SQLSetDescRec** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido chamando **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_DESC e um *identificador* de *DescriptorHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLSetDescRec** e explica cada um no contexto dessa função; a notação "(DM)" precede as descrições de sqlstates retornadas pelo Gerenciador de driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
|SQLSTATE|Erro|DESCRIÇÃO|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa específica do driver. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|07009|Índice de descritor inválido|O argumento *RecNumber* foi definido como 0 e o *DescriptorHandle* fez referência a um identificador de IPD.<br /><br /> O argumento *RecNumber* era menor que 0.<br /><br /> O argumento *RecNumber* era maior que o número máximo de colunas ou parâmetros aos quais a fonte de dados pode dar suporte e o argumento *DESCRIPTORHANDLE* era um APD, IPD ou ARD.<br /><br /> O argumento *RecNumber* era igual a 0 e o argumento *DescriptorHandle* se referiu a um APD alocado implicitamente. (Esse erro não ocorre com um descritor de aplicativo explicitamente alocado porque não é conhecido se um descritor de aplicativo explicitamente alocado é um APD ou ARD até o tempo de execução.)|  
|08S01|Falha no link de comunicação|O link de comunicação entre o driver e a fonte de dados ao qual o driver foi conectado falhou antes da função concluir o processamento.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia um SQLSTATE específico e para o qual nenhum SQLSTATE específico de implementação foi definido. A mensagem de erro retornada por **SQLGetDiagRec** no buffer * \*MessageText* descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar memória necessária para dar suporte à execução ou à conclusão da função.|  
|HY010|Erro de sequência de função|(DM) o *DescriptorHandle* foi associado a um *StatementHandle* para o qual uma função de execução assíncrona (não esta) foi chamada e ainda estava em execução quando essa função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**ou **SQLSetPos** foi chamado para o *StatementHandle* com o qual o *DescriptorHandle* estava associado e retornou SQL_NEED_DATA. Esta função foi chamada antes de os dados serem enviados para todos os parâmetros de dados em execução ou colunas.<br /><br /> (DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado ao *DescriptorHandle*. Esta função aynchronous ainda estava em execução quando a função **SQLSetDescRec** foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**ou **SQLMoreResults** foi chamado para um dos identificadores de instrução associados ao *DescriptorHandle* e retornou SQL_PARAM_DATA_AVAILABLE. Esta função foi chamada antes de os dados serem recuperados para todos os parâmetros transmitidos.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não puderam ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY016|Não é possível modificar um descritor de linha de implementação|O argumento *DescriptorHandle* foi associado a um IRD.|  
|HY021|Informações de descritor inconsistentes|O campo de *tipo* ou qualquer outro campo associado ao campo SQL_DESC_TYPE no descritor não era válido ou consistente.<br /><br /> As informações de descritor verificadas durante uma verificação de consistência não estavam consistentes. (Consulte "verificações de consistência", mais adiante nesta seção.)|  
|HY090|Comprimento de cadeia de caracteres ou buffer inválido|(DM) o driver era um driver ODBC *2. x* , o descritor era um ARD, o argumento *ColumnNumber* foi definido como 0 e o valor especificado para o argumento *BufferLength* não era igual a 4.|  
|HY117|A conexão foi suspensa devido a um estado de transação desconhecido. Somente funções de desconexão e somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tempo limite de conexão expirado|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|O driver não oferece suporte a essa função|(DM) o driver associado ao *DescriptorHandle* não oferece suporte à função.|  
  
## <a name="comments"></a>Comentários  
 Um aplicativo pode chamar **SQLSetDescRec** para definir os seguintes campos para uma única coluna ou parâmetro:  
  
-   SQL_DESC_TYPE  
  
-   SQL_DESC_DATETIME_INTERVAL_CODE (para registros cujo tipo é SQL_DATETIME ou SQL_INTERVAL)  
  
-   SQL_DESC_OCTET_LENGTH  
  
-   SQL_DESC_PRECISION  
  
-   SQL_DESC_SCALE  
  
-   SQL_DESC_DATA_PTR  
  
-   SQL_DESC_OCTET_LENGTH_PTR  
  
-   SQL_DESC_INDICATOR_PTR  
  
> [!NOTE]  
>  Se uma chamada para **SQLSetDescRec** falhar, o conteúdo do registro de descritor identificado pelo argumento *RecNumber* será indefinido.  
  
 Ao associar uma coluna ou parâmetro, **SQLSetDescRec** permite que você altere vários campos que afetam a associação sem chamar **SQLBindCol** ou **SQLBindParameter** ou fazer várias chamadas para **SQLSetDescField**. **SQLSetDescRec** pode definir campos em um descritor não associado atualmente a uma instrução. Observe que **SQLBindParameter** define mais campos do que **SQLSetDescRec**, pode definir campos em um APD e um IPD em uma chamada e não requer um identificador de descritor.  
  
> [!NOTE]  
>  O atributo de instrução SQL_ATTR_USE_BOOKMARKS sempre deve ser definido antes de chamar **SQLSetDescRec** com um argumento *RecNumber* de 0 para definir campos de indicador. Embora isso não seja obrigatório, é altamente recomendável.  
  
## <a name="consistency-checks"></a>Verificações de consistência  
 Uma verificação de consistência é executada automaticamente pelo driver sempre que um aplicativo define o SQL_DESC_DATA_PTR campo de um APD, ARD ou IPD. Se qualquer um dos campos estiver inconsistente com outros campos, **SQLSetDescRec** retornará SQLSTATE HY021 (informações de descritor inconsistentes).  
  
 Sempre que um aplicativo define o SQL_DESC_DATA_PTR campo de um APD, ARD ou IPD, o driver verifica se o valor do campo SQL_DESC_TYPE e os valores aplicáveis a esse campo SQL_DESC_TYPE são válidos e consistentes. Essa verificação é sempre executada quando **SQLBindParameter** ou **SQLBindCol** é chamado ou quando **SQLSETDESCREC** é chamado para um APD, ARD ou IPD. Essa verificação de consistência inclui as seguintes verificações nos campos de descritor:  
  
-   O campo SQL_DESC_TYPE deve ser um dos tipos ODBC C ou SQL válidos ou um tipo SQL específico de driver. O campo de SQL_DESC_CONCISE_TYPE deve ser um dos tipos ODBC C ou SQL válidos ou um tipo C ou SQL específico de driver, incluindo os tipos de DateTime e de intervalo concisos.  
  
-   Se o campo de registro de SQL_DESC_TYPE for SQL_DATETIME ou SQL_INTERVAL, o campo SQL_DESC_DATETIME_INTERVAL_CODE deverá ser um dos códigos DateTime ou interval válidos. (Consulte a descrição do campo SQL_DESC_DATETIME_INTERVAL_CODE em [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).)  
  
-   Se o campo SQL_DESC_TYPE indicar um tipo numérico, os campos SQL_DESC_PRECISION e SQL_DESC_SCALE serão verificados como válidos.  
  
-   Se o campo de SQL_DESC_CONCISE_TYPE for um tipo de dados de tempo ou carimbo de data/hora, um tipo de intervalo com um componente de segundos ou um dos tipos de dados de intervalo com um componente de tempo, o campo SQL_DESC_PRECISION será verificado como uma precisão de segundos válida.  
  
-   Se o SQL_DESC_CONCISE_TYPE for um tipo de dados de intervalo, o campo SQL_DESC_DATETIME_INTERVAL_PRECISION será verificado como um valor de precisão inicial de intervalo válido.  
  
 O campo SQL_DESC_DATA_PTR de um IPD não é normalmente definido; no entanto, um aplicativo pode fazer isso para forçar uma verificação de consistência de campos de IPD. Uma verificação de consistência não pode ser executada em um IRD. O valor ao qual o campo SQL_DESC_DATA_PTR do IPD está definido não é realmente armazenado e não pode ser recuperado por uma chamada para **SQLGetDescField** ou **SQLGetDescRec**; a configuração é feita somente para forçar a verificação de consistência.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Associando uma coluna|[Função SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Associando um parâmetro|[Função SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|Obtendo um único campo de descritor|[Função SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|Obtendo vários campos de descritor|[Função SQLGetDescRec](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|Definindo campos de descritor único|[Função SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
