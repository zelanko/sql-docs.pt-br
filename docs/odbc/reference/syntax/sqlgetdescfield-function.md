---
title: Função SQLGetDescField | Microsoft Docs
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
- SQLGetDescField
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetDescField
helpviewer_keywords:
- SQLGetDescField function [ODBC]
ms.assetid: f09ff660-1e4a-4370-be85-90d4da0487d3
caps.latest.revision: 21
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 900d85e7aa8e2ff100df7ba223929671903b3d90
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32922131"
---
# <a name="sqlgetdescfield-function"></a>Função SQLGetDescField
**Conformidade**  
 Versão introduzidas: Conformidade de padrões 3.0 ODBC: 92 ISO  
  
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
 [Entrada] Indica que o registro do descritor do qual o aplicativo busca de informações. Registros de descritor são numerados de 0, com o número de registro sendo o registro do indicador de 0. Se o *FieldIdentifier* argumento indica um campo de cabeçalho, *RecNumber* será ignorado. Se *RecNumber* é menor ou igual a SQL_DESC_COUNT, mas a linha não contém dados de uma coluna ou parâmetro, uma chamada para **SQLGetDescField** retornará os valores padrão dos campos. (Para obter mais informações, consulte "Inicialização de campos de descritor" [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).)  
  
 *FieldIdentifier*  
 [Entrada] Indica o campo do descritor cujo valor será retornado. Para obter mais informações, consulte o "*FieldIdentifier* argumento" seção [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).  
  
 *ValuePtr*  
 [Saída] Ponteiro para um buffer no qual retornar as informações do descritor. O tipo de dados depende do valor de *FieldIdentifier*.  
  
 Se *ValuePtr* é do tipo inteiro, os aplicativos devem usar um buffer de SQLULEN e inicializar o valor para 0 antes de chamar essa função como alguns drivers somente pode gravar o inferior 32 bits ou 16 bits de um buffer e deixe o bit de ordem superior inalterado.  
  
 Se *ValuePtr* for NULL, *StringLengthPtr* ainda retornará o número total de bytes (excluindo o caractere null de terminação para dados de caractere) disponíveis para retornar o buffer apontado pelo  *ValuePtr*.  
  
 *BufferLength*  
 [Entrada] Se *FieldIdentifier* é um campo definido pelo ODBC e *ValuePtr* aponta para uma cadeia de caracteres ou um buffer binário, este argumento deve ser o comprimento de \* *ValuePtr*. Se *FieldIdentifier* é um campo definido pelo ODBC e \* *ValuePtr* é um inteiro, *BufferLength* será ignorado. Se o valor em  *\*ValuePtr* é de um tipo de dados Unicode (ao chamar **SQLGetDescFieldW**), o *BufferLength* argumento deve ser um número par.  
  
 Se *FieldIdentifier* é um campo definido pelo driver, o aplicativo indica a natureza do campo para o Gerenciador de Driver, definindo o *BufferLength* argumento. *BufferLength* pode ter os seguintes valores:  
  
-   Se  *\*ValuePtr* é um ponteiro para uma cadeia de caracteres, em seguida, *BufferLength* é o comprimento da cadeia de caracteres ou SQL_NTS.  
  
-   Se  *\*ValuePtr* é um ponteiro para um buffer de binário, em seguida, o aplicativo coloca o resultado da SQL_LEN_BINARY_ATTR (*comprimento*) macro em *BufferLength*. Isso coloca um valor negativo em *BufferLength*.  
  
-   Se  *\*ValuePtr* é um ponteiro para um valor diferente de uma cadeia de caracteres ou cadeia de caracteres binária, em seguida, *BufferLength* devem ter o valor SQL_IS_POINTER.  
  
-   Se  *\*ValuePtr* é contém um tipo de dados de comprimento fixo, em seguida, *BufferLength* é SQL_IS_INTEGER, SQL_IS_UINTEGER, SQL_IS_SMALLINT ou SQL_IS_USMALLINT, conforme apropriado.  
  
 *StringLengthPtr*  
 [Saída] Ponteiro para o buffer no qual retornar o número total de bytes (excluindo o número de bytes necessários para o caractere null de terminação) disponíveis para retornar em **ValuePtr*.  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_NO_DATA ou SQL_INVALID_HANDLE.  
  
 SQL_NO_DATA seja retornado se *RecNumber* é maior que o número atual de registros de descritor.  
  
 SQL_NO_DATA seja retornado se *DescriptorHandle* é um identificador IRD e a instrução está no estado preparado ou executado, mas não havia nenhum cursor aberto associado a ele.  
  
## <a name="diagnostics"></a>diagnóstico  
 Quando **SQLGetDescField** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtida chamando **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_STMT e um *tratar* de *StatementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLGetDescField** e explica cada uma no contexto dessa função; a notação "(DM)" precede as descrições de SQLSTATEs retornados pelo Gerenciador de Driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado em contrário.  
  
