---
title: Função SQLGetDescField | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetDescField
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetDescField
helpviewer_keywords:
- SQLGetDescField function [ODBC]
ms.assetid: f09ff660-1e4a-4370-be85-90d4da0487d3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 89972d7f36b436868cc8e243b03827f095b90492
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81285470"
---
# <a name="sqlgetdescfield-function"></a>Função SQLGetDescField
**Conformidade**  
 Versão introduzida: conformidade de padrões do ODBC 3,0: ISO 92  
  
 **Resumo**  
 **SQLGetDescField** retorna a configuração ou o valor atual de um único campo de um registro de descritor.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLGetDescField(  
     SQLHDESC        DescriptorHandle,  
     SQLSMALLINT     RecNumber,  
     SQLSMALLINT     FieldIdentifier,  
     SQLPOINTER      ValuePtr,  
     SQLINTEGER      BufferLength,  
     SQLINTEGER *    StringLengthPtr);  
```  
  
## <a name="arguments"></a>Argumentos  
 *DescriptorHandle*  
 Entrada Identificador do descritor.  
  
 *RecNumber*  
 Entrada Indica o registro do descritor do qual o aplicativo busca informações. Os registros de descritores são numerados de 0, com o número de registro 0 sendo o registro de indicador. Se o argumento *FieldIdentifier* indicar um campo de cabeçalho, *RecNumber* será ignorado. Se *RecNumber* for menor ou igual a SQL_DESC_COUNT, mas a linha não contiver dados para uma coluna ou parâmetro, uma chamada para **SQLGetDescField** retornará os valores padrão dos campos. (Para obter mais informações, consulte "inicialização de campos de descritor" em [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).)  
  
 *FieldIdentifier*  
 Entrada Indica o campo do descritor cujo valor deve ser retornado. Para obter mais informações, consulte a seção "argumento*FieldIdentifier* " em [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).  
  
 *ValuePtr*  
 Der Ponteiro para um buffer no qual as informações do descritor são retornadas. O tipo de dados depende do valor de *FieldIdentifier*.  
  
 Se *ValuePtr* for um tipo inteiro, os aplicativos deverão usar um buffer de SQLULEN e inicializar o valor para 0 antes de chamar essa função, já que alguns drivers só podem gravar os mais baixos 32 bits ou 16 bits de um buffer e deixar o bit de ordem superior inalterado.  
  
 Se *ValuePtr* for NULL, *StringLengthPtr* ainda retornará o número total de bytes (excluindo o caractere de terminação nula para dados de caracteres) disponíveis para retornar no buffer apontado por *ValuePtr*.  
  
 *BufferLength*  
 Entrada Se *FieldIdentifier* for um campo definido pelo ODBC e *ValuePtr* apontar para uma cadeia de caracteres ou um buffer binário, esse argumento deverá ter o comprimento \*de *ValuePtr*. Se *FieldIdentifier* for um campo definido pelo ODBC e \* *ValuePtr* for um inteiro, *BufferLength* será ignorado. Se o valor em * \*ValuePtr* for de um tipo de dados Unicode (ao chamar **SQLGetDescFieldW**), o argumento *BufferLength* deverá ser um número par.  
  
 Se *FieldIdentifier* for um campo definido pelo driver, o aplicativo indicará a natureza do campo para o Gerenciador de driver, definindo o argumento *BufferLength* . *BufferLength* pode ter os seguintes valores:  
  
-   Se * \*ValuePtr* for um ponteiro para uma cadeia de caracteres, *BufferLength* será o comprimento da cadeia de caracteres ou SQL_NTS.  
  
-   Se * \*ValuePtr* for um ponteiro para um buffer binário, o aplicativo colocará o resultado da macro SQL_LEN_BINARY_ATTR (*Length*) em *BufferLength*. Isso coloca um valor negativo em *BufferLength*.  
  
-   Se * \*ValuePtr* for um ponteiro para um valor diferente de uma cadeia de caracteres ou uma cadeia de caracteres binária, *BufferLength* deverá ter o valor SQL_IS_POINTER.  
  
-   Se * \*ValuePtr* contiver um tipo de dados de comprimento fixo, o *BufferLength* será SQL_IS_INTEGER, SQL_IS_UINTEGER, SQL_IS_SMALLINT ou SQL_IS_USMALLINT, conforme apropriado.  
  
 *StringLengthPtr*  
 Der Ponteiro para o buffer no qual retornar o número total de bytes (exceto o número de bytes necessários para o caractere de terminação nula) disponível para retornar em **ValuePtr*.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_NO_DATA ou SQL_INVALID_HANDLE.  
  
 SQL_NO_DATA será retornado se *RecNumber* for maior que o número atual de registros de descritor.  
  
 SQL_NO_DATA será retornado se *DescriptorHandle* for um identificador de IRD e a instrução estiver no estado preparado ou executado, mas não houver nenhum cursor aberto associado a ele.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLGetDescField** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido chamando **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_STMT e um *identificador* de *StatementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLGetDescField** e explica cada um no contexto dessa função; a notação "(DM)" precede as descrições de sqlstates retornadas pelo Gerenciador de driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa específica do driver. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|01004|Dados de cadeia de caracteres, truncados à direita|O buffer \* *ValuePtr* não era grande o suficiente para retornar o campo do descritor inteiro, portanto, o campo foi truncado. O comprimento do campo de descritor não truncado é retornado em **StringLengthPtr*. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|07009|Índice de descritor inválido|(DM) o argumento *RecNumber* era igual a 0, o atributo de instrução SQL_ATTR_USE_BOOKMARK foi SQL_UB_OFF e o argumento *DescriptorHandle* era um identificador IRD. (Esse erro pode ser retornado para um descritor explicitamente alocado somente se o descritor estiver associado a um identificador de instrução.)<br /><br /> O argumento *FieldIdentifier* era um campo de registro, o argumento *RecNumber* era 0 e o argumento *DESCRIPTORHANDLE* era um identificador de IPD.<br /><br /> O argumento *RecNumber* era menor que 0.|  
|08S01|Falha no link de comunicação|O link de comunicação entre o driver e a fonte de dados ao qual o driver foi conectado falhou antes da função concluir o processamento.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia um SQLSTATE específico e para o qual nenhum SQLSTATE específico de implementação foi definido. A mensagem de erro retornada por **SQLGetDiagRec** no buffer * \*MessageText* descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar a memória necessária para dar suporte à execução ou à conclusão da função.|  
|HY007|A instrução associada não está preparada|*DescriptorHandle* foi associado a um *STATEMENTHANDLE* como um IRD, e o identificador de instrução associado não foi preparado ou executado.|  
|HY010|Erro de sequência de função|(DM) *DescriptorHandle* foi associado a um *StatementHandle* para o qual uma função de execução assíncrona (não esta) foi chamada e ainda estava em execução quando essa função foi chamada.<br /><br /> (DM) *DescriptorHandle* foi associado a um *StatementHandle* para o qual **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**ou **SQLSetPos** foi chamado e retornou SQL_NEED_DATA. Esta função foi chamada antes de os dados serem enviados para todos os parâmetros de dados em execução ou colunas.<br /><br /> (DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado ao *DescriptorHandle*. Esta função assíncrona ainda estava em execução quando a função **SQLGetDescField** foi chamada.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não puderam ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY021|Informações de descritor inconsistentes|Os campos SQL_DESC_TYPE e SQL_DESC_DATETIME_INTERVAL_CODE não formam um tipo SQL ODBC válido, um tipo de SQL específico de driver válido (para IPDs) ou um tipo ODBC C válido (para APDs ou ARDs).|  
|HY090|Comprimento de cadeia de caracteres ou buffer inválido|(DM) * \*ValuePtr* era uma cadeia de caracteres e *BufferLength* era menor que zero.|  
|HY091|Identificador de campo de descritor inválido|*FieldIdentifier* não era um campo definido pelo ODBC e não era um valor definido pela implementação.<br /><br /> *FieldIdentifier* foi indefinido para o *DescriptorHandle*.|  
|HY117|A conexão foi suspensa devido a um estado de transação desconhecido. Somente funções de desconexão e somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tempo limite de conexão expirado|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|O driver não oferece suporte a essa função|(DM) o driver associado ao *DescriptorHandle* não oferece suporte à função.|  
  
## <a name="comments"></a>Comentários  
 Um aplicativo pode chamar **SQLGetDescField** para retornar o valor de um único campo de um registro de descritor. Uma chamada para **SQLGetDescField** pode retornar a configuração de qualquer campo em qualquer tipo de descritor, incluindo campos de cabeçalho, campos de registro e campos de indicador. Um aplicativo pode obter as configurações de vários campos nos mesmos ou descritores diferentes, em ordem arbitrária, fazendo chamadas repetidas para **SQLGetDescField**. **SQLGetDescField** também pode ser chamado para retornar campos de descritor definidos pelo driver.  
  
 Por motivos de desempenho, um aplicativo não deve chamar **SQLGetDescField** para um IRD antes de executar uma instrução.  
  
 As configurações de vários campos que descrevem o nome, o tipo de dados e o armazenamento de colunas ou dados de parâmetros também podem ser recuperadas em uma única chamada para **SQLGetDescRec**. **SQLGetStmtAttr** pode ser chamado para retornar a configuração de um único campo no cabeçalho do descritor que também é um atributo de instrução. **SQLColAttribute**, **SQLDescribeCol**e **SQLDescribeParam** retornam campos de registro ou de indicador.  
  
 Quando um aplicativo chama **SQLGetDescField** para recuperar o valor de um campo que é indefinido para um determinado tipo de descritor, a função retorna SQL_SUCCESS, mas o valor retornado para o campo é indefinido. Por exemplo, chamar **SQLGetDescField** para o campo SQL_DESC_NAME ou SQL_DESC_NULLABLE de um APD ou ARD retornará SQL_SUCCESS, mas um valor indefinido para o campo.  
  
 Quando um aplicativo chama **SQLGetDescField** para recuperar o valor de um campo que é definido para um determinado tipo de descritor, mas que não tem valor padrão e ainda não foi definido, a função retorna SQL_SUCCESS, mas o valor retornado para o campo é indefinido. Para obter mais informações sobre a inicialização de campos de descritor e descrições dos campos, consulte "inicialização de campos de descritor" em [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md). Para obter mais informações sobre descritores, consulte [descritores](../../../odbc/reference/develop-app/descriptors.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Obtendo vários campos de descritor|[Função SQLGetDescRec](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|Configurando um único campo de descritor|[Função SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|Configurando vários campos de descritor|[Função SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
