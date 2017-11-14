---
title: "Função SQLCopyDesc | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLCopyDesc
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLCopyDesc
helpviewer_keywords:
- SQLCopyDesc function [ODBC]
ms.assetid: d5450895-3824-44c4-8aa4-d4f9752a9602
caps.latest.revision: 19
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e8e7383a16b40a966612784e864594588cc37199
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="sqlcopydesc-function"></a>Função SQLCopyDesc
**Conformidade**  
 Versão introduzidas: Conformidade de padrões 3.0 ODBC: 92 ISO  
  
 **Resumo**  
 **SQLCopyDesc** copia informações do descritor de identificador de um descritor para outro.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SQLRETURN SQLCopyDesc(  
     SQLHDESC     SourceDescHandle,  
     SQLHDESC     TargetDescHandle);  
```  
  
## <a name="arguments"></a>Argumentos  
 *SourceDescHandle*  
 [Entrada] Identificador do descritor de origem.  
  
 *TargetDescHandle*  
 [Entrada] Identificador do descritor de destino. O *TargetDescHandle* argumento pode ser um identificador para um descritor de aplicativo ou um IPD. *TargetDescHandle* não pode ser definido como um identificador para um IRD, ou **SQLCopyDesc** retornará SQLSTATE HY016 (não é possível modificar um descritor de linha de implementação).  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>diagnóstico  
 Quando **SQLCopyDesc** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtida chamando **SQLGetDiagRec** com um *HandleType* de SQL _ HANDLE_DESC e um *tratar* de *TargetDescHandle*. Se um inválido *SourceDescHandle* foi passado na chamada de SQL_INVALID_HANDLE será retornado, mas nenhum SQLSTATE será retornado. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLCopyDesc** e explica cada uma no contexto dessa função; a notação "(DM)" precede as descrições de SQLSTATEs retornados pelo Gerenciador de Driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado em contrário.  
  
 Quando um erro é retornado, a chamada para **SQLCopyDesc** imediatamente for cancelada e o conteúdo dos campos a *TargetDescHandle* descritor são indefinidos.  
  
 Porque **SQLCopyDesc** podem ser implementadas chamando **SQLGetDescField** e **SQLSetDescField**, **SQLCopyDesc** pode retornar SQLSTATEs retornados por **SQLGetDescField** ou **SQLSetDescField**.  
  
|SQLSTATE|Erro|Description|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem de informação específica do driver. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|08S01|Falha de link de comunicação|Falha do link de comunicação entre o driver e a fonte de dados ao qual o driver foi conectado antes do processamento da função foi concluída.|  
|HY000|Erro geral|Ocorreu um erro para o qual não houve nenhuma SQLSTATE específico e para o qual nenhuma SQLSTATE específicos de implementação foi definida. A mensagem de erro retornada pelo **SQLGetDiagRec** no  *\*MessageText* buffer descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar a memória necessária para dar suporte a execução ou a conclusão da função.|  
|HY007|Instrução associada não está preparada|*SourceDescHandle* foi associado um IRD, e o identificador de instrução associado não estava no estado preparado ou executado.|  
|HY010|Erro de sequência de função|(DM) o descritor de manipular *SourceDescHandle* ou *TargetDescHandle* foi associado um *StatementHandle* para o qual uma função de execução assíncrona (não Este um) foi chamado e ainda estava em execução quando esta função foi chamada.<br /><br /> (DM) o descritor de manipular *SourceDescHandle* ou *TargetDescHandle* foi associado um *StatementHandle* para o qual **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, ou **SQLSetPos** foi chamado e retornou SQL_NEED_DATA. Essa função foi chamada antes de dados foi enviados para todas as colunas ou parâmetros de dados em execução.<br /><br /> (DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado a *SourceDescHandle* ou *TargetDescHandle*. Essa função assíncrona ainda estava em execução quando o **SQLCopyDesc** função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, ou **SQLMoreResults** foi chamado para uma das alças de instrução associadas a *SourceDescHandle* ou *TargetDescHandle* e retornado SQL_PARAM_DATA_AVAILABLE. Essa função foi chamada antes de recuperação para todos os parâmetros de fluxo de dados.|  
|HY013|Erro de gerenciamento de memória|Não foi possível processar a chamada de função porque os objetos de memória subjacente não podem ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY016|Não é possível modificar um descritor de linha de implementação|*TargetDescHandle* foi associado um IRD.|  
|HY021|Informações do descritor inconsistentes|As informações de descritor verificadas durante uma verificação de consistência não estavam consistentes. Para obter mais informações, consulte "Verificações de consistência" **SQLSetDescField**.|  
|HY092|Identificador de atributo/opção inválido|A chamada para **SQLCopyDesc** solicitado uma chamada para **SQLSetDescField**, mas  *\*ValuePtr* não era válido para o *FieldIdentifier* argumento *TargetDescHandle*.|  
|HY117|Conexão está suspenso devido ao estado de transação desconhecido. Somente Desconecte e funções de somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tempo limite de Conexão expirou|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não dá suporte a esta função|O driver em (DM) associado a *SourceDescHandle* ou *TargetDescHandle* não oferece suporte para a função.|  
  
## <a name="comments"></a>Comentários  
 Uma chamada para **SQLCopyDesc** cópias de lidar com os campos do descritor de origem para o identificador do descritor de destino. Campos podem ser copiados somente para um descritor de aplicativo ou um IPD, mas não para um IRD. Campos podem ser copiados de um aplicativo ou um descritor de implementação.  
  
 Campos podem ser copiados de um IRD somente se o identificador de instrução está no estado preparado ou executado; Caso contrário, a função retornará SQLSTATE HY007 (a instrução associada não está preparada).  
  
 Campos podem ser copiados de um IPD se ou não uma instrução foi preparada. Se uma instrução SQL com parâmetros dinâmicos foi preparada e preenchimento automático do IPD é compatível e habilitado, o IPD é preenchida pelo driver. Quando **SQLCopyDesc** é chamado com o IPD como o *SourceDescHandle*, os campos populados são copiados. Se o IPD não é populado pelo driver, o conteúdo dos campos originalmente o IPD é copiado.  
  
 Todos os campos do descritor, exceto SQL_DESC_ALLOC_TYPE (que especifica se o identificador do descritor automaticamente ou explicitamente alocado), são copiados, se o campo está definido para o descritor de destino ou não. Campos copiados substituem os campos existentes.  
  
 O driver copia todos os campos de descritor se o *SourceDescHandle* e *TargetDescHandle* argumentos estão associados com o mesmo driver, mesmo se os drivers estão em duas conexões diferentes ou ambientes. Se o *SourceDescHandle* e *TargetDescHandle* argumentos estão associados a diferentes drivers, o Gerenciador de Driver copia os campos definidos pelo ODBC, mas não copiar campos definidos pelo driver ou campos que não são definidas pelo ODBC para o tipo de descritor.  
  
 A chamada para **SQLCopyDesc** anulada imediatamente se ocorrer um erro.  
  
 Quando o campo SQL_DESC_DATA_PTR é copiado, é realizada uma verificação de consistência no descritor de destino. Se a verificação de consistência falhar, o SQLSTATE HY021 (informações de descritor inconsistentes) serão retornadas e a chamada para **SQLCopyDesc** imediatamente é anulada. Para obter mais informações sobre as verificações de consistência, consulte "Verificações de consistência" [função SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md).  
  
 Identificadores de descritor podem ser copiados em conexões mesmo se a conexão estiver em ambientes diferentes. Se o Gerenciador de Driver detecta que a origem e o descritor de destino identificadores não pertencem a mesma conexão e duas conexões pertencerem para separar os drivers, ele implementa **SQLCopyDesc** executando um campo por campo Copiar usando **SQLGetDescField** e **SQLSetDescField**.  
  
 Quando **SQLCopyDesc** é chamado com um *SourceDescHandle* em um driver e uma *TargetDescHandle* em outro driver, a fila de erros do  *SourceDescHandle* está desmarcada. Isso ocorre porque **SQLCopyDesc** nesse caso é implementado por chamadas para **SQLGetDescField** e **SQLSetDescField**.  
  
> [!NOTE]  
>  Um aplicativo poderá associar um indicador de descritor alocado explicitamente com um *StatementHandle*, em vez de chamar **SQLCopyDesc** para copiar os campos de um descritor para outro. Um descritor explicitamente alocado pode ser associado a outro *StatementHandle* na mesma *identificador da conexão* definindo a instrução SQL_ATTR_APP_ROW_DESC ou SQL_ATTR_APP_PARAM_DESC o atributo para o identificador do descritor alocado explicitamente. Quando isso for feito, **SQLCopyDesc** não precisa ser chamado para copiar valores de campo do descritor de um descritor para outro. Um identificador do descritor não pode ser associado com um *StatementHandle* em outro *identificador da conexão*, no entanto; para usar os mesmos valores de campo de descritor no *StatementHandles*em diferentes *ConnectionHandles*, **SQLCopyDesc** precisa ser chamado.  
  
 Para obter uma descrição dos campos em um cabeçalho do descritor ou registro, consulte [função SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md). Para obter mais informações sobre os descritores, consulte [descritores](../../../odbc/reference/develop-app/descriptors.md).  
  
## <a name="copying-rows-between-tables"></a>Copiando linhas entre tabelas  
 Um aplicativo pode copiar dados de uma tabela para outra sem copiar os dados no nível do aplicativo. Para fazer isso, o aplicativo associa os mesmos buffers de dados e as informações de descritor para uma instrução que busca os dados e a instrução que insere os dados em uma cópia. Isso pode ser feito compartilhando um descritor de aplicativo (associando um descritor alocado explicitamente como descartar para uma instrução e APD em outro) ou usando **SQLCopyDesc** para copiar as associações entre a descartar e APD das duas instruções. Se as instruções estão em conexões diferentes, **SQLCopyDesc** deve ser usado. Além disso, **SQLCopyDesc** precisa ser chamado para copiar as associações entre o IRD e IPD das duas instruções. Ao copiar entre instruções sobre a mesma conexão, o tipo de informação SQL_ACTIVE_STATEMENTS retornada pelo driver para uma chamada para **SQLGetInfo** deve ser maior que 1 para essa operação seja bem-sucedida. (Isso não é o caso quando copiando entre conexões.)  
  
### <a name="code-example"></a>Exemplo de código  
 No exemplo a seguir, as operações de descritor são usadas para copiar os campos da tabela PartsSource na tabela PartsCopy. O conteúdo da tabela PartsSource é buscado em buffers do conjunto de linhas no *hstmt0*. Esses valores são usados como parâmetros de uma instrução INSERT em *hstmt1* para preencher as colunas da tabela PartsCopy. Para fazer isso, os campos ird de *hstmt0* são copiados para os campos do IPD de *hstmt1*e os campos de descartar de *hstmt0* são copiados para os campos de APD de *hstmt1*. Use **SQLSetDescField** para definir o atributo SQL_DESC_PARAMETER_TYPE do IPD para SQL_PARAM_INPUT quando você copia campos IRD de uma instrução com parâmetros de saída para campos IPD que precisam ser parâmetros de entrada.  
  
```  
#define ROWS 100  
#define DESC_LEN 50  
#define SQL_SUCCEEDED(rc) (rc == SQL_SUCCESS || rc == SQL_SUCCESS_WITH_INFO)  
  