|SQLSTATE|Erro|Description|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem de informação específica do driver. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|01004|Dados de cadeia de caracteres truncados à direita|O buffer \* *ValuePtr* não era grande o suficiente para retornar o campo do descritor inteira, para que o campo foi truncado. O comprimento do campo de descritor completo é retornado em **StringLengthPtr*. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|07009|Índice do descritor inválido|(DM) a *RecNumber* argumento era igual a 0, o atributo da instrução SQL_ATTR_USE_BOOKMARK foi SQL_UB_OFF e o *DescriptorHandle* argumento era um identificador de IRD. (Esse erro pode ser retornado para um descritor alocado explicitamente somente se o descritor está associado um identificador de instrução.)<br /><br /> O *FieldIdentifier* argumento era um campo de registro, o *RecNumber* argumento era 0 e o *DescriptorHandle* argumento era um identificador de IPD.<br /><br /> O *RecNumber* argumento era menor do que 0.|  
|08S01|Falha de link de comunicação|Falha do link de comunicação entre o driver e a fonte de dados ao qual o driver foi conectado antes do processamento da função foi concluída.|  
|HY000|Erro geral|Ocorreu um erro para o qual não houve nenhuma SQLSTATE específico e para o qual nenhuma SQLSTATE específicos de implementação foi definida. A mensagem de erro retornada pelo **SQLGetDiagRec** no  *\*MessageText* buffer descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar a memória necessária para dar suporte a execução ou a conclusão da função.|  
|HY007|Instrução associada não está preparada|*DescriptorHandle* foi associado um *StatementHandle* como um IRD e a instrução associada identificador tinha não foi preparado ou executado.|  
|HY010|Erro de sequência de função|(DM) *DescriptorHandle* foi associado um *StatementHandle* para que uma função de execução assíncrona (não esse um) foi chamada e ainda estava em execução quando esta função foi chamada.<br /><br /> (DM) *DescriptorHandle* foi associado um *StatementHandle* para o qual **SQLExecute**, **SQLExecDirect**,  **SQLBulkOperations**, ou **SQLSetPos** foi chamado e retornou SQL_NEED_DATA. Essa função foi chamada antes de dados foi enviados para todas as colunas ou parâmetros de dados em execução.<br /><br /> (DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado a *DescriptorHandle*. Essa função assíncrona ainda estava em execução quando o **SQLGetDescField** função foi chamada.|  
|HY013|Erro de gerenciamento de memória|Não foi possível processar a chamada de função porque os objetos de memória subjacente não podem ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY021|Informações do descritor inconsistentes|Os campos SQL_DESC_TYPE e SQL_DESC_DATETIME_INTERVAL_CODE não formam um tipo válido do ODBC SQL, um tipo SQL específicos de driver válido (para IPDs) ou um tipo válido do ODBC C (para APDs ou ARDs).|  
|HY090|Comprimento de buffer ou cadeia de caracteres inválido|(DM)  *\*ValuePtr* era uma cadeia de caracteres, e *BufferLength* foi menor que zero.|  
|HY091|Identificador de campo de descritor inválido|*FieldIdentifier* não um campo definido pelo ODBC e não era um valor definido pela implementação.<br /><br /> *FieldIdentifier* foi indefinido para o *DescriptorHandle*.|  
|HY117|Conexão está suspenso devido ao estado de transação desconhecido. Somente Desconecte e funções de somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tempo limite de Conexão expirou|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não dá suporte a esta função|O driver em (DM) associado a *DescriptorHandle* não oferece suporte para a função.|  
  
## <a name="comments"></a>Comentários  
 Um aplicativo pode chamar **SQLGetDescField** para retornar o valor de um único campo de um registro do descritor. Uma chamada para **SQLGetDescField** pode retornar a configuração de qualquer campo em qualquer tipo de descritor, inclusive campos de cabeçalho, campos de registros e campos de indicador. Um aplicativo pode obter as configurações de vários campos nos descritores igual ou diferentes, em uma ordem arbitrária, fazendo chamadas repetidas para **SQLGetDescField**. **SQLGetDescField** também pode ser chamado para retornar campos de descritor definidos pelo driver.  
  
 Por motivos de desempenho, um aplicativo não deve chamar **SQLGetDescField** para um IRD antes de executar uma instrução.  
  
 As configurações de vários campos que descrevem o nome, tipo de dados e armazenamento de dados de coluna ou parâmetro também podem ser recuperadas em uma única chamada para **SQLGetDescRec**. **SQLGetStmtAttr** pode ser chamado para retornar a configuração de um único campo no cabeçalho do descritor que também é um atributo de instrução. **SQLColAttribute**, **SQLDescribeCol**, e **SQLDescribeParam** retornar campos de registro ou indicador.  
  
 Quando um aplicativo chama **SQLGetDescField** para recuperar o valor de um campo que não está definido para um tipo de descritor específico, a função retornará SQL_SUCCESS, mas o valor retornado para o campo será indefinido. Por exemplo, chamar **SQLGetDescField** para o campo SQL_DESC_NAME ou SQL_DESC_NULLABLE de APD ou descartar retornará SQL_SUCCESS, mas um valor indefinido para o campo.  
  
 Quando um aplicativo chama **SQLGetDescField** para recuperar o valor de um campo que é definido para um tipo de descritor específico, mas que não tem valor padrão e ainda não foi definida, a função retornará SQL_SUCCESS, mas o valor retornado para o campo será indefinido. Para obter mais informações sobre a inicialização de campos de descritor e descrições dos campos, consulte "Inicialização de campos de descritor" [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md). Para obter mais informações sobre os descritores, consulte [descritores](../../../odbc/reference/develop-app/descriptors.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Obtendo vários campos de descritor|[Função SQLGetDescRec](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|Configuração de um campo de descritor único|[Função SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|Definindo vários campos de descritor|[Função SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Referência de API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
