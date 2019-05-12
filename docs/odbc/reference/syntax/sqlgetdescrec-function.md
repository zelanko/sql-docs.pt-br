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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c737a9dfd6e7a33b5e160b3d952fac0b354148b4
ms.sourcegitcommit: 7a3243c45830cb3f49a7fa71c2991a9454fd6f5a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/11/2019
ms.locfileid: "65538198"
---
# <a name="sqlgetdescrec-function"></a>Função SQLGetDescRec
**Conformidade com**  
 Versão introduzida: Conformidade com padrões 3.0 ODBC: ISO 92  
  
 **Resumo**  
 **SQLGetDescRec** retorna as configurações atuais ou valores de vários campos de um registro de descritor. Os campos retornados descrevem o nome, tipo de dados e armazenamento de dados de coluna ou parâmetro.  
  
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
 [Entrada] Identificador do descritor.  
  
 *RecNumber*  
 [Entrada] Indica que o registro do descritor do qual o aplicativo busca informações. Registros de descritor são numerados de 1, com o número de registro que está sendo o registro de indicador de 0. O *RecNumber* argumento deve ser menor ou igual ao valor de SQL_DESC_COUNT. Se *RecNumber* é menor ou igual a SQL_DESC_COUNT, mas a linha não contém dados para uma coluna ou parâmetro, uma chamada para **SQLGetDescRec** retornará os valores padrão dos campos. (Para obter mais informações, consulte "Inicialização de campos de descritor" na [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).)  
  
 *Nome*  
 [Saída] Um ponteiro para um buffer no qual retornar o campo SQL_DESC_NAME para o registro do descritor.  
  
 Se *nome* for NULL, *StringLengthPtr* ainda retornará o número total de caracteres (exceto o caractere nulo de terminação para dados de caracteres) disponíveis para retornar no buffer apontado por  *Nome*.  
  
 *BufferLength*  
 [Entrada] Comprimento do **nome* buffer em caracteres.  
  
 *StringLengthPtr*  
 [Saída] Um ponteiro para um buffer no qual retornar o número de caracteres de dados disponíveis para retornar os \* *nome* buffer, exceto o caractere nulo de terminação. Se o número de caracteres era maior que ou igual a *BufferLength*, os dados no \* *nome* será truncado com *BufferLength* menos o comprimento de um caractere de terminação NULL e é terminada em nulo pelo driver.  
  
 *TypePtr*  
 [Saída] Um ponteiro para um buffer no qual retornar o valor do campo SQL_DESC_TYPE para o registro do descritor.  
  
 *SubTypePtr*  
 [Saída] Para os registros cujo tipo for SQL_DATETIME ou SQL_INTERVAL, esse é um ponteiro para um buffer no qual retornar o valor do campo SQL_DESC_DATETIME_INTERVAL_CODE.  
  
 *LengthPtr*  
 [Saída] Um ponteiro para um buffer no qual retornar o valor do campo SQL_DESC_OCTET_LENGTH para o registro do descritor.  
  
 *PrecisionPtr*  
 [Saída] Um ponteiro para um buffer no qual retornar o valor do campo SQL_DESC_PRECISION para o registro do descritor.  
  
 *ScalePtr*  
 [Saída] Um ponteiro para um buffer no qual retornar o valor do campo SQL_DESC_SCALE para o registro do descritor.  
  
 *NullablePtr*  
 [Saída] Um ponteiro para um buffer no qual retornar o valor do campo SQL_DESC_NULLABLE para o registro do descritor.  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_NO_DATA ou SQL_INVALID_HANDLE.  
  
 SQL_NO_DATA seja retornado se *RecNumber* é maior que o número atual de registros de descritor.  
  
 SQL_NO_DATA seja retornado se *DescriptorHandle* é um identificador IRD e a instrução está no estado preparado ou executado, mas não havia nenhum cursor aberto associado a ele.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLGetDescRec** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtida chamando **SQLGetDiagRec** com um *HandleType* de SQL _ HANDLE_DESC e uma *manipular* dos *DescriptorHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLGetDescRec** e explica cada uma no contexto dessa função; a notação "(DM)" precede as descrições das SQLSTATEs retornados pelo Gerenciador de Driver. O código de retorno associado com cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa de específicos do driver. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|01004|Dados de cadeia de caracteres truncados à direita|O buffer \* *nome* não era grande o suficiente para retornar o campo do descritor de inteiro. Portanto, o campo foi truncado. O comprimento do campo de descritor completo será retornado no **StringLengthPtr*. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|07009|Índice de descritor inválido|O *FieldIdentifier* argumento era um campo de registro, o *RecNumber* argumento foi definido como 0 e o *DescriptorHandle* argumento era um identificador IPD.<br /><br /> (DM) a *RecNumber* argumento foi definido como 0, e o atributo da instrução SQL_ATTR_USE_BOOKMARKS foi definido como SQL_UB_OFF e o *DescriptorHandle* argumento era um identificador IRD.<br /><br /> O *RecNumber* argumento era menor que 0.|  
