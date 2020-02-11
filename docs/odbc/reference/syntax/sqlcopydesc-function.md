---
title: Função SQLCopyDesc | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLCopyDesc
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLCopyDesc
helpviewer_keywords:
- SQLCopyDesc function [ODBC]
ms.assetid: d5450895-3824-44c4-8aa4-d4f9752a9602
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8aec6dc776f5fdd84932be089e9503f0083a49c2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68345483"
---
# <a name="sqlcopydesc-function"></a>Função SQLCopyDesc
**Conformidade**  
 Versão introduzida: conformidade de padrões do ODBC 3,0: ISO 92  
  
 **Resumo**  
 **SQLCopyDesc** copia informações de descritor de um identificador de descritor para outro.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLCopyDesc(  
     SQLHDESC     SourceDescHandle,  
     SQLHDESC     TargetDescHandle);  
```  
  
## <a name="arguments"></a>Argumentos  
 *SourceDescHandle*  
 Entrada Identificador do descritor de origem.  
  
 *TargetDescHandle*  
 Entrada Identificador do descritor de destino. O argumento *TargetDescHandle* pode ser um identificador para um descritor de aplicativo ou um IPD. *TargetDescHandle* não pode ser definido como um identificador para um IRD, ou **SQLCOPYDESC** retornará SQLSTATE HY016 (não é possível modificar um descritor de linha de implementação).  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **SQLCopyDesc** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido chamando **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_DESC e um *identificador* de *TargetDescHandle*. Se um *SourceDescHandle* inválido foi passado na chamada, SQL_INVALID_HANDLE será retornado, mas nenhum SQLSTATE será retornado. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLCopyDesc** e explica cada um no contexto dessa função; a notação "(DM)" precede as descrições de sqlstates retornadas pelo Gerenciador de driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
 Quando um erro é retornado, a chamada para **SQLCopyDesc** é anulada imediatamente e o conteúdo dos campos no descritor *TargetDescHandle* são indefinidos.  
  
 Como **SQLCopyDesc** pode ser implementado chamando **SQLGetDescField** e **SQLSetDescField**, **SQLCopyDesc** pode retornar sqlstates retornado por **SQLGetDescField** ou **SQLSetDescField**.  
  
|SQLSTATE|Erro|DESCRIÇÃO|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa específica do driver. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|08S01|Falha no link de comunicação|O link de comunicação entre o driver e a fonte de dados ao qual o driver foi conectado falhou antes da função concluir o processamento.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia um SQLSTATE específico e para o qual nenhum SQLSTATE específico de implementação foi definido. A mensagem de erro retornada por **SQLGetDiagRec** no buffer * \*MessageText* descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar a memória necessária para dar suporte à execução ou à conclusão da função.|  
|HY007|A instrução associada não está preparada|*SourceDescHandle* foi associado a um IRD, e o identificador de instrução associado não estava no estado preparado ou executado.|  
|HY010|Erro de sequência de função|(DM) o identificador do descritor em *SourceDescHandle* ou *TargetDescHandle* foi associado a um *StatementHandle* para o qual uma função de execução assíncrona (não esta) foi chamada e ainda estava em execução quando essa função foi chamada.<br /><br /> (DM) o identificador do descritor em *SourceDescHandle* ou *TargetDescHandle* foi associado a um *StatementHandle* para o qual **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**ou **SQLSetPos** foi chamado e retornou SQL_NEED_DATA. Esta função foi chamada antes de os dados serem enviados para todos os parâmetros de dados em execução ou colunas.<br /><br /> (DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado ao *SourceDescHandle* ou *TargetDescHandle*. Esta função assíncrona ainda estava em execução quando a função **SQLCopyDesc** foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**ou **SQLMoreResults** foi chamado para um dos identificadores de instrução associados ao *SourceDescHandle* ou ao *TargetDescHandle* e retornou SQL_PARAM_DATA_AVAILABLE. Esta função foi chamada antes de os dados serem recuperados para todos os parâmetros transmitidos.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não puderam ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY016|Não é possível modificar um descritor de linha de implementação|*TargetDescHandle* foi associado a um IRD.|  
|HY021|Informações de descritor inconsistentes|As informações de descritor verificadas durante uma verificação de consistência não estavam consistentes. Para obter mais informações, consulte "verificações de consistência" em **SQLSetDescField**.|  
|HY092|Identificador de atributo/opção inválido|A chamada para **SQLCopyDesc** solicitou uma chamada para **SQLSetDescField**, mas * \*ValuePtr* não era válida para o argumento *FieldIdentifier* em *TargetDescHandle*.|  
|HY117|A conexão foi suspensa devido a um estado de transação desconhecido. Somente funções de desconexão e somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tempo limite de conexão expirado|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|O driver não oferece suporte a essa função|(DM) o driver associado ao *SourceDescHandle* ou *TargetDescHandle* não oferece suporte à função.|  
  
## <a name="comments"></a>Comentários  
 Uma chamada para **SQLCopyDesc** copia os campos do identificador do descritor de origem para o identificador do descritor de destino. Os campos podem ser copiados somente para um descritor de aplicativo ou um IPD, mas não para um IRD. Os campos podem ser copiados de um aplicativo ou de um descritor de implementação.  
  
 Os campos podem ser copiados de um IRD somente se o identificador da instrução estiver no estado preparado ou executado; caso contrário, a função retornará SQLSTATE HY007 (a instrução associada não será preparada).  
  
 Os campos podem ser copiados de um IPD se uma instrução tiver sido preparada ou não. Se uma instrução SQL com parâmetros dinâmicos tiver sido preparada e a população automática do IPD tiver suporte e estiver habilitada, o IPD será preenchido pelo driver. Quando **SQLCopyDesc** é chamado com o IPD como *SourceDescHandle*, os campos preenchidos são copiados. Se o IPD não for preenchido pelo driver, o conteúdo dos campos originalmente no IPD será copiado.  
  
 Todos os campos do descritor, exceto SQL_DESC_ALLOC_TYPE (que especifica se o identificador do descritor foi alocado automaticamente ou explicitamente), são copiados, se o campo está ou não definido para o descritor de destino. Os campos copiados substituem os campos existentes.  
  
 O driver copiará todos os campos de descritor se os argumentos *SourceDescHandle* e *TargetDescHandle* estiverem associados ao mesmo Driver, mesmo que os drivers estejam em duas conexões ou ambientes diferentes. Se os argumentos *SourceDescHandle* e *TargetDescHandle* estiverem associados a drivers diferentes, o Gerenciador de driver copiará campos definidos pelo ODBC, mas não copiará campos ou campos definidos pelo driver que não são definidos pelo ODBC para o tipo de descritor.  
  
 A chamada para **SQLCopyDesc** será anulada imediatamente se ocorrer um erro.  
  
 Quando o campo de SQL_DESC_DATA_PTR é copiado, uma verificação de consistência é executada no descritor de destino. Se a verificação de consistência falhar, SQLSTATE HY021 (informações de descritor inconsistentes) será retornado e a chamada para **SQLCopyDesc** será anulada imediatamente. Para obter mais informações sobre verificações de consistência, consulte "verificações de consistência" na [função SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md).  
  
 Identificadores de descritor podem ser copiados entre conexões, mesmo se as conexões estiverem em ambientes diferentes. Se o Gerenciador de driver detectar que os identificadores de descritor de origem e de destino não pertencem à mesma conexão e as duas conexões pertencem a drivers separados, ele implementa o **SQLCopyDesc** executando uma cópia Field-by-Field usando **SQLGetDescField** e **SQLSetDescField**.  
  
 Quando **SQLCopyDesc** é chamado com um *SourceDescHandle* em um driver e um *TargetDescHandle* em outro driver, a fila de erros do *SourceDescHandle* é apagada. Isso ocorre porque **SQLCopyDesc** nesse caso é implementado por chamadas para **SQLGetDescField** e **SQLSetDescField**.  
  
> [!NOTE]  
>  Um aplicativo pode ser capaz de associar um identificador de descritor explicitamente alocado a um *StatementHandle*, em vez de chamar **SQLCopyDesc** para copiar campos de um descritor para outro. Um descritor explicitamente alocado pode ser associado a outro *StatementHandle* no mesmo *ConnectionHandle* , definindo o atributo SQL_ATTR_APP_ROW_DESC ou SQL_ATTR_APP_PARAM_DESC instrução como o identificador do descritor explicitamente alocado. Quando isso é feito, **SQLCopyDesc** não precisa ser chamado para copiar valores de campo de descritor de um descritor para outro. Um identificador de descritor não pode ser associado a um *StatementHandle* em outro *ConnectionHandle*; no entanto; para usar os mesmos valores de campo de descritor em *StatementHandles* em *ConnectionHandles*diferentes, **SQLCopyDesc** deve ser chamado.  
  
 Para obter uma descrição dos campos em um cabeçalho ou registro de descritor, consulte a [função SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md). Para obter mais informações sobre descritores, consulte [descritores](../../../odbc/reference/develop-app/descriptors.md).  
  
## <a name="copying-rows-between-tables"></a>Copiando linhas entre tabelas  
 Um aplicativo pode copiar dados de uma tabela para outra sem copiar os dados no nível do aplicativo. Para fazer isso, o aplicativo associa os mesmos buffers de dados e informações de descritor a uma instrução que busca os dados e a instrução que insere os dados em uma cópia. Isso pode ser feito compartilhando um descritor de aplicativo (associando um descritor explicitamente alocado como ARD para uma instrução e o APD em outro) ou usando **SQLCopyDesc** para copiar as associações entre ARD e APD das duas instruções. Se as instruções estiverem em conexões diferentes, **SQLCopyDesc** deverá ser usado. Além disso, **SQLCopyDesc** precisa ser chamado para copiar as associações entre o IRD e o IPD das duas instruções. Ao copiar entre instruções na mesma conexão, o tipo de informação SQL_ACTIVE_STATEMENTS retornado pelo driver para uma chamada para **SQLGetInfo** deve ser maior que 1 para que essa operação tenha sucesso. (Esse não é o caso ao copiar entre conexões.)  
  
### <a name="code-example"></a>Exemplo de código  
 No exemplo a seguir, as operações de descritor são usadas para copiar os campos da tabela PartName na tabela PartsCopy. O conteúdo da tabela perparts é buscado em buffers de conjunto de linhas no *hstmt0*. Esses valores são usados como parâmetros de uma instrução INSERT em *hstmt1* para popular as colunas da tabela PartsCopy. Para fazer isso, os campos de IRD de *hstmt0* são copiados para os campos do IPD de *hstmt1*, e os campos do ARD de *hstmt0* são copiados para os campos do APD de *hstmt1*. Use **SQLSetDescField** para definir o atributo SQL_DESC_PARAMETER_TYPE do IPD como SQL_PARAM_INPUT ao copiar campos IRD de uma instrução com parâmetros de saída para os campos IPD que precisam ser parâmetros de entrada.  
  
```cpp  
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
|Configurando um único campo de descritor|[Função SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|Configurando vários campos de descritor|[Função SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
