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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ef1fa5b319e8d72d5b70e6f2010e493eec6f844a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301223"
---
# <a name="sqlcopydesc-function"></a>Função SQLCopyDesc
**Conformidade**  
 Versão introduzida: ODBC 3.0 Standards Compliance: ISO 92  
  
 **Resumo**  
 **SQLCopyDesc** copia informações do descritor de uma alça de descritor para outra.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLCopyDesc(  
     SQLHDESC     SourceDescHandle,  
     SQLHDESC     TargetDescHandle);  
```  
  
## <a name="arguments"></a>Argumentos  
 *SourceDescHandle*  
 [Entrada] Alça do descritor fonte.  
  
 *TargetDescHandle*  
 [Entrada] Alça do descritor alvo. O *argumento TargetDescHandle* pode ser uma alça para um descritor de aplicativo ou um IPD. *TargetDescHandle* não pode ser definido como um cabo para um IRD, ou **O SQLCopyDesc** retornará o SQLSTATE HY016 (não é possível modificar um descritor da linha de implementação).  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **o SQLCopyDesc** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido ligando para **sqlGetDiagRec** com um *HandleType* de SQL_HANDLE_DESC e uma *alça* de *TargetDescHandle*. Se um *SourceDescHandle* inválido foi aprovado na chamada, SQL_INVALID_HANDLE serão devolvidos, mas nenhum SQLSTATE será devolvido. A tabela a seguir lista os valores SQLSTATE comumente retornados pelo **SQLCopyDesc** e explica cada um no contexto desta função; a notação "(DM)" precede as descrições de SQLSTATEs devolvidas pelo Driver Manager. O código de devolução associado a cada valor SQLSTATE é SQL_ERROR, a menos que seja observado o contrário.  
  
 Quando um erro é retornado, a chamada para **SQLCopyDesc** é imediatamente abortada e o conteúdo dos campos no descritor *TargetDescHandle* são indefinidos.  
  
 Como **o SQLCopyDesc** pode ser implementado ligando para **SQLGetDescField** e **SQLSetDescField,** **o SQLCopyDesc** pode retornar SQLSTATEs retornado por **SQLGetDescField** ou **SQLSetDescField**.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informacional específica do motorista. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|08S01|Falha no link de comunicação|O link de comunicação entre o driver e a fonte de dados à qual o driver estava conectado falhou antes da função ser concluída.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia SQLSTATE específico e para o qual não foi definido sqlSTATE específico para a implementação. A mensagem de erro retornada pelo **SQLGetDiagRec** no * \** buffer MessageText descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não conseguiu alocar a memória necessária para suportar a execução ou a conclusão da função.|  
|HY007|A declaração associada não está preparada|*SourceDescHandle* foi associado a um IRD, e a alça de declaração associada não estava no estado preparado ou executado.|  
|HY010|Erro de seqüência de função|(DM) O cabo do descritor em *SourceDescHandle* ou *TargetDescHandle* estava associado a um *StatementHandle* para o qual uma função de execução assíncrona (não esta) foi chamada e ainda estava sendo executada quando esta função foi chamada.<br /><br /> (DM) A alça do descritor no *SourceDescHandle* ou *targetDescHandle* foi associada a um *StatementHandle* para o qual **SQLExecute,** **SQLExecDirect,** **SQLBulkOperations**ou **SQLSetPos** foram chamados e retornados SQL_NEED_DATA. Essa função foi chamada antes de os dados serem enviados para todos os parâmetros ou colunas de execução de dados.<br /><br /> (DM) Uma função de execução assíncrona foi chamada para o cabo de conexão associado ao *SourceDescHandle* ou *TargetDescHandle*. Esta função assíncrona ainda estava sendo executada quando a função **SQLCopyDesc** foi chamada.<br /><br /> (DM) **SQLExecute,** **SQLExecDirect**ou **SQLMoreResults** foi chamado para uma das alças de declaração associadas ao *SourceDescHandle* ou *TargetDescHandle* e retornou SQL_PARAM_DATA_AVAILABLE. Esta função foi chamada antes de os dados serem recuperados para todos os parâmetros transmitidos.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não podiam ser acessados, possivelmente devido às baixas condições de memória.|  
|HY016|Não é possível modificar um descritor de linha de implementação|*TargetDescHandle* estava associado a um IRD.|  
|HY021|Informações dedescritores inconsistentes|As informações do descritor verificadas durante uma verificação de consistência não foram consistentes. Para obter mais informações, consulte "Verificações de consistência" no **SQLSetDescField**.|  
|HY092|Identificador de atributo/opção inválido|A chamada para **SQLCopyDesc** motivou uma chamada para **SQLSetDescField,** mas * \*o ValuePtr* não era válido para o argumento *FieldIdentifier* no *TargetDescHandle*.|  
|HY117|A conexão está suspensa devido ao estado de transação desconhecido. Somente funções desconectadas e somente leitura são permitidas.|(DM) Para obter mais informações sobre o estado suspenso, consulte [a função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tempo de tempo de conexão expirado|O período de tempo de tempo de conexão expirou antes que a fonte de dados respondesse à solicitação. O período de tempo de tempo de conexão é definido através **de SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não suporta esta função|(DM) O driver associado ao *SourceDescHandle* ou *TargetDescHandle* não suporta a função.|  
  
## <a name="comments"></a>Comentários  
 Uma chamada para **SQLCopyDesc** copia os campos da alça do descritor de origem para a alça do descritor de destino. Os campos podem ser copiados apenas para um descritor de aplicativo ou um IPD, mas não para um IRD. Os campos podem ser copiados de um aplicativo ou de um descritor de implementação.  
  
 Os campos só podem ser copiados de um IRD se a alça da declaração estiver no estado preparado ou executado; caso contrário, a função retorna SQLSTATE HY007 (a declaração associada não está preparada).  
  
 Os campos podem ser copiados de um IPD se uma declaração foi ou não preparada. Se uma declaração SQL com parâmetros dinâmicos tiver sido preparada e a população automática do IPD for suportada e habilitada, o IPD será preenchido pelo driver. Quando **o SQLCopyDesc** é chamado com o IPD como *SourceDescHandle,* os campos preenchidos são copiados. Se o IPD não for preenchido pelo driver, o conteúdo dos campos originalmente no IPD será copiado.  
  
 Todos os campos do descritor, exceto SQL_DESC_ALLOC_TYPE (que especifica se a alça do descritor foi alocada automaticamente ou explicitamente), são copiadas, quer o campo seja definido ou não para o descritor de destino. Campos copiados sobreescrevem os campos existentes.  
  
 O driver copia todos os campos de descritores se os *argumentos SourceDescHandle* e *TargetDescHandle* estiverem associados ao mesmo driver, mesmo que os drivers estejam em duas conexões ou ambientes diferentes. Se os *argumentos SourceDescHandle* e *TargetDescHandle* estiverem associados a diferentes drivers, o Driver Manager copiará campos definidos pelo ODBC, mas não copiará campos ou campos definidos pelo driver que não são definidos pela ODBC para o tipo de descritor.  
  
 A chamada para **SQLCopyDesc** é abortada imediatamente se ocorrer um erro.  
  
 Quando o campo SQL_DESC_DATA_PTR é copiado, uma verificação de consistência é realizada no descritor de destino. Se a verificação de consistência falhar, o SQLSTATE HY021 (informações inconsistentes do descritor) é retornado e a chamada para **SQLCopyDesc** é imediatamente abortada. Para obter mais informações sobre verificações de consistência, consulte "Verificações de consistência" na [função SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md).  
  
 As alças do descritor podem ser copiadas entre conexões mesmo que as conexões estejam em ambientes diferentes. Se o Gerenciador de driver detectar que as alças do descritor de origem e destino não pertencem à mesma conexão e as duas conexões pertencem a drivers separados, ele implementará **o SQLCopyDesc** executando uma cópia de campo por campo usando **SQLGetDescField** e **SQLSetDescField**.  
  
 Quando **o SQLCopyDesc** é chamado com um *SourceDescHandle* em um driver e um *TargetDescHandle* em outro driver, a fila de erros do *SourceDescHandle* é limpa. Isso ocorre porque **o SQLCopyDesc,** neste caso, é implementado por chamadas para **SQLGetDescField** e **SQLSetDescField**.  
  
> [!NOTE]  
>  Um aplicativo pode ser capaz de associar uma alça descritor explicitamente alocada com um *StatementHandle*, em vez de chamar **o SQLCopyDesc** para copiar campos de um descritor a outro. Um descritor explicitamente alocado pode ser associado a outra *InstruçãoLidar* na mesma *ConexãoLidar* definindo o atributo de declaração SQL_ATTR_APP_ROW_DESC ou SQL_ATTR_APP_PARAM_DESC para a alça do descritor explicitamente alocado. Quando isso é feito, **o SQLCopyDesc** não precisa ser chamado para copiar valores de campo descritor de um descritor para outro. No entanto, uma alça de descritor não pode ser associada a uma *declaraçãoHandle* em outra *ConexãoHandle;* para usar os mesmos valores de campo do descritor em *StatementHandles* em *diferentes ConexõesHandles,* **SQLCopyDesc** tem que ser chamado.  
  
 Para obter uma descrição dos campos em um cabeçalho ou registro do descritor, consulte [SQLSetDescField Function](../../../odbc/reference/syntax/sqlsetdescfield-function.md). Para obter mais informações sobre descritores, consulte [Descritores](../../../odbc/reference/develop-app/descriptors.md).  
  
## <a name="copying-rows-between-tables"></a>Copiando linhas entre tabelas  
 Um aplicativo pode copiar dados de uma tabela para outra sem copiar os dados no nível do aplicativo. Para isso, o aplicativo vincula os mesmos buffers de dados e informações do descritor a uma instrução que busca os dados e a instrução que insere os dados em uma cópia. Isso pode ser feito compartilhando um descritor de aplicativo (vinculando um descritor explicitamente alocado como ard para uma instrução e apd em outra) ou usando **SQLCopyDesc** para copiar as vinculações entre o ARD e o APD das duas declarações. Se as instruções estiverem em diferentes conexões, **o SQLCopyDesc** deve ser usado. Além disso, **o SQLCopyDesc** deve ser chamado para copiar as vinculações entre o IRD e o IPD das duas declarações. Ao copiar através de declarações na mesma conexão, o SQL_ACTIVE_STATEMENTS tipo de informação retornado pelo driver para uma chamada ao **SQLGetInfo** deve ser maior que 1 para que essa operação tenha sucesso. (Este não é o caso ao copiar em conexões.)  
  
### <a name="code-example"></a>Exemplo de código  
 No exemplo a seguir, as operações do descritor são usadas para copiar os campos da tabela PartsSource na tabela PartsCopy. O conteúdo da tabela PartsSource é obtido em buffers de conjunto de linhas em *hstmt0*. Esses valores são usados como parâmetros de uma instrução INSERT no *hstmt1* para preencher as colunas da tabela PartsCopy. Para isso, os campos do IRD de *hstmt0* são copiados para os campos do IPD de *hstmt1*, e os campos do ARD de *hstmt0* são copiados para os campos da APD de *hstmt1*. Use **SQLSetDescField** para definir o atributo SQL_DESC_PARAMETER_TYPE do IPD para SQL_PARAM_INPUT quando você copiar campos IRD de uma declaração com parâmetros de saída para campos IPD que precisam ser parâmetros de entrada.  
  
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
|Obtendo vários campos de descritores|[Função SQLGetDescRec](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|Definindo um único campo descritor|[Função SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|Configuração de vários campos de descritor|[Função SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API oDBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