|08S01|Falha de link de comunicação|Falha do link de comunicação entre o driver e a fonte de dados ao qual o driver foi conectado antes do processamento da função foi concluída.|  
|HY000|Erro geral|Ocorreu um erro para o qual não houve nenhum SQLSTATE específico e para o qual não foi definida nenhuma SQLSTATE específicos de implementação. A mensagem de erro retornada por **SQLGetDiagRec** na  *\*MessageText* buffer descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar a memória necessária para dar suporte à execução ou a conclusão da função.|  
|HY007|Instrução associada não está preparada.|*DescriptorHandle* foi associado um IRD, e o identificador de instrução associado não estava no estado preparado ou executado.|  
|HY010|Erro de sequência de função|(DM) *DescriptorHandle* foi associada com um *StatementHandle* para que uma função de execução assíncrona (não esta uma) foi chamada e ainda estava em execução quando essa função foi chamada.<br /><br /> (DM) *DescriptorHandle* foi associada com um *StatementHandle* para o qual **SQLExecute**, **SQLExecDirect**,  **SQLBulkOperations**, ou **SQLSetPos** foi chamado e retornou SQL_NEED_DATA. Essa função foi chamada antes de dados foi enviados para todos os parâmetros de dados em execução ou colunas.<br /><br /> (DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado a *DescriptorHandle*. Essa função assíncrona ainda estava em execução quando **SQLGetDescRec** foi chamado.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacente não pôde ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY117|Conexão está suspenso devido ao estado de transação desconhecida. Somente se desconectar e funções de somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tempo limite da Conexão expirado|O período de tempo limite de conexão expirado antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não oferece suporte a essa função|O driver em (DM) associados *DescriptorHandle* não suporta a função.|  
  
## <a name="comments"></a>Comentários  
 Um aplicativo pode chamar **SQLGetDescRec** para recuperar os valores dos seguintes campos de descritor para uma única coluna ou parâmetro:  
  
-   SQL_DESC_NAME  
  
-   SQL_DESC_TYPE  
  
-   SQL_DESC_DATETIME_INTERVAL_CODE (para registros cujo tipo for SQL_DATETIME ou SQL_INTERVAL)  
  
-   SQL_DESC_OCTET_LENGTH  
  
-   SQL_DESC_PRECISION  
  
-   SQL_DESC_SCALE  
  
-   SQL_DESC_NULLABLE  
  
 **SQLGetDescRec** não recuperar os valores para os campos de cabeçalho.  
  
 Um aplicativo pode evitar o retorno de configuração de um campo, definindo o argumento que corresponde ao campo como um ponteiro nulo.  
  
 Quando um aplicativo chama **SQLGetDescRec** para recuperar o valor de um campo que não está definido para um tipo de descritor específico, a função retornará SQL_SUCCESS, mas o valor retornado para o campo será indefinido. Por exemplo, chamar **SQLGetDescRec** para o campo SQL_DESC_NAME ou SQL_DESC_NULLABLE de um APD ou descartar retornará SQL_SUCCESS, mas um valor indefinido para o campo.  
  
 Quando um aplicativo chama **SQLGetDescRec** para recuperar o valor de um campo que é definido para um tipo de descritor específico, mas que não tem valor padrão e ainda não foi definida, a função retornará SQL_SUCCESS, mas o valor retornado para o campo será indefinido. Para obter mais informações, consulte "Inicialização de campos de descritor" na [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).  
  
 Os valores dos campos também podem ser recuperados individualmente por uma chamada para **SQLGetDescField**. Para obter uma descrição dos campos em um cabeçalho do descritor ou registro, consulte [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md). Para obter mais informações sobre descritores, consulte [descritores](../../../odbc/reference/develop-app/descriptors.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Uma coluna de associação|[Função SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Um parâmetro de associação|[Função SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|Obter um campo de descritor|[Função SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|Configurando vários campos de descritor|[Função SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