// Template for a row  
typedef struct {  
   SQLINTEGER   sPartID;  
   SQLINTEGER   cbPartID;  
   SQLUCHAR     szDescription[DESC_LENGTH];  
   SQLINTEGER   cbDescription;  
   REAL         sPrice;  
   SQLINTEGER   cbPrice;  
} PartsSource;  
  
PartsSource    rget[ROWS];          // rowset buffer  
SQLUSMALLINT   sts_ptr[ROWS];       // status pointer  
SQLHSTMT       hstmt0, hstmt1;  
SQLHDESC       hArd0, hIrd0, hApd1, hIpd1;  
  
// ARD and IRD of hstmt0  
SQLGetStmtAttr(hstmt0, SQL_ATTR_APP_ROW_DESC, &hArd0, 0, NULL);  
SQLGetStmtAttr(hstmt0, SQL_ATTR_IMP_ROW_DESC, &hIrd0, 0, NULL);  
  
// APD and IPD of hstmt1  
SQLGetStmtAttr(hstmt1, SQL_ATTR_APP_PARAM_DESC, &hApd1, 0, NULL);  
SQLGetStmtAttr(hstmt1, SQL_ATTR_IMP_PARAM_DESC, &hIpd1, 0, NULL);  
  
// Use row-wise binding on hstmt0 to fetch rows  
SQLSetStmtAttr(hstmt0, SQL_ATTR_ROW_BIND_TYPE, (SQLPOINTER) sizeof(PartsSource), 0);  
  
