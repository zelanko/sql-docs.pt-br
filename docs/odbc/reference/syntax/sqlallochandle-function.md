---
title: Função SQLAllocHandle | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLAllocHandle
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLAllocHandle
helpviewer_keywords:
- SQLAllocHandle function [ODBC]
ms.assetid: 6e7fe420-8cf4-4e72-8dad-212affaff317
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2fcf08a4a55a7c65dbc94219ac908da83ea15bad
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68344275"
---
# <a name="sqlallochandle-function"></a>Função SQLAllocHandle
**Conformidade**  
 Versão introduzida: conformidade de padrões do ODBC 3,0: ISO 92  
  
 **Resumo**  
 **SQLAllocHandle** aloca um ambiente, uma conexão, uma instrução ou um identificador de descritor.  
  
> [!NOTE]  
>  Essa função é uma função genérica para alocar identificadores que substitui as funções de ODBC 2,0 **SQLAllocConnect**, **SQLAllocEnv**e **SQLAllocStmt**. Para permitir que aplicativos que chamam o **SQLAllocHandle** funcionem com o ODBC 2. drivers *x* , uma chamada para **SQLAllocHandle** é mapeada no Gerenciador de driver para **SQLAllocConnect**, **SQLAllocEnv**ou **SQLAllocStmt**, conforme apropriado. Para obter mais informações, consulte "Comentários". Para obter mais informações sobre como o Gerenciador de driver mapeia essa função quando um ODBC 3. o aplicativo *x* está funcionando com um ODBC 2. Driver *x* , consulte [mapeando funções de substituição para compatibilidade com versões anteriores de aplicativos](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLAllocHandle(  
      SQLSMALLINT   HandleType,  
      SQLHANDLE     InputHandle,  
      SQLHANDLE *   OutputHandlePtr);  
```  
  
## <a name="arguments"></a>Argumentos  
 *HandleType*  
 Entrada O tipo de identificador a ser alocado por **SQLAllocHandle**. Deve ser um dos seguintes valores:   
  
-   SQL_HANDLE_DBC  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV  
  
-   SQL_HANDLE_STMT  
  
 O identificador de SQL_HANDLE_DBC_INFO_TOKEN é usado somente pelo driver e pelo Gerenciador de driver. Os aplicativos não devem usar esse tipo de identificador. Para obter mais informações sobre SQL_HANDLE_DBC_INFO_TOKEN, consulte [desenvolvendo o reconhecimento do pool de conexões em um driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md).  
  
 *InputHandle*  
 Entrada O identificador de entrada em cujo contexto o novo identificador deve ser alocado. Se *HandleType* for SQL_HANDLE_ENV, isso será SQL_NULL_HANDLE. Se *HandleType* for SQL_HANDLE_DBC, ele deverá ser um identificador de ambiente e, se for SQL_HANDLE_STMT ou SQL_HANDLE_DESC, ele deverá ser um identificador de conexão.  
  
 *OutputHandlePtr*  
 Der Ponteiro para um buffer no qual retornar o identificador para a estrutura de dados alocada recentemente.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_INVALID_HANDLE ou SQL_ERROR.  
  
 Ao alocar um identificador que não seja um identificador de ambiente, se **SQLAllocHandle** retornar SQL_ERROR, ele definirá *OutputHandlePtr* como SQL_NULL_HDBC, SQL_NULL_HSTMT ou SQL_NULL_HDESC, dependendo do valor de *HandleType*, a menos que o argumento de saída seja um ponteiro nulo. O aplicativo pode obter informações adicionais da estrutura de dados de diagnóstico associada ao identificador no argumento *InputHandle* .  
  
## <a name="environment-handle-allocation-errors"></a>Erros de alocação de identificador de ambiente  
 A alocação de ambiente ocorre tanto no Gerenciador de driver quanto em cada driver. O erro retornado por **SQLAllocHandle** com um *handletype* de SQL_HANDLE_ENV depende do nível em que o erro ocorreu.  
  
 Se o Gerenciador de driver não puder alocar memória para * \*OutputHandlePtr* quando **SQLAllocHandle** com um *HandleType* de SQL_HANDLE_ENV for chamado ou o aplicativo fornecer um ponteiro nulo para *OutputHandlePtr*, **SQLAllocHandle** retornará SQL_ERROR. O Gerenciador de driver define **OutputHandlePtr* como SQL_NULL_HENV (a menos que o aplicativo tenha fornecido um ponteiro nulo, que retorna SQL_ERROR). Não há nenhum identificador com o qual associar informações de diagnóstico adicionais.  
  
 O Gerenciador de driver não chama a função de alocação de identificador de ambiente de nível de driver até que o aplicativo chame **SQLConnect**, **SQLBrowseConnect**ou **SQLDriverConnect**. Se ocorrer um erro na função **SQLAllocHandle** no nível do driver, a função de nível do Gerenciador de driver **SQLConnect**, **SQLBrowseConnect**ou **SQLDriverConnect** retornará SQL_ERROR. A estrutura de dados de diagnóstico contém SQLSTATE IM004 (falha de **SQLAllocHandle** do driver). O erro é retornado em um identificador de conexão.  
  
 Para obter mais informações sobre o fluxo de chamadas de função entre o Gerenciador de driver e um driver, consulte [função SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md).  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **SQLAllocHandle** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido chamando **SQLGetDiagRec** com o *identificadortype* apropriado e o *identificador* definido como o valor de *InputHandle*. SQL_SUCCESS_WITH_INFO (mas não SQL_ERROR) podem ser retornados para o argumento *OutputHandle* . A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLAllocHandle** e explica cada um no contexto dessa função; a notação "(DM)" precede as descrições de sqlstates retornadas pelo Gerenciador de driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
|SQLSTATE|Erro|DESCRIÇÃO|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa específica do driver. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|08003|Conexão não aberta|(DM) o argumento *HandleType* foi SQL_HANDLE_STMT ou SQL_HANDLE_DESC, mas a conexão especificada pelo argumento *InputHandle* não foi aberta. O processo de conexão deve ser concluído com êxito (e a conexão deve estar aberta) para que o driver aloque uma instrução ou um identificador de descritor.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia um SQLSTATE específico e para o qual nenhum SQLSTATE específico de implementação foi definido. A mensagem de erro retornada por **SQLGetDiagRec** no buffer **MessageText* descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|(DM) o Gerenciador de driver não pôde alocar memória para o identificador especificado.<br /><br /> O driver não pôde alocar memória para o identificador especificado.|  
|HY009|Uso inválido de ponteiro nulo|(DM) o argumento *OutputHandlePtr* era um ponteiro nulo.|  
|HY010|Erro de sequência de função|(DM) o argumento *HandleType* foi SQL_HANDLE_DBC e **SQLSetEnvAttr** não foi chamado para definir o atributo de ambiente SQL_ODBC_VERSION.<br /><br /> (DM) uma função de execução assíncrona foi chamada para o **InputHandle** e ainda estava em execução quando a função **SQLAllocHandle** foi chamada com **HandleType** definido como SQL_HANDLE_STMT ou SQL_HANDLE_DESC.|  
|HY013|Erro de gerenciamento de memória|O argumento *HandleType* foi SQL_HANDLE_DBC, SQL_HANDLE_STMT ou SQL_HANDLE_DESC; e a chamada de função não pôde ser processada porque os objetos de memória subjacentes não puderam ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY014|Limite do número de identificadores excedido|O limite definido pelo driver para o número de identificadores que podem ser alocados para o tipo de identificador indicado pelo argumento *HandleType* foi atingido.|  
|HY092|Identificador de atributo/opção inválido|(DM) o argumento *HandleType* não foi: SQL_HANDLE_ENV, SQL_HANDLE_DBC, SQL_HANDLE_STMT ou SQL_HANDLE_DESC.|  
|HY117|A conexão foi suspensa devido a um estado de transação desconhecido. Somente funções de desconexão e somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Recurso opcional não implementado|O argumento *HandleType* foi SQL_HANDLE_DESC e o driver era um ODBC 2. Driver *x* .|  
|HYT01|Tempo limite de conexão expirado|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|O driver não oferece suporte a essa função|(DM) o argumento *HandleType* foi SQL_HANDLE_STMT e o driver não era um driver ODBC válido.<br /><br /> (DM) o argumento *HandleType* foi SQL_HANDLE_DESC e o driver não dá suporte à alocação de um identificador de descritor.|  
  
## <a name="comments"></a>Comentários  
 **SQLAllocHandle** é usado para alocar identificadores para ambientes, conexões, instruções e descritores, conforme descritos nas seções a seguir. Para obter informações gerais sobre identificadores, consulte [Handles](../../../odbc/reference/develop-app/handles.md).  
  
 Mais de um ambiente, conexão ou identificador de instrução podem ser alocados por um aplicativo por vez se várias alocações forem suportadas pelo driver. No ODBC, nenhum limite é definido no número de identificadores de ambiente, conexão, instrução ou descritor que podem ser alocados a qualquer momento. Os drivers podem impor um limite no número de um determinado tipo de identificador que pode ser alocado de cada vez; para obter mais informações, consulte a documentação do driver.  
  
 Se o aplicativo chamar **SQLAllocHandle** com * \*OutputHandlePtr* definido como um ambiente, uma conexão, uma instrução ou um identificador de descritor que já existe, o driver substituirá as informações associadas ao *identificador*, a menos que o aplicativo esteja usando o pool de conexões (consulte "alocando um atributo de ambiente para o pool de conexões" mais adiante nesta seção). O Gerenciador de driver não verifica se o *identificador* inserido no * \*OutputHandlePtr* já está sendo usado, nem verifica o conteúdo anterior de um identificador antes de substituí-lo.  
  
> [!NOTE]  
>  É uma programação de aplicativo ODBC incorreta para chamar **SQLAllocHandle** duas vezes com a mesma variável de aplicativo definida para * \*OutputHandlePtr* sem chamar **SQLFreeHandle** para liberar o identificador antes de realocá-lo. A substituição de identificadores ODBC de forma pode levar a um comportamento inconsistente ou erros na parte de drivers ODBC.  
  
 Em sistemas operacionais que dão suporte a vários threads, os aplicativos podem usar o mesmo ambiente, conexão, instrução ou identificador de descritor em threads diferentes. Os drivers devem, portanto, dar suporte ao acesso seguro e multithread a essas informações; uma maneira de conseguir isso, por exemplo, é usar uma seção crítica ou um semáforo. Para obter mais informações sobre Threading, consulte [multithreading](../../../odbc/reference/develop-app/multithreading.md).  
  
 **SQLAllocHandle** não define o atributo de ambiente SQL_ATTR_ODBC_VERSION quando ele é chamado para alocar um identificador de ambiente; o atributo de ambiente deve ser definido pelo aplicativo, ou SQLSTATE HY010 (erro de sequência de função) será retornado quando **SQLAllocHandle** for chamado para alocar um identificador de conexão.  
  
 Para aplicativos em conformidade com os padrões, **SQLAllocHandle** é mapeado para **SQLAllocHandleStd** no momento da compilação. A diferença entre essas duas funções é que **SQLAllocHandleStd** define o atributo de ambiente SQL_ATTR_ODBC_VERSION como SQL_OV_ODBC3 quando ele é chamado com o argumento *HandleType* definido como SQL_HANDLE_ENV. Isso é feito porque os aplicativos em conformidade com os padrões sempre são ODBC 3. aplicativos *x* . Além disso, os padrões não exigem que a versão do aplicativo seja registrada. Essa é a única diferença entre essas duas funções; caso contrário, eles serão idênticos. **SQLAllocHandleStd** é mapeado para **SQLAllocHandle** dentro do Gerenciador de driver. Portanto, os drivers de terceiros não precisam implementar **SQLAllocHandleStd**.  
  
 Os aplicativos ODBC 3,8 devem usar:  
  
-   **SQLAllocHandle e não SQLAllocHandleStd** para alocar um identificador de ambiente.  
  
-   **SQLSetEnvAttr** para definir o atributo de ambiente SQL_ATTR_ODBC_VERSION como SQL_OV_ODBC3_80.  
  
## <a name="allocating-an-environment-handle"></a>Alocando um identificador de ambiente  
 Um identificador de ambiente fornece acesso a informações globais, como identificadores de conexão e identificadores de conexão ativos válidos. Para obter informações gerais sobre os identificadores de ambiente, consulte [identificadores de ambiente](../../../odbc/reference/develop-app/environment-handles.md).  
  
 Para solicitar um identificador de ambiente, um aplicativo chama **SQLAllocHandle** com um *handletype* de SQL_HANDLE_ENV e um *InputHandle* de SQL_NULL_HANDLE. O driver aloca memória para as informações de ambiente e passa o valor do identificador associado de volta no argumento * \*OutputHandlePtr* . O aplicativo passa o * \*valor OutputHandle* em todas as chamadas subsequentes que exigem um argumento de identificador de ambiente. Para obter mais informações, consulte [alocando o identificador de ambiente](../../../odbc/reference/develop-app/allocating-the-environment-handle.md).  
  
 Em um identificador de ambiente do Gerenciador de driver, se já existir um identificador de ambiente do driver, **SQLAllocHandle** com um *handletype* de SQL_HANDLE_ENV não será chamado nesse driver quando uma conexão for feita, somente **SQLAllocHandle** com um *HandleType* de SQL_HANDLE_DBC. Se o identificador de ambiente de um driver não existir no identificador de ambiente do Gerenciador de driver, ambos SQLAllocHandle com um HandleType de SQL_HANDLE_ENV e SQLAllocHandle com um HandleType de SQL_HANDLE_DBC serão chamados no driver quando a primeira conexão o identificador do ambiente está conectado ao driver.  
  
 Quando o Gerenciador de driver processa a função **SQLAllocHandle** com um *handletype* de SQL_HANDLE_ENV, ele verifica a palavra-chave **trace** na seção [ODBC] das informações do sistema. Se estiver definido como 1, o Gerenciador de driver habilitará o rastreamento para o aplicativo atual. Se o sinalizador de rastreamento for definido, o rastreamento será iniciado quando o primeiro identificador de ambiente for alocado e terminará quando o último identificador de ambiente for liberado. Para obter mais informações, consulte [Configurando fontes de dados](../../../odbc/reference/install/configuring-data-sources.md).  
  
 Depois de alocar um identificador de ambiente, um aplicativo deve chamar **SQLSetEnvAttr** no identificador de ambiente para definir o atributo de ambiente SQL_ATTR_ODBC_VERSION. Se esse atributo não for definido antes de **SQLAllocHandle** ser chamado para alocar um identificador de conexão no ambiente, a chamada para alocar a conexão retornará SQLSTATE HY010 (erro de sequência de função). Para obter mais informações, consulte [declarando a versão ODBC do aplicativo](../../../odbc/reference/develop-app/declaring-the-application-s-odbc-version.md).  
  
## <a name="allocating-shared-environments-for-connection-pooling"></a>Alocando ambientes compartilhados para o pool de conexões  
 Os ambientes podem ser compartilhados entre vários componentes em um único processo. Um ambiente compartilhado pode ser usado por mais de um componente ao mesmo tempo. Quando um componente usa um ambiente compartilhado, ele pode usar conexões em pool, o que permite alocar e usar uma conexão existente sem recriar essa conexão.  
  
 Antes de alocar um ambiente compartilhado que possa ser usado para o pool de conexões, um aplicativo deve chamar **SQLSetEnvAttr** para definir o atributo de ambiente SQL_ATTR_CONNECTION_POOLING como SQL_CP_ONE_PER_DRIVER ou SQL_CP_ONE_PER_HENV. **SQLSetEnvAttr** nesse caso é chamado com *EnvironmentHandle* definido como NULL, o que torna o atributo um atributo de nível de processo.  
  
 Depois que o pool de conexões tiver sido habilitado, um aplicativo chamará **SQLAllocHandle** com o argumento *HandleType* definido como SQL_HANDLE_ENV. O ambiente alocado por essa chamada será um ambiente compartilhado implícito porque o pool de conexões foi habilitado.  
  
 Quando um ambiente compartilhado é alocado, o ambiente que será usado não é determinado até que **SQLAllocHandle** com um *handletype* de SQL_HANDLE_DBC seja chamado. Nesse ponto, o Gerenciador de driver tenta encontrar um ambiente existente que corresponda aos atributos de ambiente solicitados pelo aplicativo. Se esse ambiente não existir, um será criado como um ambiente compartilhado. O Gerenciador de driver mantém uma contagem de referência para cada ambiente compartilhado; a contagem é definida como 1 quando o ambiente é criado pela primeira vez. Se um ambiente de correspondência for encontrado, o identificador desse ambiente será retornado ao aplicativo e a contagem de referência será incrementada. Um identificador de ambiente alocado dessa maneira pode ser usado em qualquer função ODBC que aceite um identificador de ambiente como um argumento de entrada.  
  
## <a name="allocating-a-connection-handle"></a>Alocando um identificador de conexão  
 Um identificador de conexão fornece acesso a informações como os identificadores de instrução e descritores válidos na conexão e se uma transação está aberta no momento. Para obter informações gerais sobre identificadores de conexão, consulte [identificadores de conexão](../../../odbc/reference/develop-app/connection-handles.md).  
  
 Para solicitar um identificador de conexão, um aplicativo chama **SQLAllocHandle** com um *handletype* de SQL_HANDLE_DBC. O argumento *InputHandle* é definido como o identificador de ambiente que foi retornado pela chamada para **SQLAllocHandle** que alocou esse identificador. O driver aloca memória para as informações de conexão e passa o valor do identificador associado de volta no * \*OutputHandlePtr*. O aplicativo passa o * \*valor OutputHandlePtr* em todas as chamadas subsequentes que exigem um identificador de conexão. Para obter mais informações, consulte [alocando um identificador de conexão](../../../odbc/reference/develop-app/allocating-a-connection-handle-odbc.md).  
  
 O Gerenciador de driver processa a função **SQLAllocHandle** e chama a função **SQLAllocHandle** do driver quando o aplicativo chama **SQLConnect**, **SQLBrowseConnect**ou **SQLDriverConnect**. (Para obter mais informações, consulte [função SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md).)  
  
 Se o atributo de ambiente SQL_ATTR_ODBC_VERSION não estiver definido antes de **SQLAllocHandle** ser chamado para alocar um identificador de conexão no ambiente, a chamada para alocar a conexão retornará SQLSTATE HY010 (erro de sequência de função).  
  
 Quando um aplicativo chama **SQLAllocHandle** com o argumento *InputHandle* definido como SQL_HANDLE_DBC e também é definido como um identificador de ambiente compartilhado, o Gerenciador de driver tenta encontrar um ambiente compartilhado existente que corresponda aos atributos de ambiente definidos pelo aplicativo. Se esse ambiente não existir, um será criado, com uma contagem de referência (mantida pelo Gerenciador de driver) de 1. Se um ambiente compartilhado correspondente for encontrado, esse identificador será retornado para o aplicativo e sua contagem de referência será incrementada.  
  
 A conexão real que será usada não será determinada pelo Gerenciador de driver até que **SQLConnect** ou **SQLDriverConnect** seja chamado. O Gerenciador de driver usa as opções de conexão na chamada para **SQLConnect** (ou as palavras-chave de conexão na chamada de **SQLDriverConnect**) e os atributos de conexão definidos após a alocação de conexão para determinar qual conexão no pool deve ser usada. Para obter mais informações, consulte [função SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md).  
  
## <a name="allocating-a-statement-handle"></a>Alocando um identificador de instrução  
 Um identificador de instrução fornece acesso a informações de instrução, como mensagens de erro, o nome do cursor e informações de status do processamento da instrução SQL. Para obter informações gerais sobre identificadores de instrução, consulte [identificadores de instrução](../../../odbc/reference/develop-app/statement-handles.md).  
  
 Para solicitar um identificador de instrução, um aplicativo se conecta a uma fonte de dados e, em seguida, chama **SQLAllocHandle** antes de enviar instruções SQL. Nesta chamada, *identificadortype* deve ser definido como SQL_HANDLE_STMT e *InputHandle* deve ser definido como o identificador de conexão que foi retornado pela chamada para **SQLAllocHandle** que alocou esse identificador. O driver aloca memória para as informações da instrução, associa o identificador de instrução à conexão especificada e passa o valor do identificador associado de volta em * \*OutputHandlePtr*. O aplicativo passa o * \*valor OutputHandlePtr* em todas as chamadas subsequentes que exigem um identificador de instrução. Para obter mais informações, consulte [alocando um identificador de instrução](../../../odbc/reference/develop-app/allocating-a-statement-handle-odbc.md).  
  
 Quando o identificador de instrução é alocado, o driver aloca automaticamente um conjunto de quatro descritores e atribui os identificadores para esses descritores ao SQL_ATTR_APP_ROW_DESC, SQL_ATTR_APP_PARAM_DESC, SQL_ATTR_IMP_ROW_DESC e SQL_ATTR_IMP_PARAM_DESC atributos de instrução. Eles são chamados de descritores *implicitamente* alocados. Para alocar um descritor de aplicativo explicitamente, consulte a seção a seguir, "alocando um identificador de descritor".  
  
## <a name="allocating-a-descriptor-handle"></a>Alocando um identificador de descritor  
 Quando um aplicativo chama **SQLAllocHandle** com um *handletype* de SQL_HANDLE_DESC, o driver aloca um descritor de aplicativo. Eles são chamados de descritores *explicitamente* alocados. O aplicativo direciona um driver para usar um descritor de aplicativo explicitamente alocado em vez de um atribuído automaticamente para um determinado identificador de instrução chamando a função **SQLSetStmtAttr** com o atributo SQL_ATTR_APP_ROW_DESC ou SQL_ATTR_APP_PARAM_DESC. Um descritor de implementação não pode ser alocado explicitamente nem um descritor de implementação pode ser especificado em uma chamada de função **SQLSetStmtAttr** .  
  
 Os descritores explicitamente alocados são associados a um identificador de conexão em vez de um identificador de instrução (já que os descritores alocados automaticamente são). Os descritores permanecem alocados somente quando um aplicativo está realmente conectado ao banco de dados. Como os descritores explicitamente alocados estão associados a um identificador de conexão, um aplicativo pode associar um descritor explicitamente alocado a mais de uma instrução em uma conexão. Um descritor de aplicativo implicitamente alocado, por outro lado, não pode ser associado a mais de um identificador de instrução. (Ele não pode ser associado a qualquer identificador de instrução diferente daquele para o qual foi alocado.) Identificadores de descritor explicitamente alocados podem ser liberados explicitamente pelo aplicativo ou chamando **SQLFreeHandle** com um *handletype* de SQL_HANDLE_DESC ou implicitamente quando a conexão é fechada.  
  
 Quando o descritor explicitamente alocado for liberado, o descritor implicitamente alocado será associado novamente à instrução. (O atributo SQL_ATTR_APP_ROW_DESC ou SQL_ATTR_APP_PARAM_DESC para essa instrução é definido novamente como o identificador de descritor alocado implicitamente.) Isso é verdadeiro para todas as instruções que foram associadas ao descritor explicitamente alocado na conexão.  
  
 Para obter mais informações sobre descritores, consulte [descritores](../../../odbc/reference/develop-app/descriptors.md).  
  
## <a name="code-example"></a>Exemplo de código  
 Consulte [exemplo de programa de ODBC](../../../odbc/reference/sample-odbc-program.md), [função SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md), [função SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)e [função SQLSetCursorName](../../../odbc/reference/syntax/sqlsetcursorname-function.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Executando uma instrução SQL|[Função SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Executando uma instrução SQL preparada|[Função SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Liberando um ambiente, conexão, instrução ou identificador de descritor|[Função SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|Preparando uma instrução para execução|[Função SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|  
|Definindo um atributo de conexão|[Função SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|Configurando um campo de descritor|[Função SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|Configurando um atributo de ambiente|[Função SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)|  
|Definindo um atributo de instrução|[Função SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
