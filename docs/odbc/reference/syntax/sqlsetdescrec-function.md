---
title: Função SQLSetDescRec | Microsoft Docs
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
- SQLSetDescRec
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSetDescRec
helpviewer_keywords:
- SQLSetDescRec function [ODBC]
ms.assetid: bf55256c-7eb7-4e3f-97ef-b0fee09ba829
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 085543aca838cfe1a8123f891c30f618b86eb15d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlsetdescrec-function"></a>Função SQLSetDescRec
**Conformidade**  
 Versão introduzidas: Conformidade de padrões 3.0 ODBC: 92 ISO  
  
 **Resumo**  
 O **SQLSetDescRec** função define vários campos de descritor que afetam o tipo de dados e buffer associados a uma coluna ou parâmetro de dados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
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
 [Entrada] Identificador do descritor. Isso não deve ser um identificador IRD.  
  
 *RecNumber*  
 [Entrada] Indica que o registro do descritor que contém os campos a serem definidos. Registros de descritor são numerados de 0, com o número de registro sendo o registro do indicador de 0. Esse argumento deve ser igual ou maior que 0. Se *RecNumber* é maior que o valor de SQL_DESC_COUNT, SQL_DESC_COUNTis alterado para o valor de *RecNumber*.  
  
 *Tipo*  
 [Entrada] O valor para o qual definir o campo SQL_DESC_TYPE para o registro do descritor.  
  
 *SubType*  
 [Entrada] Para registros cujo tipo é SQL_DATETIME ou SQL_INTERVAL, esse é o valor para o qual definir o campo SQL_DESC_DATETIME_INTERVAL_CODE.  
  
 *Comprimento*  
 [Entrada] O valor para o qual definir o campo SQL_DESC_OCTET_LENGTH para o registro do descritor.  
  
 *Precisão*  
 [Entrada] O valor para o qual definir o campo SQL_DESC_PRECISION para o registro do descritor.  
  
 *Escala*  
 [Entrada] O valor para o qual definir o campo SQL_DESC_SCALE para o registro do descritor.  
  
 *DataPtr*  
 [Adiada de entrada ou saída] O valor para o qual definir o campo SQL_DESC_DATA_PTR para o registro do descritor. *DataPtr* pode ser definido como um ponteiro nulo.  
  
 O *DataPtr* argumento pode ser definido como um ponteiro nulo para definir o campo SQL_DESC_DATA_PTR para um ponteiro nulo. Se o identificador no *DescriptorHandle* argumento está associado um descartar, isso desvincula a coluna.  
  
 *StringLengthPtr*  
 [Adiada de entrada ou saída] O valor para o qual definir o campo SQL_DESC_OCTET_LENGTH_PTR para o registro do descritor. *StringLengthPtr* pode ser definido como um ponteiro nulo para definir o campo SQL_DESC_OCTET_LENGTH_PTR como um ponteiro nulo.  
  
 *IndicatorPtr*  
 [Adiada de entrada ou saída] O valor para o qual definir o campo SQL_DESC_INDICATOR_PTR para o registro do descritor. *IndicatorPtr* pode ser definido como um ponteiro nulo para definir o campo SQL_DESC_INDICATOR_PTR como um ponteiro nulo.  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>diagnóstico  
 Quando **SQLSetDescRec** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtida chamando **SQLGetDiagRec** com um *HandleType* de SQL _ HANDLE_DESC e um *tratar* de *DescriptorHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLSetDescRec** e explica cada uma no contexto dessa função; a notação "(DM)" precede as descrições de SQLSTATEs retornados pelo Gerenciador de Driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado em contrário.  
  