// Set rowset size for hstmt0  
SQLSetStmtAttr(hstmt0, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER) ROWS, 0);  
  
// Execute a select statement  
SQLExecDirect(hstmt0, "SELECT PARTID, DESCRIPTION, PRICE FROM PARTS ORDER BY 3, 1, 2"",  
               SQL_NTS);  
  
// Bind  
SQLBindCol(hstmt0, 1, SQL_C_SLONG, rget[0].sPartID, 0,   
   &rget[0].cbPartID);  
SQLBindCol(hstmt0, 2, SQL_C_CHAR, &rget[0].szDescription, DESC_LEN,   
   &rget[0].cbDescription);  
SQLBindCol(hstmt0, 3, SQL_C_FLOAT, rget[0].sPrice,   
   0, &rget[0].cbPrice);  
  
// Perform parameter bindings on hstmt1.   
SQLCopyDesc(hArd0, hApd1);  
SQLCopyDesc(hIrd0, hIpd1);  
  
// Set the array status pointer of IRD  
SQLSetStmtAttr(hstmt0, SQL_ATTR_ROW_STATUS_PTR, sts_ptr, SQL_IS_POINTER);  
  
// Set the ARRAY_STATUS_PTR field of APD to be the same  
// as that in IRD.  
SQLSetStmtAttr(hstmt1, SQL_ATTR_PARAM_OPERATION_PTR, sts_ptr, SQL_IS_POINTER);  
  
