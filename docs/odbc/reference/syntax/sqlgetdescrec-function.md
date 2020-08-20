---
description: Função SQLGetDescRec
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
ms.openlocfilehash: 5237d8b1a1d070752219abd22936615060371a89
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461046"
---
# <a name="sqlgetdescrec-function"></a>Função SQLGetDescRec
**Conformidade**  
 Versão introduzida: conformidade de padrões do ODBC 3,0: ISO 92  
  
 **Resumo**  
 **SQLGetDescRec** retorna as configurações ou valores atuais de vários campos de um registro de descritor. Os campos retornados descrevem o nome, o tipo de dados e o armazenamento dos dados da coluna ou do parâmetro.  
  
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
 Entrada Identificador do descritor.  
  
 *RecNumber*  
 Entrada Indica o registro do descritor do qual o aplicativo busca informações. Os registros de descritores são numerados de 1, com o número de registro 0 sendo o registro de indicador. O argumento *RecNumber* deve ser menor ou igual ao valor de SQL_DESC_COUNT. Se *RecNumber* for menor ou igual a SQL_DESC_COUNT, mas a linha não contiver dados para uma coluna ou parâmetro, uma chamada para **SQLGetDescRec** retornará os valores padrão dos campos. (Para obter mais informações, consulte "inicialização de campos de descritor" em [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).)  
  
 *Nome*  
 Der Um ponteiro para um buffer no qual retornar o campo de SQL_DESC_NAME para o registro de descritor.  
  
 Se *Name* for NULL, *StringLengthPtr* ainda retornará o número total de caracteres (excluindo o caractere de terminação nula para dados de caracteres) disponíveis para retornar no buffer apontado pelo *nome*.  
  
 *BufferLength*  
 Entrada Comprimento do * buffer de*nome* , em caracteres.  
  
 *StringLengthPtr*  
 Der Um ponteiro para um buffer no qual retornar o número de caracteres de dados disponíveis para retornar no buffer de \* *nome* , excluindo o caractere de terminação nula. Se o número de caracteres for maior ou igual a *BufferLength*, os dados em \* *nome* serão truncados para *BufferLength* menos o comprimento de um caractere de terminação de nulo e serão terminados em nulo pelo driver.  
  
 *TypePtr*  
 Der Um ponteiro para um buffer no qual retornar o valor do campo SQL_DESC_TYPE para o registro do descritor.  
  
 *SubTypePtr*  
 Der Para registros cujo tipo é SQL_DATETIME ou SQL_INTERVAL, esse é um ponteiro para um buffer no qual retornar o valor do campo SQL_DESC_DATETIME_INTERVAL_CODE.  
  
 *LengthPtr*  
 Der Um ponteiro para um buffer no qual retornar o valor do campo SQL_DESC_OCTET_LENGTH para o registro do descritor.  
  
 *PrecisionPtr*  
 Der Um ponteiro para um buffer no qual retornar o valor do campo SQL_DESC_PRECISION para o registro do descritor.  
  
 *ScalePtr*  
 Der Um ponteiro para um buffer no qual retornar o valor do campo SQL_DESC_SCALE para o registro do descritor.  
  
 *NullablePtr*  
 Der Um ponteiro para um buffer no qual retornar o valor do campo SQL_DESC_NULLABLE para o registro do descritor.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_NO_DATA ou SQL_INVALID_HANDLE.  
  
 SQL_NO_DATA será retornado se *RecNumber* for maior que o número atual de registros de descritor.  
  
 SQL_NO_DATA será retornado se *DescriptorHandle* for um identificador de IRD e a instrução estiver no estado preparado ou executado, mas não houver nenhum cursor aberto associado a ele.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **SQLGetDescRec** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido chamando **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_DESC e um *identificador* de *DescriptorHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLGetDescRec** e explica cada um no contexto dessa função; a notação "(DM)" precede as descrições de sqlstates retornadas pelo Gerenciador de driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa específica do driver. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|01004|Dados de cadeia de caracteres, truncados à direita|O \* *nome* do buffer não era grande o suficiente para retornar o campo do descritor inteiro. Portanto, o campo foi truncado. O comprimento do campo de descritor não truncado é retornado em **StringLengthPtr*. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|07009|Índice de descritor inválido|O argumento *FieldIdentifier* era um campo de registro, o argumento *RecNumber* foi definido como 0 e o argumento *DESCRIPTORHANDLE* era um identificador de IPD.<br /><br /> (DM) o argumento *RecNumber* foi definido como 0 e o atributo de instrução SQL_ATTR_USE_BOOKMARKS foi definido como SQL_UB_OFF, e o argumento *DescriptorHandle* era um identificador IRD.<br /><br /> O argumento *RecNumber* era menor que 0.|  
