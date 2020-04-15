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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b29879ff7635d6eb7d5a0f7489ff3994758d4a35
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299526"
---
# <a name="sqlsetdescrec-function"></a>Função SQLSetDescRec
**Conformidade**  
 Versão introduzida: ODBC 3.0 Standards Compliance: ISO 92  
  
 **Resumo**  
 A função **SQLSetDescRec** define vários campos de descritores que afetam o tipo de dados e o buffer vinculados a uma coluna ou parâmetro.  
  
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
 [Entrada] Alça do descritor. Isto não deve ser uma alça IRD.  
  
 *RecNumber*  
 [Entrada] Indica o registro descritor que contém os campos a serem definidos. Os registros do descritor são numerados de 0, com o número recorde 0 sendo o recorde do marcador. Este argumento deve ser igual ou maior que 0. Se *recNumber* for maior que o valor de SQL_DESC_COUNT, SQL_DESC_COUNTis alterado para o valor de *RecNumber*.  
  
 *Tipo*  
 [Entrada] O valor para definir o campo SQL_DESC_TYPE para o registro do descritor.  
  
 *Subtipo*  
 [Entrada] Para registros cujo tipo é SQL_DATETIME ou SQL_INTERVAL, este é o valor para definir o campo SQL_DESC_DATETIME_INTERVAL_CODE.  
  
 *Duração*  
 [Entrada] O valor para definir o campo SQL_DESC_OCTET_LENGTH para o registro do descritor.  
  
 *Precisão*  
 [Entrada] O valor para definir o campo SQL_DESC_PRECISION para o registro do descritor.  
  
 *Escala*  
 [Entrada] O valor para definir o campo SQL_DESC_SCALE para o registro do descritor.  
  
 *DataPtr*  
 [Entrada ou saída diferida] O valor para definir o campo SQL_DESC_DATA_PTR para o registro do descritor. *DataPtr* pode ser definido como um ponteiro nulo.  
  
 O argumento *DataPtr* pode ser definido como um ponteiro nulo para definir o campo SQL_DESC_DATA_PTR para um ponteiro nulo. Se a alça no argumento *DescritorHandle* estiver associada a um ARD, isso desvinculará a coluna.  
  
 *StringLengthPtr*  
 [Entrada ou saída diferida] O valor para definir o campo SQL_DESC_OCTET_LENGTH_PTR para o registro do descritor. *StringLengthPtr* pode ser definido como um ponteiro nulo para definir o campo SQL_DESC_OCTET_LENGTH_PTR para um ponteiro nulo.  
  
 *IndicadorPtr*  
 [Entrada ou saída diferida] O valor para definir o campo SQL_DESC_INDICATOR_PTR para o registro do descritor. *IndicatorPtr* pode ser definido como um ponteiro nulo para definir o campo SQL_DESC_INDICATOR_PTR para um ponteiro nulo.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **o SQLSetDescRec** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido ligando para **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_DESC e uma *alça* de *DscriptorHandle*. A tabela a seguir lista os valores SQLSTATE comumente retornados pelo **SQLSetDescRec** e explica cada um no contexto desta função; a notação "(DM)" precede as descrições de SQLSTATEs devolvidas pelo Driver Manager. O código de devolução associado a cada valor SQLSTATE é SQL_ERROR, a menos que seja observado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informacional específica do motorista. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|07009|Índice de descritor inválido|O argumento *RecNumber* foi definido como 0, e o *DescritorHandle* se referiu a uma alça IPD.<br /><br /> O argumento *RecNumber* foi menor que 0.<br /><br /> O argumento *RecNumber* foi maior do que o número máximo de colunas ou parâmetros que a fonte de dados pode suportar, e o argumento *DscriptorHandle* foi um APD, IPD ou ARD.<br /><br /> O argumento *RecNumber* era igual a 0, e o argumento *Discritoder* referia-se a uma APD implicitamente alocada. (Este erro não ocorre com um descritor de aplicativo explicitamente alocado porque não se sabe se um descritor de aplicativo alocado explicitamente é um APD ou ARD até a hora da execução.)|  