// Set the hIpd1 records as input parameters  
rc = SQLSetDescField(hIpd1, 1, SQL_DESC_PARAMETER_TYPE, (SQLPOINTER)SQL_PARAM_INPUT, SQL_IS_INTEGER);  
rc = SQLSetDescField(hIpd1, 2, SQL_DESC_PARAMETER_TYPE, (SQLPOINTER)SQL_PARAM_INPUT, SQL_IS_INTEGER);  
rc = SQLSetDescField(hIpd1, 3, SQL_DESC_PARAMETER_TYPE, (SQLPOINTER)SQL_PARAM_INPUT, SQL_IS_INTEGER);  
  
// Prepare an insert statement on hstmt1. PartsCopy is a copy of  
// PartsSource  
SQLPrepare(hstmt1, "INSERT INTO PARTS_COPY VALUES (?, ?, ?)", SQL_NTS);  
  
// In a loop, fetch a rowset, and copy the fetched rowset to PARTS_COPY  
  
rc = SQLFetchScroll(hstmt0, SQL_FETCH_NEXT, 0);  
while (SQL_SUCCEEDED(rc)) {  
  
   // After the call to SQLFetchScroll, the status array has row   
   // statuses. This array is used as input status in the APD  
   // and hence determines which elements of the rowset buffer  
   // are inserted.  
   SQLExecute(hstmt1);  
  
   rc = SQLFetchScroll(hstmt0, SQL_FETCH_NEXT, 0);  
} // while  
```  
  
### <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Obtendo vários campos de descritor|[Função SQLGetDescRec](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|Configuração de um campo de descritor único|[Função SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|Definindo vários campos de descritor|[Função SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Referência de API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)