|SQLSTATE|Erro|Description|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem de informação específica do driver. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|07009|Índice do descritor inválido|O *RecNumber* argumento foi definido como 0 e o *DescriptorHandle* chamado um identificador IPD.<br /><br /> O *RecNumber* argumento era menor do que 0.<br /><br /> O *RecNumber* argumento era maior que o número máximo de colunas ou parâmetros que pode dar suporte a fonte de dados, e o *DescriptorHandle* argumento era um APD, IPD ou descartar.<br /><br /> O *RecNumber* argumento era igual a 0 e o *DescriptorHandle* argumento chamado um APD alocado implicitamente. (Esse erro não ocorre com um descritor de aplicativo explicitamente alocado porque não se sabe se um descritor de aplicativo explicitamente alocado é um APD ou descartar até que o tempo de execução.)|  
|08S01|Falha de link de comunicação|Falha do link de comunicação entre o driver e a fonte de dados ao qual o driver foi conectado antes do processamento da função foi concluída.|  
|HY000|Erro geral|Ocorreu um erro para o qual não houve nenhuma SQLSTATE específico e para o qual nenhuma SQLSTATE específicos de implementação foi definida. A mensagem de erro retornada pelo **SQLGetDiagRec** no  *\*MessageText* buffer descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar a memória necessária para dar suporte a execução ou a conclusão da função.|  
|HY010|Erro de sequência de função|(DM) a *DescriptorHandle* foi associado um *StatementHandle* para que uma função de execução assíncrona (não esse um) foi chamada e ainda estava em execução quando esta função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, ou **SQLSetPos** foi chamado para o  *StatementHandle* com a qual o *DescriptorHandle* foi retornado de SQL_NEED_DATA e associados. Essa função foi chamada antes de dados foi enviados para todas as colunas ou parâmetros de dados em execução.<br /><br /> (DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado a *DescriptorHandle*. Essa função assíncrono ainda estava em execução quando o **SQLSetDescRec** função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, ou **SQLMoreResults** foi chamado para uma das alças de instrução associadas a *DescriptorHandle* e retornado SQL_PARAM_DATA_AVAILABLE. Essa função foi chamada antes de recuperação para todos os parâmetros de fluxo de dados.|  
|HY013|Erro de gerenciamento de memória|Não foi possível processar a chamada de função porque os objetos de memória subjacente não podem ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY016|Não é possível modificar um descritor de linha de implementação|O *DescriptorHandle* argumento foi associado um IRD.|  
|HY021|Informações do descritor inconsistentes|O *tipo* campo, ou qualquer outro campo associado ao campo SQL_DESC_TYPE no descritor de não era válida ou consistente.<br /><br /> Informações de descritor verificadas durante uma verificação de consistência não estavam consistentes. (Consulte "Verificações de consistência," nesta seção.)|  
|HY090|Comprimento de buffer ou cadeia de caracteres inválido|(DM) o driver foi um ODBC 2 *. x* driver, o descritor foi um descartar o *ColumnNumber* argumento foi definido como 0 e o valor especificado para o argumento *BufferLength* foi não é igual a 4.|  
|HY117|Conexão está suspenso devido ao estado de transação desconhecido. Somente Desconecte e funções de somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tempo limite de Conexão expirou|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não dá suporte a esta função|O driver em (DM) associado a *DescriptorHandle* não oferece suporte para a função.|  
  
## <a name="comments"></a>Comentários  
 Um aplicativo pode chamar **SQLSetDescRec** para definir os campos a seguir para uma única coluna ou parâmetro:  
  
-   SQL_DESC_TYPE  
  
-   SQL_DESC_DATETIME_INTERVAL_CODE (para registros cujo tipo é SQL_DATETIME ou SQL_INTERVAL)  
  
-   SQL_DESC_OCTET_LENGTH  
  
-   SQL_DESC_PRECISION  
  
-   SQL_DESC_SCALE  
  
-   SQL_DESC_DATA_PTR  
  
-   SQL_DESC_OCTET_LENGTH_PTR  
  
-   SQL_DESC_INDICATOR_PTR  
  
> [!NOTE]  
>  Se uma chamada para **SQLSetDescRec** falhar, o conteúdo do registro do descritor identificado pelo *RecNumber* argumento são indefinidos.  
  
 Ao associar uma coluna ou parâmetro, **SQLSetDescRec** permite que você altere os vários campos que afetam a associação sem chamar **SQLBindCol** ou **SQLBindParameter** ou fazer várias chamadas para **SQLSetDescField**. **SQLSetDescRec** pode definir os campos em um descritor de não atualmente associado a uma instrução. Observe que **SQLBindParameter** define mais campos que **SQLSetDescRec**, pode definir campos em um APD e um IPD em uma chamada e não requer um identificador do descritor.  
  
> [!NOTE]  
>  O atributo de instrução SQL_ATTR_USE_BOOKMARKS sempre deve ser definido antes de chamar **SQLSetDescRec** com um *RecNumber* argumento de 0 para definir campos de indicador. Embora não seja obrigatório, é altamente recomendável.  
  
## <a name="consistency-checks"></a>Verificações de consistência  
 Uma verificação de consistência é executada pelo driver automaticamente sempre que um aplicativo define o campo SQL_DESC_DATA_PTR de APD, descartar ou IPD. Se qualquer um dos campos é inconsistente com outros campos, **SQLSetDescRec** retornará SQLSTATE HY021 (informações de descritor inconsistentes).  
  
 Sempre que um aplicativo define o campo SQL_DESC_DATA_PTR de APD, descartar ou IPD, o driver verifica o valor do campo SQL_DESC_TYPE e os valores aplicáveis para o campo SQL_DESC_TYPE são válidos e consistentes. Essa verificação é sempre executada quando **SQLBindParameter** ou **SQLBindCol** é chamado ou quando **SQLSetDescRec** é chamado para um APD, descartar ou IPD. Essa verificação de consistência inclui as seguintes verificações nos campos de descritor:  
  
-   O campo SQL_DESC_TYPE deve ser um dos válido ODBC C ou tipos de SQL ou um tipo SQL específica do driver. O campo SQL_DESC_CONCISE_TYPE deve ser um dos tipos ODBC C ou SQL válidos ou um driver C ou SQL tipo específico, incluindo os tipos de data/hora e intervalo concisos.  
  
-   Se o campo de registro SQL_DESC_TYPE for SQL_DATETIME ou SQL_INTERVAL, o campo SQL_DESC_DATETIME_INTERVAL_CODE deve ser um dos códigos de intervalo ou datetime válido. (Consulte a descrição do campo SQL_DESC_DATETIME_INTERVAL_CODE na [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).)  
  
-   Se o campo SQL_DESC_TYPE indica um tipo numérico, os campos SQL_DESC_PRECISION e SQL_DESC_SCALE são verificados para ser válido.  
  
-   Se o campo SQL_DESC_CONCISE_TYPE é um tipo de dados de tempo ou carimbo de hora, um intervalo de tipo com um componente de segundos, ou um dos tipos de dados de intervalo com um componente de tempo, o campo SQL_DESC_PRECISION é verificado para ser uma precisão de segundos válido.  
  
-   Se o SQL_DESC_CONCISE_TYPE é um tipo de dados de intervalo, o campo SQL_DESC_DATETIME_INTERVAL_PRECISION é verificado para ser um valor de precisão à esquerda do intervalo válido.  
  
 O campo SQL_DESC_DATA_PTR de um IPD normalmente não está definido; No entanto, um aplicativo pode fazê-lo para forçar uma verificação de consistência de campos do IPD. Uma verificação de consistência não pode ser executada em um IRD. O valor definido para o campo SQL_DESC_DATA_PTR do IPD, na verdade, não é armazenado e não pode ser recuperado por uma chamada para **SQLGetDescField** ou **SQLGetDescRec**; a configuração é feita apenas para forçar o verificação de consistência.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Associação de uma coluna|[Função SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Um parâmetro de associação|[Função SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|Obter um campo de descritor único|[Função SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|Obtendo vários campos de descritor|[Função SQLGetDescRec](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|Definindo campos de descritor único|[Função SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Referência de API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
