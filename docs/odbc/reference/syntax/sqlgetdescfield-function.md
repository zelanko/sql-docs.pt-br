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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f6762eb4ea9b350a76fc794fa7074af2a107b511
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63258933"
---
# <a name="sqlgetdescfield-function"></a>Função SQLGetDescField
**Conformidade com**  
 Versão introduzida: Conformidade com padrões 3.0 ODBC: ISO 92  
  
 **Resumo**  
 **SQLGetDescField** retorna a configuração atual ou o valor de um único campo de um registro do descritor.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
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
 [Entrada] Identificador do descritor.  
  
 *RecNumber*  
 [Entrada] Indica que o registro do descritor do qual o aplicativo busca informações. Registros de descritor são numerados de 0, com o número de registro que está sendo o registro de indicador de 0. Se o *FieldIdentifier* argumento indica um campo de cabeçalho *RecNumber* será ignorado. Se *RecNumber* é menor ou igual a SQL_DESC_COUNT, mas a linha não contém dados para uma coluna ou parâmetro, uma chamada para **SQLGetDescField** retornará os valores padrão dos campos. (Para obter mais informações, consulte "Inicialização de campos de descritor" na [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).)  
  
 *FieldIdentifier*  
 [Entrada] Indica o campo do descritor cujo valor deve ser retornado. Para obter mais informações, consulte o "*FieldIdentifier* argumento" seção [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).  
  
 *ValuePtr*  
 [Saída] Ponteiro para um buffer no qual retornar as informações do descritor. O tipo de dados depende do valor de *FieldIdentifier*.  
  
 Se *ValuePtr* é do tipo inteiro, os aplicativos devem usar um buffer de SQLULEN e inicializar o valor para 0 antes de chamar essa função como alguns drivers pode apenas gravar o inferior 32 bits ou 16 bits de um buffer e deixar o bit de ordem superior inalterado.  
  
 Se *ValuePtr* for NULL, *StringLengthPtr* ainda retornará o número total de bytes (exceto o caractere nulo de terminação para dados de caracteres) disponíveis para retornar no buffer apontado por  *ValuePtr*.  
  
 *BufferLength*  
 [Entrada] Se *FieldIdentifier* é um campo definido pelo ODBC e *ValuePtr* aponta para uma cadeia de caracteres ou um buffer de binário, este argumento deve ser o comprimento da \* *ValuePtr*. Se *FieldIdentifier* é um campo definido pelo ODBC e \* *ValuePtr* é um inteiro, *BufferLength* será ignorado. Se o valor em  *\*ValuePtr* é de um tipo de dados Unicode (ao chamar **SQLGetDescFieldW**), o *BufferLength* argumento deve ser um número par.  
  
 Se *FieldIdentifier* é um campo definido pelo driver, o aplicativo indica a natureza do campo para o Gerenciador de Driver, definindo o *BufferLength* argumento. *BufferLength* pode ter os seguintes valores:  
  
-   Se  *\*ValuePtr* é um ponteiro para uma cadeia de caracteres, em seguida, *BufferLength* é o comprimento da cadeia de caracteres ou SQL_NTS.  
  
-   Se  *\*ValuePtr* é um ponteiro para um buffer de binário, em seguida, o aplicativo coloca o resultado do SQL_LEN_BINARY_ATTR (*comprimento*) macro na *BufferLength*. Isso coloca um valor negativo em *BufferLength*.  
  
-   Se  *\*ValuePtr* é um ponteiro para um valor diferente de uma cadeia de caracteres ou cadeia de caracteres binária, então *BufferLength* deve ter o valor SQL_IS_POINTER.  
  
-   Se  *\*ValuePtr* é contiver um tipo de dados de comprimento fixo, então *BufferLength* é SQL_IS_INTEGER, SQL_IS_UINTEGER, SQL_IS_SMALLINT ou SQL_IS_USMALLINT, conforme apropriado.  
  
 *StringLengthPtr*  
 [Saída] Ponteiro para o buffer no qual retornar o número total de bytes (excluindo o número de bytes necessários para o caractere nulo de terminação) disponíveis para retornar no **ValuePtr*.  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_NO_DATA ou SQL_INVALID_HANDLE.  
  
 SQL_NO_DATA seja retornado se *RecNumber* é maior que o número atual de registros de descritor.  
  
 SQL_NO_DATA seja retornado se *DescriptorHandle* é um identificador IRD e a instrução está no estado preparado ou executado, mas não havia nenhum cursor aberto associado a ele.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLGetDescField** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtida chamando **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_STMT e uma *manipular* dos *StatementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLGetDescField** e explica cada uma no contexto dessa função; a notação "(DM)" precede as descrições das SQLSTATEs retornados pelo Gerenciador de Driver. O código de retorno associado com cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa de específicos do driver. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|01004|Dados de cadeia de caracteres truncados à direita|O buffer \* *ValuePtr* não era grande o suficiente para retornar o campo do descritor de inteiro, portanto, o campo foi truncado. O comprimento do campo de descritor completo será retornado no **StringLengthPtr*. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|07009|Índice de descritor inválido|(DM) a *RecNumber* argumento era igual a 0, o atributo da instrução SQL_ATTR_USE_BOOKMARK era SQL_UB_OFF e o *DescriptorHandle* argumento era um identificador IRD. (Esse erro pode ser retornado para um descritor alocado explicitamente somente se o descritor estiver associado um identificador de instrução.)<br /><br /> O *FieldIdentifier* argumento era um campo de registro, o *RecNumber* argumento era 0 e o *DescriptorHandle* argumento era um identificador IPD.<br /><br /> O *RecNumber* argumento era menor que 0.|  
