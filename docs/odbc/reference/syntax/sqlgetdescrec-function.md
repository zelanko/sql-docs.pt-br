---
title: Função SQLGetDescRec | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
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
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 569a3708c13a4182e651c902ce7e1f1f9c7711dd
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="sqlgetdescrec-function"></a>Função SQLGetDescRec
**Conformidade**  
 Versão introduzidas: Conformidade de padrões 3.0 ODBC: 92 ISO  
  
 **Resumo**  
 **SQLGetDescRec** retorna as configurações atuais ou valores de vários campos de um registro do descritor. Os campos retornados descrevem o nome, tipo de dados e armazenamento de dados de coluna ou parâmetro.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
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
 [Entrada] Identificador do descritor.  
  
 *RecNumber*  
 [Entrada] Indica que o registro do descritor do qual o aplicativo busca de informações. Registros de descritor são numerados de 1, com o número de registro sendo o registro do indicador de 0. O *RecNumber* argumento deve ser menor ou igual ao valor de SQL_DESC_COUNT. Se *RecNumber* é menor ou igual a SQL_DESC_COUNT, mas a linha não contém dados de uma coluna ou parâmetro, uma chamada para **SQLGetDescRec** retornará os valores padrão dos campos. (Para obter mais informações, consulte "Inicialização de campos de descritor" [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).)  
  
 *Nome*  
 [Saída] Um ponteiro para um buffer no qual retornar o campo SQL_DESC_NAME para o registro do descritor.  
  
 Se *nome* for NULL, *StringLengthPtr* ainda retornará o número total de caracteres (excluindo o caractere null de terminação para dados de caractere) disponíveis para retornar o buffer apontado pelo  *Nome*.  
  
 *BufferLength*  
 [Entrada] Comprimento do **nome* buffer, em caracteres.  
  
 *StringLengthPtr*  
 [Saída] Um ponteiro para um buffer no qual retornar o número de caracteres de dados disponíveis para retornar o \* *nome* buffer, exceto o caractere null de terminação. Se o número de caracteres era maior que ou igual a *BufferLength*, os dados em \* *nome* será truncado para *BufferLength* menos o comprimento de um caractere de terminação NULL e é terminada em nulo pelo driver.  
  
 *TypePtr*  
 [Saída] Um ponteiro para um buffer no qual retornar o valor do campo SQL_DESC_TYPE para registro do descritor.  
  
 *SubTypePtr*  
 [Saída] Para registros cujo tipo é SQL_DATETIME ou SQL_INTERVAL, esse é um ponteiro para um buffer no qual retornar o valor do campo SQL_DESC_DATETIME_INTERVAL_CODE.  
  
 *LengthPtr*  
 [Saída] Um ponteiro para um buffer no qual retornar o valor do campo SQL_DESC_OCTET_LENGTH para registro do descritor.  
  
 *PrecisionPtr*  
 [Saída] Um ponteiro para um buffer no qual retornar o valor do campo SQL_DESC_PRECISION para registro do descritor.  
  
 *ScalePtr*  
 [Saída] Um ponteiro para um buffer no qual retornar o valor do campo SQL_DESC_SCALE para registro do descritor.  
  
 *NullablePtr*  
 [Saída] Um ponteiro para um buffer no qual retornar o valor do campo SQL_DESC_NULLABLE para registro do descritor.  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_NO_DATA ou SQL_INVALID_HANDLE.  
  
 SQL_NO_DATA seja retornado se *RecNumber* é maior que o número atual de registros de descritor.  
  
 SQL_NO_DATA seja retornado se *DescriptorHandle* é um identificador IRD e a instrução está no estado preparado ou executado, mas não havia nenhum cursor aberto associado a ele.  
  
## <a name="diagnostics"></a>diagnóstico  
 Quando **SQLGetDescRec** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtida chamando **SQLGetDiagRec** com um *HandleType* de SQL _ HANDLE_DESC e um *tratar* de *DescriptorHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLGetDescRec** e explica cada uma no contexto dessa função; a notação "(DM)" precede as descrições de SQLSTATEs retornados pelo Gerenciador de Driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado em contrário.  
  
