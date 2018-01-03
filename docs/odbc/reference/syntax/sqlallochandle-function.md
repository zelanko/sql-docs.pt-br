---
title: "Função SQLAllocHandle | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLAllocHandle
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLAllocHandle
helpviewer_keywords: SQLAllocHandle function [ODBC]
ms.assetid: 6e7fe420-8cf4-4e72-8dad-212affaff317
caps.latest.revision: "43"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: b8bf173bf0055dc06cf475aa72e137d9ca426222
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="sqlallochandle-function"></a>Função SQLAllocHandle
**Conformidade**  
 Versão introduzidas: Conformidade de padrões 3.0 ODBC: 92 ISO  
  
 **Resumo**  
 **SQLAllocHandle** aloca um identificador de ambiente, conexão, instrução ou descritor.  
  
> [!NOTE]  
>  Essa função é uma função genérica para alocar identificadores que substitui as funções ODBC 2.0 **SQLAllocConnect**, **SQLAllocEnv**, e **SQLAllocStmt**. Para permitir que aplicativos que chamam **SQLAllocHandle** para trabalhar com ODBC 2. *x* drivers, uma chamada para **SQLAllocHandle** está mapeado no Gerenciador de Driver para **SQLAllocConnect**, **SQLAllocEnv**, ou  **SQLAllocStmt**, conforme apropriado. Para obter mais informações, consulte "Comentários". Para obter mais informações sobre o que o Gerenciador de Driver mapeia essa função quando um ODBC 3. *x* aplicativo estiver trabalhando com um ODBC 2. *x* driver, consulte [mapeamento de funções de substituição para compatibilidade com versões anteriores de aplicativos](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SQLRETURN SQLAllocHandle(  
      SQLSMALLINT   HandleType,  
      SQLHANDLE     InputHandle,  
      SQLHANDLE *   OutputHandlePtr);  
```  
  
## <a name="arguments"></a>Argumentos  
 *HandleType*  
 [Entrada] O tipo de identificador a ser alocada por **SQLAllocHandle**. Deve ser um dos seguintes valores:  
  
-   SQL_HANDLE_DBC  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV  
  
-   SQL_HANDLE_STMT  
  
 Identificador SQL_HANDLE_DBC_INFO_TOKEN é usado somente pelo Gerenciador de Driver e do driver. Aplicativos não devem usar este tipo de identificador. Para obter mais informações sobre SQL_HANDLE_DBC_INFO_TOKEN, consulte [desenvolvendo o reconhecimento do Pool de Conexão em um Driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md).  
  
 *InputHandle*  
 [Entrada] O identificador de entrada em cujo contexto o novo identificador é a ser alocada. Se *HandleType* é SQL_HANDLE_ENV, isso é SQL_NULL_HANDLE. Se *HandleType* é SQL_HANDLE_DBC, isso deve ser um identificador de ambiente e se ele for SQL_HANDLE_STMT ou SQL_HANDLE_DESC, ele deve ser um identificador de conexão.  
  
 *OutputHandlePtr*  
 [Saída] Ponteiro para um buffer no qual retornar o identificador para a estrutura de dados recentemente alocado.  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_INVALID_HANDLE ou SQL_ERROR.  
  
 Ao alocar um identificador que não seja um identificador de ambiente, se **SQLAllocHandle** retornará SQL_ERROR, ele define *OutputHandlePtr* SQL_NULL_HDBC, SQL_NULL_HSTMT ou SQL_NULL_HDESC, dependendo do valor de *HandleType*, a menos que o argumento de saída é um ponteiro nulo. O aplicativo pode, em seguida, obter informações adicionais da estrutura de dados de diagnóstico associada com o identificador no *InputHandle* argumento.  
  
## <a name="environment-handle-allocation-errors"></a>Erros de alocação de identificador de ambiente  
 Alocação de ambiente ocorre no Gerenciador de Driver e dentro de cada driver. O erro retornado por **SQLAllocHandle** com um *HandleType* SQL_HANDLE_ENV depende do nível no qual ocorreu o erro.  
  
 Se o Gerenciador de Driver não pode alocar memória para  *\*OutputHandlePtr* quando **SQLAllocHandle** com um *HandleType* SQL_HANDLE_ENV é chamado, ou o aplicativo fornece um ponteiro nulo para *OutputHandlePtr*, **SQLAllocHandle** retornará SQL_ERROR. O Gerenciador de Driver define **OutputHandlePtr* para SQL_NULL_HENV (a menos que o aplicativo fornecido um ponteiro nulo, que retorna SQL_ERROR). Não há nenhum identificador ao qual associar informações adicionais de diagnóstico.  
  
 O Gerenciador de Driver não chama a função de alocação de identificador de ambiente de nível de driver até que o aplicativo chama **SQLConnect**, **SQLBrowseConnect**, ou **SQLDriverConnect**. Se ocorrer um erro no nível do driver **SQLAllocHandle** função, em seguida, o Gerenciador de Driver – nível **SQLConnect**, **SQLBrowseConnect**, ou  **SQLDriverConnect** função retornará SQL_ERROR. A estrutura de dados de diagnóstico contém SQLSTATE IM004 (do Driver **SQLAllocHandle** falha). O erro é retornado em um identificador de conexão.  
  
 Para obter mais informações sobre o fluxo de chamadas de função entre o Gerenciador de Driver e um driver, consulte [função SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md).  
  
## <a name="diagnostics"></a>diagnóstico  
 Quando **SQLAllocHandle** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtida chamando **SQLGetDiagRec** com apropriada *HandleType* e *tratar* definido como o valor de *InputHandle*. SQL_SUCCESS_WITH_INFO (mas não SQL_ERROR) podem ser retornadas para o *OutputHandle* argumento. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLAllocHandle** e explica cada uma no contexto dessa função; a notação "(DM)" precede as descrições de SQLSTATEs retornados pelo Gerenciador de Driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado em contrário.  
  
|SQLSTATE|Erro|Description|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem de informação específica do driver. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|08003|Conexão não aberta|(DM) a *HandleType* argumento era SQL_HANDLE_STMT ou SQL_HANDLE_DESC, mas a conexão especificada pelo *InputHandle* argumento não foi aberto. O processo de conexão deve ser concluído com êxito (e a conexão deve estar aberta) para o driver a alocar uma instrução ou um descritor de identificador.|  
|HY000|Erro geral|Ocorreu um erro para o qual não houve nenhuma SQLSTATE específico e para o qual nenhuma SQLSTATE específicos de implementação foi definida. A mensagem de erro retornada pelo **SQLGetDiagRec** no **MessageText* buffer descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O Gerenciador de Driver (DM) não pôde alocar memória para o identificador especificado.<br /><br /> O driver não pôde alocar memória para o identificador especificado.|  
|HY009|Uso inválido de ponteiro nulo|(DM) a *OutputHandlePtr* argumento era um ponteiro nulo.|  
|HY010|Erro de sequência de função|(DM) a *HandleType* argumento era SQL_HANDLE_DBC, e **SQLSetEnvAttr** não foi chamado para definir o atributo de ambiente SQL_ODBC_VERSION.<br /><br /> (DM) uma função de execução assíncrona foi chamada para o **InputHandle** e ainda estava em execução quando o **SQLAllocHandle** função foi chamada com **HandleType** definido SQL_HANDLE_STMT ou SQL_HANDLE_DESC.|  
|HY013|Erro de gerenciamento de memória|O *HandleType* argumento era SQL_HANDLE_DBC, SQL_HANDLE_STMT ou SQL_HANDLE_DESC; e a chamada de função não pôde ser processada porque os objetos de memória subjacente não podem ser acessados, possivelmente devido à memória insuficiente condições.|  
|HY014|Limite o número de identificadores excedido|O limite definido pelo driver para o número de identificadores que podem ser alocados para o tipo de identificador indicado pelo *HandleType* argumento foi atingido.|  
|HY092|Identificador de atributo/opção inválido|(DM) a *HandleType* argumento não era: SQL_HANDLE_ENV, SQL_HANDLE_DBC, SQL_HANDLE_STMT ou SQL_HANDLE_DESC.|  
|HY117|Conexão está suspenso devido ao estado de transação desconhecido. Somente Desconecte e funções de somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Recurso opcional não implementado|O *HandleType* argumento SQL_HANDLE_DESC e o driver era um ODBC 2. *x* driver.|  
|HYT01|Tempo limite de Conexão expirou|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não dá suporte a esta função|(DM) a *HandleType* argumento SQL_HANDLE_STMT, e o driver não era um driver ODBC válido.<br /><br /> (DM) a *HandleType* argumento era SQL_HANDLE_DESC, e o driver não dá suporte para alocar um identificador do descritor.|  
  
## <a name="comments"></a>Comentários  
 **SQLAllocHandle** é usada para alocar identificadores para ambientes, conexões, instruções e descritores, conforme descrito nas seções a seguir. Para obter informações gerais sobre identificadores, consulte [identificadores](../../../odbc/reference/develop-app/handles.md).  
  
 Mais de um identificador de ambiente, conexão ou instrução pode ser alocado por um aplicativo por vez se várias alocações são suportadas pelo driver. No ODBC, nenhum limite é definido no número de ambiente, conexão, instrução ou identificadores de descritor que podem ser alocados a qualquer momento. Drivers podem impor um limite no número de um determinado tipo de identificador que pode ser alocada ao mesmo tempo; Para obter mais informações, consulte a documentação do driver.  
  
 Se o aplicativo chama **SQLAllocHandle** com  *\*OutputHandlePtr* definido para um ambiente, a conexão, a instrução ou o identificador do descritor que já existe, o driver substituirá o informações associadas a *tratar*, a menos que o aplicativo está usando a conexão pooling (consulte "Alocar um ambiente de atributo de Conexão Pooling" nesta seção). O Gerenciador de Driver não verifica para ver se o *tratar* inserido no  *\*OutputHandlePtr* já está sendo usado, nem a ele verifique o conteúdo anterior de um identificador antes de substituí-las .  
  
> [!NOTE]  
>  É incorretova programação de aplicativo de ODBC para chamar **SQLAllocHandle** duas vezes com a mesma variável de aplicativo definida para  *\*OutputHandlePtr* sem chamar  **SQLFreeHandle** para liberar o identificador antes realocando-lo. Substituindo o ODBC identificadores dessa forma podem levar a um comportamento inconsistente ou erros por parte de drivers ODBC.  
  
 Em sistemas operacionais que oferecem suporte a vários threads, os aplicativos podem usar o mesmo identificador de ambiente, conexão, instrução ou descritor em threads diferentes. Drivers, portanto, devem oferecer suporte ao acesso seguro, multithread essas informações; uma maneira de fazer isso, por exemplo, é por meio de uma seção crítica ou um semáforo. Para obter mais informações sobre threading, consulte [Multithreading](../../../odbc/reference/develop-app/multithreading.md).  
  
 **SQLAllocHandle** não define o atributo de ambiente SQL_ATTR_ODBC_VERSION quando ela é chamada para alocar um identificador de ambiente; o atributo de ambiente deve ser definido pelo aplicativo ou SQLSTATE HY010 serão (erro de sequência de função) retornado quando **SQLAllocHandle** é chamado para alocar um identificador de conexão.  
  
 Para aplicativos compatíveis com padrões, **SQLAllocHandle** é mapeado para **SQLAllocHandleStd** em tempo de compilação. A diferença entre essas duas funções é que **SQLAllocHandleStd** define o atributo de ambiente SQL_ATTR_ODBC_VERSION como SQL_OV_ODBC3 quando ele é chamado com o *HandleType* argumento definido como SQL _HANDLE_ENV. Isso é feito porque aplicativos compatíveis com os padrões são sempre ODBC 3. *x* aplicativos. Além disso, os padrões não exigem a versão do aplicativo a ser registrado. Essa é a única diferença entre essas duas funções; Caso contrário, eles são idênticos. **SQLAllocHandleStd** é mapeado para **SQLAllocHandle** dentro do Gerenciador de driver. Portanto, os drivers de terceiros não é necessário que implementar **SQLAllocHandleStd**.  
  
 Aplicativos ODBC 3.8 devem usar:  
  
-   **SQLAllocHandle e não SQLAllocHandleStd** para alocar um identificador de ambiente.  
  
-   **SQLSetEnvAttr** para definir o atributo de ambiente SQL_ATTR_ODBC_VERSION como SQL_OV_ODBC3_80.  
  
## <a name="allocating-an-environment-handle"></a>Alocando um identificador de ambiente  
 Um identificador de ambiente fornece acesso às informações globais, como identificadores de conexão válido e conexão ativa. Para obter informações gerais sobre identificadores de ambiente, consulte [identificadores de ambiente](../../../odbc/reference/develop-app/environment-handles.md).  
  
 Para solicitar um identificador de ambiente, um aplicativo chama **SQLAllocHandle** com um *HandleType* SQL_HANDLE_ENV e um *InputHandle* de SQL_NULL_HANDLE. O driver aloca memória para as informações de ambiente e passa o valor do identificador associado novamente o  *\*OutputHandlePtr* argumento. A aplicativo passa o  *\*OutputHandle* valor em todas as chamadas subsequentes que exigem um argumento de identificador de ambiente. Para obter mais informações, consulte [ao alocar identificador de ambiente](../../../odbc/reference/develop-app/allocating-the-environment-handle.md).  
  
 Em um Gerenciador de Driver do identificador de ambiente, se já houver identificador de ambiente do driver, em seguida, **SQLAllocHandle** com um *HandleType* SQL_HANDLE_ENV não é chamado no driver quando um conexão é feita, somente **SQLAllocHandle** com um *HandleType* SQL_HANDLE_DBC. Se o identificador de ambiente do driver não existe no identificador de ambiente do Gerenciador de Driver, SQLAllocHandle com um HandleType de SQL_HANDLE_ENV e SQLAllocHandle com um HandleType de SQL_HANDLE_DBC são chamados no driver quando a primeira conexão Identificador do ambiente é conectado ao driver.  
  
 Quando o Gerenciador de Driver processa o **SQLAllocHandle** funcionar com um *HandleType* SQL_HANDLE_ENV, ele verifica o **rastreamento** palavra-chave na seção do sistema [ODBC] informações. Se estiver definido como 1, o Gerenciador de Driver habilita rastreamento para o aplicativo atual. Se o sinalizador de rastreamento for definido, o rastreamento é iniciado quando o primeiro identificador de ambiente é alocado e termina quando o último identificador de ambiente é liberado. Para obter mais informações, consulte [configurar fontes de dados](../../../odbc/reference/install/configuring-data-sources.md).  
  
 Depois de alocar um identificador de ambiente, um aplicativo deve chamar **SQLSetEnvAttr** na alça de ambiente para definir o atributo de ambiente SQL_ATTR_ODBC_VERSION. Se esse atributo não for definido antes de **SQLAllocHandle** é chamado para alocar um identificador de conexão no ambiente, a chamada para alocar a conexão retornará SQLSTATE HY010 (erro de sequência de função). Para obter mais informações, consulte [declarar a versão do aplicativo ODBC](../../../odbc/reference/develop-app/declaring-the-application-s-odbc-version.md).  
  
## <a name="allocating-shared-environments-for-connection-pooling"></a>Alocando ambientes compartilhados para o pool de Conexão  
 Ambientes podem ser compartilhados entre vários componentes em um único processo. Um ambiente compartilhado pode ser usado por mais de um componente ao mesmo tempo. Quando um componente usa um ambiente compartilhado, ele pode usar conexões em pool, que permitem alocar e usar uma conexão existente sem recriar essa conexão.  
  
 Antes de alocar um ambiente compartilhado que pode ser usado para o pool de conexão, um aplicativo deve chamar **SQLSetEnvAttr** para definir o atributo de ambiente SQL_ATTR_CONNECTION_POOLING SQL_CP_ONE_PER_DRIVER ou SQL_CP_ONE_PER_ HENV. **SQLSetEnvAttr** nesse caso é chamado com *EnvironmentHandle* definido como null, o que torna o atributo de um atributo de nível de processo.  
  
 Após a habilitação do pool de conexão, um aplicativo chama **SQLAllocHandle** com o *HandleType* argumento definido como SQL_HANDLE_ENV. O ambiente alocado por essa chamada será um ambiente compartilhado implícito porque o pool de conexão foi ativado.  
  
 Quando é alocado um ambiente compartilhado, o ambiente que será usado não é determinado até **SQLAllocHandle** com um *HandleType* SQL_HANDLE_DBC é chamado. Nesse ponto, o Gerenciador de Driver tenta encontrar um ambiente existente que correspondem aos atributos de ambiente solicitados pelo aplicativo. Se tal ambiente não existir, um será criado como um ambiente compartilhado. O Gerenciador de Driver mantém uma contagem de referência para cada ambiente compartilhado; a contagem é definida como 1 quando o ambiente é criado pela primeira vez. Se um ambiente correspondente for encontrado, o identificador de ambiente é retornado para o aplicativo e a contagem de referência é incrementada. Um identificador de ambiente alocado dessa maneira pode ser usado em qualquer função ODBC que aceita um identificador de ambiente como um argumento de entrada.  
  
## <a name="allocating-a-connection-handle"></a>Alocando um identificador de conexão  
 Um identificador de conexão fornece acesso às informações, como a instrução válida e identificadores de descritor de conexão e se uma transação está sendo aberto. Para obter informações gerais sobre os identificadores de conexão, consulte [identificadores de Conexão](../../../odbc/reference/develop-app/connection-handles.md).  
  
 Para solicitar um identificador de conexão, um aplicativo chama **SQLAllocHandle** com um *HandleType* SQL_HANDLE_DBC. O *InputHandle* argumento é definido como o identificador de ambiente que foi retornado pela chamada para **SQLAllocHandle** que alocado esse identificador. O driver aloca memória para as informações de conexão e passa o valor do identificador associado novamente  *\*OutputHandlePtr*. A aplicativo passa o  *\*OutputHandlePtr* valor em todas as chamadas subsequentes que exigem um identificador de conexão. Para obter mais informações, consulte [alocar um identificador de Conexão](../../../odbc/reference/develop-app/allocating-a-connection-handle-odbc.md).  
  
 O Gerenciador de Driver processa o **SQLAllocHandle** de função e chama o driver **SQLAllocHandle** funcionar quando o aplicativo chama **SQLConnect**, **SQLBrowseConnect**, ou **SQLDriverConnect**. (Para obter mais informações, consulte [função SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md).)  
  
 Se o atributo de ambiente SQL_ATTR_ODBC_VERSION não está definido antes de **SQLAllocHandle** é chamado para alocar um identificador de conexão no ambiente, a chamada para alocar a conexão retornará SQLSTATE HY010 (sequência de função Erro).  
  
 Quando um aplicativo chama **SQLAllocHandle** com o *InputHandle* argumento definido como SQL_HANDLE_DBC e também definir um identificador de ambiente compartilhado, o Gerenciador de Driver tenta encontrar um compartilhado existente ambiente que correspondem aos atributos de ambiente definidos pelo aplicativo. Se tal ambiente não existir, um será criado, com uma contagem de referência (mantida pelo Gerenciador de Driver) de 1. Se uma correspondência compartilhado ambiente for encontrado, esse identificador é retornado para o aplicativo e sua contagem de referência é incrementada.  
  
 A conexão real que será usada não é determinado pelo Gerenciador de Driver até **SQLConnect** ou **SQLDriverConnect** é chamado. O Gerenciador de Driver usa as opções de conexão na chamada para **SQLConnect** (ou as palavras-chave de conexão na chamada para **SQLDriverConnect**) e os atributos de conexão definidos após a alocação de conexão Determine qual conexão no pool deve ser usado. Para obter mais informações, consulte [função SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md).  
  
## <a name="allocating-a-statement-handle"></a>Alocando um identificador de instrução  
 Um identificador de instrução fornece acesso às informações de instrução, como mensagens de erro, o nome de cursor e informações de status para o processamento de uma instrução SQL. Para obter informações gerais sobre identificadores de instrução, consulte [identificadores de instrução](../../../odbc/reference/develop-app/statement-handles.md).  
  
 Para solicitar um identificador de instrução, um aplicativo se conecta a uma fonte de dados e, em seguida, chama **SQLAllocHandle** antes que ele envia instruções SQL. Nessa chamada *HandleType* deve ser definido como SQL_HANDLE_STMT e *InputHandle* deve ser definido como o identificador de conexão que foi retornado pela chamada para **SQLAllocHandle** que alocado esse identificador. O driver aloca memória para as informações de declaração, associa o identificador de instrução de conexão especificado e passa o valor do identificador associado novamente  *\*OutputHandlePtr*. A aplicativo passa o  *\*OutputHandlePtr* valor em todas as chamadas subsequentes que exigem um identificador de instrução. Para obter mais informações, consulte [alocar um identificador de instrução](../../../odbc/reference/develop-app/allocating-a-statement-handle-odbc.md).  
  
 Quando o identificador de instrução é alocado, o driver automaticamente aloca um conjunto de descritores de quatro e atribui as alças para esses descritores de SQL_ATTR_APP_ROW_DESC, SQL_ATTR_APP_PARAM_DESC, SQL_ATTR_IMP_ROW_DESC e SQL_ATTR_IMP_PARAM_DESC atributos de instrução. Esses são chamados de *implicitamente* alocada descritores. Para alocar explicitamente um descritor de aplicativo, consulte a seção a seguir, "Alocar um identificador do descritor."  
  
## <a name="allocating-a-descriptor-handle"></a>Alocando um identificador do descritor  
 Quando um aplicativo chama **SQLAllocHandle** com um *HandleType* de SQL_HANDLE_DESC, o driver aloca um descritor de aplicativo. Esses são chamados de *explicitamente* alocada descritores. O aplicativo direciona um driver para usar um descritor de aplicativo explicitamente alocados em vez de um alocado automaticamente para um identificador de instrução determinado chamando o **SQLSetStmtAttr** função com o SQL_ATTR_APP_ROW_DESC ou o atributo SQL_ATTR_APP_PARAM_DESC. Um descritor de implementação não pode ser alocado explicitamente, nem um descritor de implementação pode ser especificado em uma **SQLSetStmtAttr** chamada de função.  
  
 Descritores explicitamente alocados estão associados com um identificador de conexão em vez de um identificador de instrução (como descritores alocados automaticamente). Descritores permanecem alocados somente quando um aplicativo, na verdade, está conectado ao banco de dados. Porque descritores explicitamente alocados estão associados com um identificador de conexão, um aplicativo pode associar um descritor alocado explicitamente com mais de uma instrução em uma conexão. Um descritor de aplicativo alocado implicitamente, por outro lado, não é possível associar mais de um identificador de instrução. (Ele não pode ser associado a qualquer identificador de instrução diferente na qual ele foi alocado para.) Identificadores de descritor alocado explicitamente podem ser liberados explicitamente pelo aplicativo ou chamando **SQLFreeHandle** com um *HandleType* de SQL_HANDLE_DESC ou implicitamente, quando a conexão é fechado.  
  
 Quando o descritor alocado explicitamente é liberado, o descritor alocado implicitamente novamente é associado à instrução. (O atributo SQL_ATTR_APP_ROW_DESC ou SQL_ATTR_APP_PARAM_DESC para essa instrução, novamente, é definido como o indicador de descritor alocado implicitamente.) Isso é verdadeiro para todas as instruções que estavam associadas com o descritor de alocado explicitamente a conexão.  
  
 Para obter mais informações sobre descritores, consulte [descritores](../../../odbc/reference/develop-app/descriptors.md).  
  
## <a name="code-example"></a>Exemplo de código  
 Consulte [ODBC programa de exemplo](../../../odbc/reference/sample-odbc-program.md), [função SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md), [função SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md), e [função SQLSetCursorName](../../../odbc/reference/syntax/sqlsetcursorname-function.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Executar uma instrução SQL|[Função SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Executar uma instrução preparada do SQL|[Função SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Liberando um identificador de ambiente, conexão, instrução ou descritor|[Função SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|Preparar uma instrução para execução|[Função SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|  
|Definir um atributo de conexão|[Função SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|Configuração de um campo de descritor|[Função SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|Definindo um atributo de ambiente|[Função SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)|  
|Definir um atributo de instrução|[Função SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
