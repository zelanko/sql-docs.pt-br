---
description: Função SQLSetEnvAttr
title: Função SQLSetEnvAttr | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetEnvAttr
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLSetEnvAttr
helpviewer_keywords:
- SQLSetEnvAttr function [ODBC]
ms.assetid: 0343241c-4b15-4d4b-aa2b-2e8ab5215cd2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6f535c860df212c708f11339165b2d05d4a79647
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421110"
---
# <a name="sqlsetenvattr-function"></a>Função SQLSetEnvAttr
**Conformidade**  
 Versão introduzida: conformidade de padrões do ODBC 3,0: ISO 92  
  
 **Resumo**  
 **SQLSetEnvAttr** define atributos que regem aspectos de ambientes.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLSetEnvAttr(  
     SQLHENV      EnvironmentHandle,  
     SQLINTEGER   Attribute,  
     SQLPOINTER   ValuePtr,  
     SQLINTEGER   StringLength);  
```  
  
## <a name="arguments"></a>Argumentos  
 *EnvironmentHandle*  
 Entrada Identificador de ambiente.  
  
 *Atributo*  
 Entrada Atributo a ser definido, listado em "Comentários".  
  
 *ValuePtr*  
 Entrada Ponteiro para o valor a ser associado ao *atributo*. Dependendo do valor do *atributo*, *ValuePtr* será um valor inteiro de 32 bits ou apontará para uma cadeia de caracteres terminada em nulo.  
  
 *StringLength*  
 Entrada Se *ValuePtr* apontar para uma cadeia de caracteres ou um buffer binário, esse argumento deverá ter o comprimento de **ValuePtr*. Para dados de cadeia de caracteres, esse argumento deve conter o número de bytes na cadeia de caracteres.  
  
 Se *ValuePtr* for um inteiro, *StringLength* será ignorado.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **SQLSetEnvAttr** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido chamando **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_ENV e um *identificador* de *EnvironmentHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLSetEnvAttr** e explica cada um no contexto dessa função; a notação "(DM)" precede as descrições de sqlstates retornadas pelo Gerenciador de driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário. Se um driver não oferecer suporte a um atributo de ambiente, o erro poderá ser retornado somente durante o tempo de conexão.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa específica do driver. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|01S02|Valor da opção alterado|O driver não oferecia suporte ao valor especificado em *ValuePtr* e substituiu um valor semelhante. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia um SQLSTATE específico e para o qual nenhum SQLSTATE específico de implementação foi definido. A mensagem de erro retornada por **SQLGetDiagRec** no buffer * \* MessageText* descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar memória necessária para dar suporte à execução ou à conclusão da função.|  
|HY009|Uso inválido de ponteiro nulo|O argumento de atributo identificou um atributo de ambiente que exigia um valor de cadeia de caracteres e o argumento *ValuePtr* era um ponteiro nulo.|  
|HY010|Erro de sequência de função|(DM) um identificador de conexão foi alocado em *EnvironmentHandle*.<br /><br /> (DM) **SQL_ATTR_ODBC_VERSION** não foi definido com **SQLSetEnvAttr** e o *atributo* não é igual a **SQL_ATTR_ODBC_VERSION**. Você não precisará definir **SQL_ATTR_ODBC_VERSION** explicitamente se estiver usando **SQLAllocHandleStd**.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não puderam ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY024|Valor de atributo inválido|Dado o valor do *atributo* especificado, um valor inválido foi especificado em *ValuePtr*.|  
|HY090|Comprimento de cadeia de caracteres ou buffer inválido|O argumento *StringLength* era menor que 0, mas não foi SQL_NTS.|  
|HY092|Identificador de atributo/opção inválido|(DM) o valor especificado para o *atributo* de argumento não era válido para a versão do ODBC com suporte do driver.|  
|HY117|A conexão foi suspensa devido a um estado de transação desconhecido. Somente funções de desconexão e somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Recurso opcional não implementado|O valor especificado para o *atributo* de argumento era um atributo de ambiente ODBC válido para a versão do ODBC com suporte do driver, mas não foi suportado pelo driver.<br /><br /> (DM) o argumento de *atributo* foi SQL_ATTR_OUTPUT_NTS e *ValuePtr* foi SQL_FALSE.|  
  
## <a name="comments"></a>Comentários  
 Um aplicativo pode chamar **SQLSetEnvAttr** somente se nenhum identificador de conexão for alocado no ambiente. Todos os atributos de ambiente definidos com êxito pelo aplicativo para o ambiente persistem até que **SQLFreeHandle** seja chamado no ambiente. Mais de um identificador de ambiente pode ser alocado simultaneamente no ODBC *3. x*.  
  
 O formato das informações definidas por meio de *ValuePtr* depende do *atributo*especificado. **SQLSetEnvAttr** aceitará informações de atributo em um dos dois formatos diferentes: uma cadeia de caracteres terminada em nulo ou um valor inteiro de 32 bits. O formato de cada um é observado na descrição do atributo.  
  
 Não há atributos de ambiente específicos do driver.  
  
 Os atributos de conexão não podem ser definidos por uma chamada para **SQLSetEnvAttr**. Tentar fazer isso retornará SQLSTATE HY092 (identificador de atributo/opção inválido).  
  
|*Atributo*|Conteúdo do *ValuePtr*|  
|-----------------|-------------------------|  
|SQL_ATTR_CONNECTION_POOLING (ODBC 3,8)|Um valor SQLUINTEGER de 32 bits que habilita ou desabilita o pool de conexões no nível do ambiente. Os seguintes valores são usados:<br /><br /> SQL_CP_OFF = o pool de conexões está desativado. Esse é o padrão.<br /><br /> SQL_CP_ONE_PER_DRIVER = há suporte para um único pool de conexões para cada driver. Cada conexão em um pool é associada a um driver.<br /><br /> SQL_CP_ONE_PER_HENV = há suporte para um único pool de conexões para cada ambiente. Cada conexão em um pool é associada a um ambiente.<br /><br /> SQL_CP_DRIVER_AWARE = use o recurso de reconhecimento de pool de conexões do driver, se estiver disponível. Se o driver não oferecer suporte ao reconhecimento do pool de conexões, SQL_CP_DRIVER_AWARE será ignorado e SQL_CP_ONE_PER_HENV será usado. Para obter mais informações, consulte [pooling de conexão com reconhecimento de driver](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md). Em um ambiente em que alguns drivers dão suporte e alguns drivers não dão suporte ao reconhecimento de pool de conexões, SQL_CP_DRIVER_AWARE pode habilitar o recurso de reconhecimento de pool de conexões nesses drivers de suporte, mas é equivalente a definir como SQL_CP_ONE_PER_HENV nesses drivers que não dão suporte ao recurso de reconhecimento de pool de conexões.<br /><br /> O pool de conexões é habilitado chamando **SQLSetEnvAttr** para definir o atributo SQL_ATTR_CONNECTION_POOLING como SQL_CP_ONE_PER_DRIVER ou SQL_CP_ONE_PER_HENV. Essa chamada deve ser feita antes que o aplicativo aloque o ambiente compartilhado para o qual o pool de conexões deve ser habilitado. O identificador de ambiente na chamada para **SQLSetEnvAttr** é definido como NULL, o que faz SQL_ATTR_CONNECTION_POOLING um atributo de nível de processo. Depois que o pool de conexões é habilitado, o aplicativo aloca um ambiente compartilhado implícito chamando **SQLAllocHandle** com o argumento *InputHandle* definido como SQL_HANDLE_ENV.<br /><br /> Depois que o pool de conexões tiver sido habilitado e um ambiente compartilhado tiver sido selecionado para um aplicativo, SQL_ATTR_CONNECTION_POOLING não poderá ser redefinido para esse ambiente, porque **SQLSetEnvAttr** é chamado com um identificador de ambiente nulo ao definir esse atributo. Se esse atributo for definido enquanto o pool de conexões já estiver habilitado em um ambiente compartilhado, o atributo afetará apenas os ambientes compartilhados que forem alocados posteriormente.<br /><br /> Também é possível habilitar o pool de conexões em um ambiente. Observe o seguinte sobre o pool de conexões de ambiente:<br /><br /> -Habilitar o pool de conexões em um identificador nulo é um atributo de nível de processo. Os ambientes alocados subsequentemente serão um ambiente compartilhado e herdarão a configuração de pool de conexões no nível de processo.<br />-Depois que um ambiente é alocado, um aplicativo ainda pode alterar sua configuração de pool de conexões.<br />-Se o pool de conexões do ambiente estiver habilitado e o driver da conexão usar o pool de drivers, o pooling de ambiente terá preferência.<br /><br /> O SQL_ATTR_CONNECTION_POOLING é implementado dentro do Gerenciador de driver. Um driver não precisa implementar SQL_ATTR_CONNECTION_POOLING. Os aplicativos ODBC 2,0 e 3,0 podem definir esse atributo de ambiente.<br /><br /> Para obter mais informações, consulte [ODBC Connection Pooling](../../../odbc/reference/develop-app/driver-manager-connection-pooling.md).|  
|SQL_ATTR_CP_MATCH (ODBC 3,0)|Um valor SQLUINTEGER de 32 bits que determina como uma conexão é escolhida de um pool de conexões. Quando **SQLConnect** ou **SQLDriverConnect** é chamado, o Gerenciador de driver determina qual conexão é reutilizada do pool. O Gerenciador de driver tenta corresponder as opções de conexão na chamada e os atributos de conexão definidos pelo aplicativo para as palavras-chave e os atributos de conexão das conexões no pool. O valor desse atributo determina o nível de precisão dos critérios de correspondência.<br /><br /> Os valores a seguir são usados para definir o valor deste atributo:<br /><br /> SQL_CP_STRICT_MATCH = somente conexões que correspondem exatamente às opções de conexão na chamada e os atributos de conexão definidos pelo aplicativo são reutilizados. Esse é o padrão.<br /><br /> SQL_CP_RELAXED_MATCH = conexões com palavras-chave de cadeia de conexão correspondentes podem ser usadas. As palavras-chave devem corresponder, mas nem todos os atributos de conexão devem corresponder.<br /><br /> Para obter mais informações sobre como o Gerenciador de driver executa a correspondência ao conectar-se a uma conexão em pool, consulte [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md). Para obter mais informações sobre o pool de conexões, consulte [ODBC Connection Pooling](../../../odbc/reference/develop-app/driver-manager-connection-pooling.md).|  
|SQL_ATTR_ODBC_VERSION (ODBC 3,0)|Um inteiro de 32 bits que determina se determinada funcionalidade exibe o comportamento ODBC *2. x* ou o comportamento ODBC *3. x* . Os valores a seguir são usados para definir o valor deste atributo:<br /><br /> SQL_OV_ODBC3_80 = o driver e o Gerenciador de driver exibem o seguinte comportamento de ODBC 3,8:<br /><br /> -O driver retorna e espera códigos ODBC *3. x* para Date, time e timestamp.<br />-O driver retorna códigos do ODBC *3. x* SQLSTATE quando **SqlError**, **SQLGetDiagField**ou **SQLGetDiagRec** é chamado.<br />-O argumento *CatalogName* em uma chamada para **SQLTables** aceita um padrão de pesquisa.<br />-O Gerenciador de driver dá suporte à extensibilidade de tipo de dados C. Para obter mais informações sobre a extensibilidade de tipo de dados C, consulte [tipos de dados c em ODBC](../../../odbc/reference/develop-app/c-data-types-in-odbc.md).<br /><br /> Para obter mais informações, consulte [What ' s New in ODBC 3,8](../../../odbc/reference/what-s-new-in-odbc-3-8.md).<br /><br /> SQL_OV_ODBC3 = o driver e o Gerenciador de driver exibem o seguinte comportamento do ODBC *3. x* :<br /><br /> -O driver retorna e espera códigos ODBC *3. x* para Date, time e timestamp.<br />-O driver retorna códigos do ODBC *3. x* SQLSTATE quando **SqlError**, **SQLGetDiagField**ou **SQLGetDiagRec** é chamado.<br />-O argumento *CatalogName* em uma chamada para **SQLTables** aceita um padrão de pesquisa.<br />-O Gerenciador de driver não dá suporte à extensibilidade de tipo de dados C.<br /><br /> SQL_OV_ODBC2 = o driver e o Gerenciador de driver exibem o seguinte comportamento ODBC *2. x* . Isso é especialmente útil para um aplicativo ODBC *2. x* trabalhando com um driver ODBC *3. x* .<br /><br /> -O driver retorna e espera códigos ODBC *2. x* para Date, time e timestamp.<br />-O driver retorna códigos ODBC *2. x* SQLSTATE quando **SqlError**, **SQLGetDiagField**ou **SQLGetDiagRec** é chamado.<br />-O argumento *CatalogName* em uma chamada para **SQLTables** não aceita um padrão de pesquisa.<br />-O Gerenciador de driver não dá suporte à extensibilidade de tipo de dados C.<br /><br /> Um aplicativo deve definir esse atributo de ambiente antes de chamar qualquer função que tenha um argumento SQLHENV, ou a chamada retornará SQLSTATE HY010 (erro de sequência de função). Ele é específico do driver, independentemente de o comportamento adicional existir para esses sinalizadores ambientais.<br /><br /> -Para obter mais informações, consulte [declarando a versão ODBC do aplicativo](../../../odbc/reference/develop-app/declaring-the-application-s-odbc-version.md) e [as alterações comportamentais](../../../odbc/reference/develop-app/behavioral-changes.md).|  
|SQL_ATTR_OUTPUT_NTS (ODBC 3,0)|Um inteiro de 32 bits que determina como o driver retorna dados de cadeia de caracteres. Se SQL_TRUE, o driver retornará dados de cadeia de caracteres terminados em nulo. Se SQL_FALSE, o driver não retornará uma cadeia de caracteres de dados terminada em nulo.<br /><br /> Esse atributo usa como padrão SQL_TRUE. Uma chamada para **SQLSetEnvAttr** para defini-lo como SQL_TRUE retorna SQL_SUCCESS. Uma chamada para **SQLSetEnvAttr** para defini-lo como SQL_FALSE retorna SQL_ERROR e SQLSTATE HYC00 (recurso opcional não implementado).|  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Alocando um identificador|[Função SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|Retornando a configuração de um atributo de ambiente|[Função SQLGetEnvAttr](../../../odbc/reference/syntax/sqlgetenvattr-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Novidades no ODBC 3.8](../../../odbc/reference/what-s-new-in-odbc-3-8.md)