|08S01|Falha no link de comunicação|O link de comunicação entre o driver e a fonte de dados ao qual o driver foi conectado falhou antes da função concluir o processamento.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia um SQLSTATE específico e para o qual nenhum SQLSTATE específico de implementação foi definido. A mensagem de erro retornada por **SQLGetDiagRec** no buffer * \* MessageText* descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar a memória necessária para dar suporte à execução ou à conclusão da função.|  
|HY007|A instrução associada não está preparada|*DescriptorHandle* foi associado a um IRD, e o identificador de instrução associado não estava no estado preparado ou executado.|  
|HY010|Erro de sequência de função|(DM) *DescriptorHandle* foi associado a um *StatementHandle* para o qual uma função de execução assíncrona (não esta) foi chamada e ainda estava em execução quando essa função foi chamada.<br /><br /> (DM) *DescriptorHandle* foi associado a um *StatementHandle* para o qual **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**ou **SQLSetPos** foi chamado e retornou SQL_NEED_DATA. Esta função foi chamada antes de os dados serem enviados para todos os parâmetros de dados em execução ou colunas.<br /><br /> (DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado ao *DescriptorHandle*. Esta função assíncrona ainda estava em execução quando **SQLGetDescRec** foi chamado.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não puderam ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY117|A conexão foi suspensa devido a um estado de transação desconhecido. Somente funções de desconexão e somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tempo limite de conexão expirado|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|O driver não oferece suporte a essa função|(DM) o driver associado a *DescriptorHandle* não oferece suporte à função.|  
  
## <a name="comments"></a>Comentários  
 Um aplicativo pode chamar **SQLGetDescRec** para recuperar os valores dos seguintes campos de descritor para uma única coluna ou parâmetro:  
  
-   SQL_DESC_NAME  
  
-   SQL_DESC_TYPE  
  
-   SQL_DESC_DATETIME_INTERVAL_CODE (para registros cujo tipo é SQL_DATETIME ou SQL_INTERVAL)  
  
-   SQL_DESC_OCTET_LENGTH  
  
-   SQL_DESC_PRECISION  
  
-   SQL_DESC_SCALE  
  
-   SQL_DESC_NULLABLE  
  
 **SQLGetDescRec** não recupera os valores dos campos de cabeçalho.  
  
 Um aplicativo pode impedir o retorno da configuração de um campo definindo o argumento que corresponde ao campo para um ponteiro nulo.  
  
 Quando um aplicativo chama **SQLGetDescRec** para recuperar o valor de um campo que é indefinido para um determinado tipo de descritor, a função retorna SQL_SUCCESS, mas o valor retornado para o campo é indefinido. Por exemplo, chamar **SQLGetDescRec** para o campo SQL_DESC_NAME ou SQL_DESC_NULLABLE de um APD ou ARD retornará SQL_SUCCESS, mas um valor indefinido para o campo.  
  
 Quando um aplicativo chama **SQLGetDescRec** para recuperar o valor de um campo que é definido para um determinado tipo de descritor, mas que não tem valor padrão e ainda não foi definido, a função retorna SQL_SUCCESS, mas o valor retornado para o campo é indefinido. Para obter mais informações, consulte "inicialização de campos de descritor" em [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).  
  
 Os valores dos campos também podem ser recuperados individualmente por uma chamada para **SQLGetDescField**. Para obter uma descrição dos campos em um cabeçalho ou registro de descritor, consulte [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md). Para obter mais informações sobre descritores, consulte [descritores](../../../odbc/reference/develop-app/descriptors.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Associando uma coluna|[Função SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Associando um parâmetro|[Função SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|Obtendo um campo de descritor|[Função SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|Configurando vários campos de descritor|[Função SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
