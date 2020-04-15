---
title: Função SQLGetCursorName | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetCursorName
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetCursorName
helpviewer_keywords:
- SQLGetCursorName function [ODBC]
ms.assetid: e6e92199-7bb6-447c-8987-049a4c6ce05d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d3ac65dc07897ddc789ee03b06b1bc1f71d37c3c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285544"
---
# <a name="sqlgetcursorname-function"></a>Função SQLGetCursorName
**Conformidade**  
 Versão introduzida: ODBC 1.0 Standards Compliance: ISO 92  
  
 **Resumo**  
 **SQLGetCursorName** retorna o nome do cursor associado a uma declaração especificada.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLGetCursorName(  
     SQLHSTMT        StatementHandle,  
     SQLCHAR *       CursorName,  
     SQLSMALLINT     BufferLength,  
     SQLSMALLINT *   NameLengthPtr);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Alça de declaração.  
  
 *CursorNome*  
 [Saída] Pointer para um buffer no qual para retornar o nome do cursor.  
  
 Se *cursorName* for NULL, *NameLengthPtr* ainda retornará o número total de caracteres (excluindo o caractere de rescisão nula para dados de caracteres) disponível para retornar no buffer apontado pelo *CursorName*.  
  
 *BufferLength*  
 [Entrada] Comprimento \*do *CursorName,* em caracteres. Se o valor no * \*CursorName* for uma seqüência unicode (ao chamar **SQLGetCursorNameW),** o argumento *BufferLength* deve ser um número uniforme.  
  
 *NameLengthPtr*  
 [Saída] Ponteiro para memória na qual retornar o número total de caracteres (excluindo \*o caractere de rescisão nula) disponível para retornar no *CursorName*. Se o número de caracteres disponíveis para retornar for maior ou \*igual a *BufferLength,* o nome do cursor no *CursorName* será truncado para *BufferLength* menos o comprimento de um caractere de rescisão nula.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **o SQLGetCursorName** retornar SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido ligando para **sqlGetDiagRec** com um *HandleType* de SQL_HANDLE_STMT e uma *alça* de *statementHandle*. A tabela a seguir lista os valores SQLSTATE comumente retornados por **SQLGetCursorName** e explica cada um no contexto desta função; a notação "(DM)" precede as descrições de SQLSTATEs devolvidas pelo Driver Manager. O código de devolução associado a cada valor SQLSTATE é SQL_ERROR, a menos que seja observado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informacional específica do motorista. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|01004|Dados de cordas, truncados direito|O \*buffer *CursorName* não era grande o suficiente para retornar todo o nome do cursor, de modo que o nome do cursor foi truncado. O comprimento do nome do cursor não truncado é devolvido em **NameLengthPtr*. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia SQLSTATE específico e para o qual não foi definido sqlSTATE específico para a implementação. A mensagem de erro retornada pelo **SQLGetDiagRec** no * \** buffer MessageText descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não conseguiu alocar a memória necessária para suportar a execução ou a conclusão da função.|  
|HY010|Erro de seqüência de função|(DM) Uma função de execução assíncrona foi chamada para o cabo de conexão associado ao *StatementHandle*. Esta função assíncrona ainda estava sendo executada quando a função **SQLGetCursorName** foi chamada.<br /><br /> (DM) **SQLExecute,** **SQLExecDirect**ou **SQLMoreResults** foram chamados para o *StatementHandle* e retornaram SQL_PARAM_DATA_AVAILABLE. Esta função foi chamada antes de os dados serem recuperados para todos os parâmetros transmitidos.<br /><br /> (DM) Uma função de execução assíncrona foi chamada para o *StatementHandle* e ainda estava sendo executada quando esta função foi chamada.<br /><br /> (DM) **SQLExecute,** **SQLExecDirect,** **SQLBulkOperations**ou **SQLSetPos** foram chamados para o *StatementHandle* e retornaram SQL_NEED_DATA. Essa função foi chamada antes de os dados serem enviados para todos os parâmetros ou colunas de execução de dados.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não podiam ser acessados, possivelmente devido às baixas condições de memória.|  
|HY015|Nenhum nome do cursor disponível|(DM) O driver era um Driver ODBC*2.x,* não havia cursor aberto na declaração e nenhum nome do cursor havia sido definido com **SQLSetCursorName**.|  
|HY090|Comprimento de seqüência ou buffer inválido|(DM) O valor especificado no argumento *BufferLength* foi inferior a 0.|  
|HY117|A conexão está suspensa devido ao estado de transação desconhecido. Somente funções desconectadas e somente leitura são permitidas.|(DM) Para obter mais informações sobre o estado suspenso, consulte [a função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tempo de tempo de conexão expirado|O período de tempo de tempo de conexão expirou antes que a fonte de dados respondesse à solicitação. O período de tempo de tempo de conexão é definido através **de SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não suporta esta função|(DM) O driver associado ao *StatementHandle* não suporta a função.|  
  
## <a name="comments"></a>Comentários  
 Os nomes do cursor são usados apenas em instruções de atualização e exclusão posicionadas (por **exemplo,** _UPDATE-name_ ... **ONDE CORRENTE DE** _cursor-nome_). Para obter mais informações, consulte [Instruções de atualização posicionada e exclusão](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md). Se o aplicativo não chamar **SQLSetCursorName** para definir um nome de cursor, o driver gerará um nome. Este nome começa com as letras SQL_CUR.  
  
> [!NOTE]
>  Em ODBC 2 *.x,* quando não havia cursor aberto e nenhum nome havia sido definido por uma chamada para **SQLSetCursorName**, uma chamada para **SQLGetCursorName** retornou SQLSTATE HY015 (Nenhum nome do cursor disponível). Em ODBC 3 *.x*, isso não é mais verdade; independentemente de quando **SQLGetCursorName** é chamado, o driver retorna o nome do cursor.  
  
 **SQLGetCursorName** retorna o nome de um cursor se o nome foi criado ou não explicitamente ou implicitamente. Um nome do cursor é gerado implicitamente se **SQLSetCursorName** não for chamado. **SQLSetCursorName** pode ser chamado para renomear um cursor em uma declaração, desde que o cursor esteja em um estado alocado ou preparado.  
  
 Um nome do cursor definido explicitamente ou implicitamente permanece definido até que o *StatementHandle* com o qual está associado seja descartado, usando **SQLFreeHandle** com um *HandleType* de SQL_HANDLE_STMT.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Executando uma declaração SQL|[Função SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Executando uma declaração SQL preparada|[Função SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Preparando uma declaração para execução|[Função SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|  
|Definindo um nome do cursor|[Função SQLSetCursorName](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API oDBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