|SQLSTATE|Erro|Description|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem de informação específica do driver. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|01004|Dados de cadeia de caracteres truncados à direita|O buffer \* *nome* não era grande o suficiente para retornar o campo do descritor inteira. Portanto, o campo foi truncado. O comprimento do campo de descritor completo é retornado em **StringLengthPtr*. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|07009|Índice do descritor inválido|O *FieldIdentifier* argumento era um campo de registro, o *RecNumber* argumento foi definido como 0 e o *DescriptorHandle* argumento era um identificador de IPD.<br /><br /> (DM) a *RecNumber* argumento foi definido como 0, e o atributo de instrução SQL_ATTR_USE_BOOKMARKS foi definido para SQL_UB_OFF e o *DescriptorHandle* argumento era um identificador de IRD.<br /><br /> O *RecNumber* argumento era menor do que 0.|  
|08S01|Falha de link de comunicação|Falha do link de comunicação entre o driver e a fonte de dados ao qual o driver foi conectado antes do processamento da função foi concluída.|  
|HY000|Erro geral|Ocorreu um erro para o qual não houve nenhuma SQLSTATE específico e para o qual nenhuma SQLSTATE específicos de implementação foi definida. A mensagem de erro retornada pelo **SQLGetDiagRec** no  *\*MessageText* buffer descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar a memória necessária para dar suporte a execução ou a conclusão da função.|  
|HY007|Instrução associada não está preparada|*DescriptorHandle* foi associado um IRD, e o identificador de instrução associado não estava no estado preparado ou executado.|  
|HY010|Erro de sequência de função|(DM) *DescriptorHandle* foi associado um *StatementHandle* para que uma função de execução assíncrona (não esse um) foi chamada e ainda estava em execução quando esta função foi chamada.<br /><br /> (DM) *DescriptorHandle* foi associado um *StatementHandle* para o qual **SQLExecute**, **SQLExecDirect**,  **SQLBulkOperations**, ou **SQLSetPos** foi chamado e retornou SQL_NEED_DATA. Essa função foi chamada antes de dados foi enviados para todas as colunas ou parâmetros de dados em execução.<br /><br /> (DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado a *DescriptorHandle*. Essa função assíncrona ainda estava em execução quando **SQLGetDescRec** foi chamado.|  
|HY013|Erro de gerenciamento de memória|Não foi possível processar a chamada de função porque os objetos de memória subjacente não podem ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY117|Conexão está suspenso devido ao estado de transação desconhecido. Somente Desconecte e funções de somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tempo limite de Conexão expirou|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não dá suporte a esta função|O driver em (DM) associados *DescriptorHandle* não oferece suporte para a função.|  
  
## <a name="comments"></a>Comentários  
 Um aplicativo pode chamar **SQLGetDescRec** para recuperar os valores dos seguintes campos de descritor para uma única coluna ou parâmetro:  
  
-   SQL_DESC_NAME  
  
-   SQL_DESC_TYPE  
  
-   SQL_DESC_DATETIME_INTERVAL_CODE (para registros cujo tipo é SQL_DATETIME ou SQL_INTERVAL)  
  
-   SQL_DESC_OCTET_LENGTH  
  
-   SQL_DESC_PRECISION  
  
-   SQL_DESC_SCALE  
  
-   SQL_DESC_NULLABLE  
  
 **SQLGetDescRec** não recuperar os valores de campos de cabeçalho.  
  
 Um aplicativo pode evitar o retorno de configuração de um campo, definindo o argumento que corresponde ao campo para um ponteiro nulo.  
  
 Quando um aplicativo chama **SQLGetDescRec** para recuperar o valor de um campo que não está definido para um tipo de descritor específico, a função retornará SQL_SUCCESS, mas o valor retornado para o campo será indefinido. Por exemplo, chamar **SQLGetDescRec** para o campo SQL_DESC_NAME ou SQL_DESC_NULLABLE de APD ou descartar retornará SQL_SUCCESS, mas um valor indefinido para o campo.  
  
 Quando um aplicativo chama **SQLGetDescRec** para recuperar o valor de um campo que é definido para um tipo de descritor específico, mas que não tem valor padrão e ainda não foi definida, a função retornará SQL_SUCCESS, mas o valor retornado para o campo será indefinido. Para obter mais informações, consulte "Inicialização de campos de descritor" [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).  
  
 Os valores dos campos também podem ser recuperados individualmente por uma chamada para **SQLGetDescField**. Para obter uma descrição dos campos em um cabeçalho do descritor ou registro, consulte [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md). Para obter mais informações sobre descritores, consulte [descritores](../../../odbc/reference/develop-app/descriptors.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Associação de uma coluna|[Função SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Um parâmetro de associação|[Função SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|Obter um campo de descritor|[Função SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|Definindo vários campos de descritor|[Função SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