|08S01|Falha de link de comunicação|Falha do link de comunicação entre o driver e a fonte de dados ao qual o driver foi conectado antes do processamento da função foi concluída.|  
|HY000|Erro geral|Ocorreu um erro para o qual não houve nenhum SQLSTATE específico e para o qual não foi definida nenhuma SQLSTATE específicos de implementação. A mensagem de erro retornada por **SQLGetDiagRec** na  *\*MessageText* buffer descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar a memória necessária para dar suporte à execução ou a conclusão da função.|  
|HY007|Instrução associada não está preparada.|*DescriptorHandle* está associada com um *StatementHandle* como um IRD e a instrução associada identificador tinha não foram preparado ou executado.|  
|HY010|Erro de sequência de função|(DM) *DescriptorHandle* foi associada com um *StatementHandle* para que uma função de execução assíncrona (não esta uma) foi chamada e ainda estava em execução quando essa função foi chamada.<br /><br /> (DM) *DescriptorHandle* foi associada com um *StatementHandle* para o qual **SQLExecute**, **SQLExecDirect**,  **SQLBulkOperations**, ou **SQLSetPos** foi chamado e retornou SQL_NEED_DATA. Essa função foi chamada antes de dados foi enviados para todos os parâmetros de dados em execução ou colunas.<br /><br /> (DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado a *DescriptorHandle*. Essa função assíncrona ainda estava em execução quando o **SQLGetDescField** função foi chamada.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacente não pôde ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY021|Informações do descritor inconsistentes|Os campos SQL_DESC_TYPE e SQL_DESC_DATETIME_INTERVAL_CODE não formam um tipo ODBC SQL válido, um tipo válido de SQL específica do driver (para IPDs) ou um tipo válido do ODBC C (para APDs ou ARDs).|  
|HY090|Comprimento de buffer ou cadeia de caracteres inválido|(DM)  *\*ValuePtr* era uma cadeia de caracteres, e *BufferLength* era menor que zero.|  
|HY091|Identificador de campo de descritor inválido|*FieldIdentifier* não estava em um campo definido pelo ODBC e não um valor definido pela implementação.<br /><br /> *FieldIdentifier* era indefinido para o *DescriptorHandle*.|  
|HY117|Conexão está suspenso devido ao estado de transação desconhecida. Somente se desconectar e funções de somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tempo limite da Conexão expirado|O período de tempo limite de conexão expirado antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não oferece suporte a essa função|O driver em (DM) associado a *DescriptorHandle* não suporta a função.|  
  
## <a name="comments"></a>Comentários  
 Um aplicativo pode chamar **SQLGetDescField** para retornar o valor de um único campo de um registro do descritor. Uma chamada para **SQLGetDescField** pode retornar a configuração de qualquer campo em qualquer tipo de descritor, inclusive campos de cabeçalho, campos de registros e campos de indicador. Um aplicativo pode obter as configurações de vários campos nos descritores iguais ou diferentes, na ordem arbitrária, fazendo repetidas chamadas a **SQLGetDescField**. **SQLGetDescField** também pode ser chamado para retornar campos de descritor definido pelo driver.  
  
 Por motivos de desempenho, um aplicativo não deve chamar **SQLGetDescField** para um IRD antes de executar uma instrução.  
  
 As configurações de vários campos que descrevem o nome, tipo de dados e armazenamento de dados de coluna ou parâmetro também podem ser recuperadas em uma única chamada para **SQLGetDescRec**. **SQLGetStmtAttr** pode ser chamado para retornar à configuração de um único campo no cabeçalho do descritor que também é um atributo de instrução. **SQLColAttribute**, **SQLDescribeCol**, e **SQLDescribeParam** retornar campos de registro ou indicador.  
  
 Quando um aplicativo chama **SQLGetDescField** para recuperar o valor de um campo que não está definido para um tipo de descritor específico, a função retornará SQL_SUCCESS, mas o valor retornado para o campo será indefinido. Por exemplo, chamar **SQLGetDescField** para o campo SQL_DESC_NAME ou SQL_DESC_NULLABLE de um APD ou descartar retornará SQL_SUCCESS, mas um valor indefinido para o campo.  
  
 Quando um aplicativo chama **SQLGetDescField** para recuperar o valor de um campo que é definido para um tipo de descritor específico, mas que não tem valor padrão e ainda não foi definida, a função retornará SQL_SUCCESS, mas o valor retornado para o campo será indefinido. Para obter mais informações sobre a inicialização de campos de descritor e descrições dos campos, consulte "Inicialização de campos de descritor" na [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md). Para obter mais informações sobre descritores, consulte [descritores](../../../odbc/reference/develop-app/descriptors.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Obtendo vários campos de descritor|[Função SQLGetDescRec](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|Definir um campo de descritor único|[Função SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|Configurando vários campos de descritor|[Função SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