|08S01|Falha no link de comunicação|O link de comunicação entre o driver e a fonte de dados à qual o driver estava conectado falhou antes da função ser concluída.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia SQLSTATE específico e para o qual não foi definido sqlSTATE específico para a implementação. A mensagem de erro retornada pelo **SQLGetDiagRec** no * \** buffer MessageText descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não conseguiu alocar a memória necessária para suportar a execução ou a conclusão da função.|  
|HY010|Erro de seqüência de função|(DM) O *DscriptorHandle* foi associado a um *StatementHandle* para o qual uma função de execução assíncrona (não esta) foi chamada e ainda estava sendo executada quando esta função foi chamada.<br /><br /> (DM) **SQLExecute,** **SQLExecDirect,** **SQLBulkOperations**ou **SQLSetPos** foram chamados para o *StatementHandle* com o qual o *DscriptorHandle* foi associado e retornou SQL_NEED_DATA. Essa função foi chamada antes de os dados serem enviados para todos os parâmetros ou colunas de execução de dados.<br /><br /> (DM) Uma função de execução assíncrona foi chamada para o cabo de conexão associado ao *DscriptorHandle*. Esta função ayncrona ainda estava sendo executada quando a função **SQLSetDescRec** foi chamada.<br /><br /> (DM) **SQLExecute,** **SQLExecDirect**ou **SQLMoreResults** foi chamado para uma das alças de declaração associadas ao *DscriptorHandle* e retornou SQL_PARAM_DATA_AVAILABLE. Esta função foi chamada antes de os dados serem recuperados para todos os parâmetros transmitidos.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não podiam ser acessados, possivelmente devido às baixas condições de memória.|  
|HY016|Não é possível modificar um descritor de linha de implementação|O argumento *DscriptorHandle* foi associado a um IRD.|  
|HY021|Informações dedescritores inconsistentes|O *campo Tipo,* ou qualquer outro campo associado ao campo SQL_DESC_TYPE no descritor, não era válido ou consistente.<br /><br /> As informações do descritor verificadas durante uma verificação de consistência não foram consistentes. (Veja "Verificações de consistência", mais tarde nesta seção.)|  
|HY090|Comprimento de seqüência ou buffer inválido|(DM) O driver era um Driver ODBC *2.x,* o descritor era um ARD, o argumento *ColunaNúmero* foi definido como 0, e o valor especificado para o argumento *BufferLength* não era igual a 4.|  
|HY117|A conexão está suspensa devido ao estado de transação desconhecido. Somente funções desconectadas e somente leitura são permitidas.|(DM) Para obter mais informações sobre o estado suspenso, consulte [a função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tempo de tempo de conexão expirado|O período de tempo de tempo de conexão expirou antes que a fonte de dados respondesse à solicitação. O período de tempo de tempo de conexão é definido através **de SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não suporta esta função|(DM) O driver associado ao *DescritorHandle* não suporta a função.|  
  
## <a name="comments"></a>Comentários  
 Um aplicativo pode chamar **SQLSetDescRec** para definir os seguintes campos para uma única coluna ou parâmetro:  
  
-   SQL_DESC_TYPE  
  
-   SQL_DESC_DATETIME_INTERVAL_CODE (para registros cujo tipo seja SQL_DATETIME ou SQL_INTERVAL)  
  
-   SQL_DESC_OCTET_LENGTH  
  
-   SQL_DESC_PRECISION  
  
-   SQL_DESC_SCALE  
  
-   SQL_DESC_DATA_PTR  
  
-   SQL_DESC_OCTET_LENGTH_PTR  
  
-   SQL_DESC_INDICATOR_PTR  
  
> [!NOTE]  
>  Se uma chamada para **SQLSetDescRec** falhar, o conteúdo do registro descritor identificado pelo argumento *RecNumber* será indefinido.  
  
 Ao vincular uma coluna ou parâmetro, **o SQLSetDescRec** permite alterar vários campos que afetam a vinculação sem ligar para **SQLBindCol** ou **SQLBindParameter** ou fazer várias chamadas para **SQLSetDescField**. **O SQLSetDescRec** pode definir campos em um descritor não associado atualmente a uma declaração. Observe que **o SQLBindParameter** define mais campos do que **o SQLSetDescRec,** pode definir campos em uma APD e um IPD em uma chamada e não requer uma alça de descritor.  
  
> [!NOTE]  
>  O atributo de declaração SQL_ATTR_USE_BOOKMARKS deve ser sempre definido antes de ligar para **o SQLSetDescRec** com um argumento *RecNumber* de 0 para definir campos de marcação de marcação. Embora isso não seja obrigatório, é fortemente recomendado.  
  
## <a name="consistency-checks"></a>Verificações de consistência  
 Uma verificação de consistência é realizada automaticamente pelo driver sempre que um aplicativo define o campo SQL_DESC_DATA_PTR de um APD, ARD ou IPD. Se algum dos campos for inconsistente com outros campos, **o SQLSetDescRec** retornará sqlstate hy021 (informações inconsistentes do descritor).  
  
 Sempre que um aplicativo define o campo SQL_DESC_DATA_PTR de um APD, ARD ou IPD, o motorista verifica se o valor do campo SQL_DESC_TYPE e os valores aplicáveis a esse campo SQL_DESC_TYPE são válidos e consistentes. Esta verificação é sempre realizada quando **SQLBindParameter** ou **SQLBindCol** é chamado ou quando **o SQLSetDescRec** é chamado para um APD, ARD ou IPD. Esta verificação de consistência inclui as seguintes verificações em campos descritores:  
  
-   O campo SQL_DESC_TYPE deve ser um dos tipos ODBC C ou SQL válidos ou um tipo SQL específico para o driver. O campo SQL_DESC_CONCISE_TYPE deve ser um dos tipos ODBC C ou SQL válidos ou um tipo C ou SQL específico do driver, incluindo os tipos de data e intervalo concisos.  
  
-   Se o campo de registro SQL_DESC_TYPE estiver SQL_DATETIME ou SQL_INTERVAL, o campo SQL_DESC_DATETIME_INTERVAL_CODE deve ser um dos códigos de data ou intervalo válidos. (Veja a descrição do campo SQL_DESC_DATETIME_INTERVAL_CODE em [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).)  
  
-   Se o campo SQL_DESC_TYPE indicar um tipo numérico, os campos SQL_DESC_PRECISION e SQL_DESC_SCALE são verificados como válidos.  
  
-   Se o campo SQL_DESC_CONCISE_TYPE for um tipo de dados de tempo ou carimbo de ponto, um tipo de intervalo com um componente de segundos ou um dos tipos de dados de intervalo com um componente de tempo, o campo SQL_DESC_PRECISION é verificado como uma precisão de segundos válida.  
  
-   Se o SQL_DESC_CONCISE_TYPE for um tipo de dados de intervalo, o campo SQL_DESC_DATETIME_INTERVAL_PRECISION é verificado como um valor de precisão de intervalo válido.  
  
 O campo SQL_DESC_DATA_PTR de um IPD normalmente não está definido; no entanto, um aplicativo pode fazê-lo para forçar uma verificação de consistência dos campos IPD. Uma verificação de consistência não pode ser realizada em um IRD. O valor para o que o SQL_DESC_DATA_PTR campo do IPD está definido não é realmente armazenado e não pode ser recuperado por uma chamada para **SQLGetDescField** ou **SQLGetDescRec**; a configuração é feita apenas para forçar a verificação de consistência.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Vinculando uma coluna|[Função SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Vinculando um parâmetro|[Função SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|Obtendo um único campo descritor|[Função SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|Obtendo vários campos de descritores|[Função SQLGetDescRec](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|Definindo campos descritores únicos|[Função SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API oDBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
