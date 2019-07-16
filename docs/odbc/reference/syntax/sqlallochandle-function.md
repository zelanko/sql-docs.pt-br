---
title: Função SQLAllocHandle | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLAllocHandle
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLAllocHandle
helpviewer_keywords:
- SQLAllocHandle function [ODBC]
ms.assetid: 6e7fe420-8cf4-4e72-8dad-212affaff317
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3f4f82a24e594a25b0b1ec9bbeab2256624ae6e9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68036256"
---
# <a name="sqlallochandle-function"></a>Função SQLAllocHandle
**Conformidade com**  
 Versão introduzida: Conformidade com padrões 3.0 ODBC: ISO 92  
  
 **Resumo**  
 **Falha de SQLAllocHandle** aloca um identificador de ambiente, conexão, instrução ou descritor.  
  
> [!NOTE]  
>  Essa função é uma função genérica para alocar identificadores que substitui as funções ODBC 2.0 **SQLAllocConnect**, **SQLAllocEnv**, e **SQLAllocStmt**. Para permitir que os aplicativos que chamam **SQLAllocHandle** para trabalhar com ODBC 2. *x* drivers, uma chamada para **SQLAllocHandle** é mapeada no Gerenciador de Driver para **SQLAllocConnect**, **SQLAllocEnv**, ou  **SQLAllocStmt**, conforme apropriado. Para obter mais informações, consulte "Comentários". Para obter mais informações sobre o que o Gerenciador de Driver mapeia essa função quando um ODBC 3. *x* aplicativo está funcionando com um ODBC 2. *x* driver, consulte [mapeamento de funções de substituição para compatibilidade com versões anteriores de aplicativos](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLAllocHandle(  
      SQLSMALLINT   HandleType,  
      SQLHANDLE     InputHandle,  
      SQLHANDLE *   OutputHandlePtr);  
```  
  
## <a name="arguments"></a>Argumentos  
 *HandleType*  
 [Entrada] O tipo de identificador a ser alocada pelo **SQLAllocHandle**. Deve ser um dos seguintes valores:  
  
-   SQL_HANDLE_DBC  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV  
  
-   SQL_HANDLE_STMT  
  
 Identificador SQL_HANDLE_DBC_INFO_TOKEN é usado somente pelo Gerenciador de Driver e o driver. Aplicativos não devem usar esse tipo de identificador. Para obter mais informações sobre SQL_HANDLE_DBC_INFO_TOKEN, consulte [desenvolvendo o reconhecimento de Pool de Conexão em um Driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md).  
  
 *InputHandle*  
 [Entrada] O identificador de entrada em cujo contexto o novo identificador deve ser alocado. Se *HandleType* é SQL_HANDLE_ENV, isso é SQL_NULL_HANDLE. Se *HandleType* é SQL_HANDLE_DBC, isso deve ser um identificador de ambiente e se ele for SQL_HANDLE_STMT ou SQL_HANDLE_DESC, ele deve ser um identificador de conexão.  
  
 *OutputHandlePtr*  
 [Saída] Ponteiro para um buffer no qual retornar o identificador para a estrutura de dados recentemente alocado.  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_INVALID_HANDLE ou SQL_ERROR.  
  
 Ao alocar um identificador que não seja um identificador de ambiente, se **SQLAllocHandle** retornará SQL_ERROR, ele define *OutputHandlePtr* SQL_NULL_HDBC, SQL_NULL_HSTMT ou SQL_NULL_HDESC, dependendo do valor de *HandleType*, a menos que o argumento de saída for um ponteiro nulo. O aplicativo, em seguida, pode obter informações adicionais da estrutura de dados de diagnóstico associada com o identificador na *InputHandle* argumento.  
  
## <a name="environment-handle-allocation-errors"></a>Erros de alocação de identificador de ambiente  
 Alocação de ambiente ocorre dentro do Gerenciador de Driver e dentro de cada driver. O erro retornado por **SQLAllocHandle** com um *HandleType* SQL_HANDLE_ENV depende do nível no qual ocorreu o erro.  
  
 Se o Gerenciador de Driver não é possível alocar memória para  *\*OutputHandlePtr* quando **SQLAllocHandle** com um *HandleType* SQL_HANDLE_ENV é chamado, ou o aplicativo fornece um ponteiro nulo para *OutputHandlePtr*, **SQLAllocHandle** retornará SQL_ERROR. Define o Gerenciador de Driver **OutputHandlePtr* para SQL_NULL_HENV (a menos que o aplicativo fornecido um ponteiro nulo, que retorna SQL_ERROR). Não há nenhum identificador ao qual associar informações adicionais de diagnóstico.  
  
 O Gerenciador de Driver não chama a função de alocação de identificador de ambiente em nível de driver até que o aplicativo chame **SQLConnect**, **SQLBrowseConnect**, ou **SQLDriverConnect**. Se ocorrer um erro no nível do driver **SQLAllocHandle** função e, em seguida, o nível de Gerenciador de Driver **SQLConnect**, **SQLBrowseConnect**, ou  **SQLDriverConnect** função retornará SQL_ERROR. A estrutura de dados de diagnóstico contém SQLSTATE IM004 (motorista **SQLAllocHandle** falha). O erro é retornado em um identificador de conexão.  
  
 Para obter mais informações sobre o fluxo de chamadas de função entre o Gerenciador de Driver e um driver, consulte [função SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md).  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLAllocHandle** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtida chamando **SQLGetDiagRec** com os devidos *HandleType* e *manipular* definido como o valor de *InputHandle*. SQL_SUCCESS_WITH_INFO (mas não SQL_ERROR) podem ser retornadas para o *OutputHandle* argumento. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLAllocHandle** e explica cada uma no contexto dessa função; a notação "(DM)" precede as descrições das SQLSTATEs retornados pelo Gerenciador de Driver. O código de retorno associado com cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa de específicos do driver. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|08003|Conexão não aberta|(DM) a *HandleType* argumento era SQL_HANDLE_STMT ou SQL_HANDLE_DESC, mas a conexão especificada pela *InputHandle* argumento não foi aberto. O processo de conexão deve ser concluído com êxito (e a conexão deve estar aberta) para o driver a alocar uma instrução ou um descritor de identificador.|  
|HY000|Erro geral|Ocorreu um erro para o qual não houve nenhum SQLSTATE específico e para o qual não foi definida nenhuma SQLSTATE específicos de implementação. A mensagem de erro retornada por **SQLGetDiagRec** no **MessageText* buffer descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O Gerenciador de Driver (DM) não pôde alocar memória para o identificador especificado.<br /><br /> O driver não pôde alocar memória para o identificador especificado.|  
|HY009|Uso inválido de ponteiro nulo|(DM) a *OutputHandlePtr* argumento é um ponteiro nulo.|  
|HY010|Erro de sequência de função|(DM) a *HandleType* argumento era SQL_HANDLE_DBC, e **SQLSetEnvAttr** não foi chamado para definir o atributo de ambiente SQL_ODBC_VERSION.<br /><br /> (DM) uma função de execução assíncrona foi chamada para o **InputHandle** e ainda estava em execução quando o **SQLAllocHandle** função foi chamada com **HandleType** definido para SQL_HANDLE_STMT ou SQL_HANDLE_DESC.|  
|HY013|Erro de gerenciamento de memória|O *HandleType* argumento era SQL_HANDLE_DBC, SQL_HANDLE_STMT ou SQL_HANDLE_DESC; e a chamada de função não pôde ser processada porque os objetos de memória subjacente não pôde ser acessados, possivelmente devido à memória insuficiente condições.|  
|HY014|Limitar o número de indicadores excedido|O limite definido pelo driver para o número de identificadores que podem ser alocados para o tipo de identificador indicada pela *HandleType* argumento foi atingido.|  
|HY092|Identificador de atributo/opção inválido|(DM) a *HandleType* argumento não era: SQL_HANDLE_ENV, SQL_HANDLE_DBC, SQL_HANDLE_STMT ou SQL_HANDLE_DESC.|  
|HY117|Conexão está suspenso devido ao estado de transação desconhecida. Somente se desconectar e funções de somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Recurso opcional não implementado|O *HandleType* argumento era SQL_HANDLE_DESC e o driver foi um ODBC 2. *x* driver.|  
|HYT01|Tempo limite da Conexão expirado|O período de tempo limite de conexão expirado antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não oferece suporte a essa função|(DM) a *HandleType* argumento era SQL_HANDLE_STMT e o driver não era um driver ODBC válido.<br /><br /> (DM) a *HandleType* argumento era SQL_HANDLE_DESC, e o driver não oferece suporte para alocar um identificador do descritor.|  
  
## <a name="comments"></a>Comentários  
 **Falha de SQLAllocHandle** é usado para alocar identificadores para ambientes, conexões, instruções e descritores, conforme descrito nas seções a seguir. Para obter informações gerais sobre identificadores, consulte [identificadores](../../../odbc/reference/develop-app/handles.md).  
  
 Mais de um identificador de ambiente, conexão ou instrução pode ser alocado por um aplicativo por vez, se várias alocações são compatíveis com o driver. No ODBC, nenhum limite é definido no número de ambiente, conexão, instrução ou identificadores de descritor que podem ser alocados a qualquer momento. Drivers podem impor um limite no número de um determinado tipo de identificador que pode ser alocada ao mesmo tempo; Para obter mais informações, consulte a documentação do driver.  
  
 Se o aplicativo chamar **SQLAllocHandle** com  *\*OutputHandlePtr* definido como um ambiente, a conexão, a instrução ou o identificador do descritor que já existe, o driver substituirá o informações associadas com o *manipular*, a menos que o aplicativo está usando a conexão pooling (consulte "Alocando um ambiente de atributo para Conexão Pooling" nesta seção). O Gerenciador de Driver não verifica para ver se o *manipular* inserido na  *\*OutputHandlePtr* já está sendo usado, nem oferece verificar o conteúdo anterior de um identificador antes de substituí-los .  
  
> [!NOTE]  
>  Ele é incorreta programação de aplicativo de ODBC para chamar **SQLAllocHandle** duas vezes com a mesma variável de aplicativo definida para  *\*OutputHandlePtr* sem chamar  **SQLFreeHandle** para liberar o identificador antes de realocar a ele. Substituindo ODBC alças dessa maneira pode levar a erros por parte de drivers ODBC ou um comportamento inconsistente.  
  
 Em sistemas operacionais que dão suporte a vários threads, os aplicativos podem usar o mesmo identificador de ambiente, conexão, instrução ou descritor em threads diferentes. Drivers, portanto, devem dar suporte ao acesso seguro, com vários threads a essas informações; uma maneira de fazer isso, por exemplo, é por meio de uma seção crítica ou um semáforo. Para obter mais informações sobre threading, consulte [Multithreading](../../../odbc/reference/develop-app/multithreading.md).  
  
 **Falha de SQLAllocHandle** não define o atributo de ambiente SQL_ATTR_ODBC_VERSION quando ela é chamada para alocar um identificador de ambiente; o atributo de ambiente deve ser definido pelo aplicativo ou SQLSTATE HY010 será (erro de sequência de função) retornado quando **SQLAllocHandle** é chamado para alocar um identificador de conexão.  
  
 Para aplicativos compatíveis com padrões, **SQLAllocHandle** é mapeado para **SQLAllocHandleStd** em tempo de compilação. A diferença entre essas duas funções é que **SQLAllocHandleStd** define o atributo de ambiente SQL_ATTR_ODBC_VERSION como SQL_OV_ODBC3 quando ele é chamado com o *HandleType* argumento definido como SQL _HANDLE_ENV. Isso é feito porque aplicativos compatíveis com os padrões são sempre ODBC 3. *x* aplicativos. Além disso, os padrões não exigem a versão do aplicativo a ser registrado. Isso é a única diferença entre essas duas funções; Caso contrário, eles são idênticos. **SQLAllocHandleStd** é mapeado para **SQLAllocHandle** dentro do Gerenciador de driver. Portanto, os drivers de terceiros não é necessário que implementar **SQLAllocHandleStd**.  
  
 Os aplicativos ODBC 3.8 devem usar:  
  
-   **Falha de SQLAllocHandle e não SQLAllocHandleStd** para alocar um identificador de ambiente.  
  
-   **SQLSetEnvAttr** para definir o atributo de ambiente SQL_ATTR_ODBC_VERSION como SQL_OV_ODBC3_80.  
  
## <a name="allocating-an-environment-handle"></a>Alocando um identificador de ambiente  
 Um identificador de ambiente fornece acesso às informações globais, como identificadores de conexão válida e identificadores de conexão do Active Directory. Para obter informações gerais sobre identificadores de ambiente, consulte [identificadores de ambiente](../../../odbc/reference/develop-app/environment-handles.md).  
  
 Para solicitar um identificador de ambiente, um aplicativo chama **SQLAllocHandle** com um *HandleType* SQL_HANDLE_ENV e uma *InputHandle* de SQL_NULL_HANDLE. O driver aloca memória para as informações de ambiente e os passa de volta o valor do identificador associado a  *\*OutputHandlePtr* argumento. O aplicativo passa o  *\*OutputHandle* valor em todas as chamadas subsequentes que exigem um argumento de identificador de ambiente. Para obter mais informações, consulte [alocar o identificador de ambiente](../../../odbc/reference/develop-app/allocating-the-environment-handle.md).  
  
 Em um identificador de ambiente do Gerenciador de Driver, se já existe identificador de ambiente de um driver, em seguida **SQLAllocHandle** com um *HandleType* SQL_HANDLE_ENV não é chamado no driver quando um conexão é feita, apenas **SQLAllocHandle** com um *HandleType* SQL_HANDLE_DBC. Se o identificador de ambiente de um driver não existe sob o identificador de ambiente do Gerenciador de Driver, SQLAllocHandle com um HandleType de SQL_HANDLE_ENV e SQLAllocHandle com um HandleType de SQL_HANDLE_DBC são chamados no driver quando a primeira conexão Identificador do ambiente é conectado ao driver.  
  
 Quando o Gerenciador de Driver processa os **SQLAllocHandle** funcionar com um *HandleType* SQL_HANDLE_ENV, ele verifica o **rastreamento** palavra-chave na seção [ODBC] do sistema informações. Se ele for definido como 1, o Gerenciador de Driver habilita rastreamento para o aplicativo atual. Se o sinalizador de rastreamento for definido, o rastreamento é iniciado quando o identificador de ambiente primeiro é alocado e termina quando o último identificador de ambiente é liberado. Para obter mais informações, consulte [Configurando fontes de dados](../../../odbc/reference/install/configuring-data-sources.md).  
  
 Depois de alocar um identificador de ambiente, um aplicativo deve chamar **SQLSetEnvAttr** o identificador de ambiente para definir o atributo de ambiente SQL_ATTR_ODBC_VERSION. Se esse atributo não for definido antes **SQLAllocHandle** é chamado para alocar um identificador de conexão no ambiente, a chamada para alocar a conexão retornará SQLSTATE HY010 (erro de sequência de função). Para obter mais informações, consulte [declarando a versão do aplicativo ODBC](../../../odbc/reference/develop-app/declaring-the-application-s-odbc-version.md).  
  
## <a name="allocating-shared-environments-for-connection-pooling"></a>Alocando ambientes compartilhados para o pool de Conexão  
 Ambientes podem ser compartilhados entre vários componentes em um único processo. Um ambiente compartilhado pode ser usado por mais de um componente ao mesmo tempo. Quando um componente usa um ambiente compartilhado, ele pode usar conexões em pool, o qual permitirem a alocar e usar uma conexão existente sem recriar essa conexão.  
  
 Antes de alocar um ambiente compartilhado que pode ser usado para o pool de conexão, um aplicativo deve chamar **SQLSetEnvAttr** para definir o atributo de ambiente SQL_ATTR_CONNECTION_POOLING SQL_CP_ONE_PER_DRIVER ou SQL_CP_ONE_PER_ HENV. **SQLSetEnvAttr** nesse caso é chamado com *EnvironmentHandle* definido como null, o que torna o atributo de um atributo de nível de processo.  
  
 Depois que o pooling de conexão tiver sido habilitado, um aplicativo chama **SQLAllocHandle** com o *HandleType* argumento definido como SQL_HANDLE_ENV. O ambiente alocado por essa chamada será um ambiente compartilhado implícito porque o pooling de conexão tiver sido habilitado.  
  
 Quando é alocado um ambiente compartilhado, o ambiente que será usado não é determinado até **SQLAllocHandle** com um *HandleType* SQL_HANDLE_DBC é chamado. Nesse ponto, o Gerenciador de Driver tenta encontrar um ambiente existente que corresponde aos atributos de ambiente solicitados pelo aplicativo. Se esse ambiente não existe, um será criado como um ambiente compartilhado. O Gerenciador de Driver mantém uma contagem de referência para cada ambiente compartilhado; a contagem é definida como 1 quando o ambiente é criado. Se um ambiente correspondente for encontrado, o identificador de ambiente é retornado ao aplicativo e a contagem de referência é incrementada. Um identificador de ambiente alocado dessa maneira pode ser usado em qualquer função ODBC que aceita um identificador de ambiente como um argumento de entrada.  
  
## <a name="allocating-a-connection-handle"></a>Alocando um identificador de conexão  
 Um identificador de conexão fornece acesso a informações de como a instrução válida e abrir identificadores de descritor sobre a conexão e se uma transação é atualmente. Para obter informações gerais sobre os identificadores de conexão, consulte [identificadores de Conexão](../../../odbc/reference/develop-app/connection-handles.md).  
  
 Para solicitar um identificador de conexão, um aplicativo chama **SQLAllocHandle** com um *HandleType* SQL_HANDLE_DBC. O *InputHandle* argumento é definido como o identificador de ambiente que foi retornado pela chamada para **SQLAllocHandle** que alocado esse identificador. O driver aloca memória para as informações de conexão e os passa de volta o valor do identificador associado  *\*OutputHandlePtr*. O aplicativo passa o  *\*OutputHandlePtr* valor em todas as chamadas subsequentes que exigem um identificador de conexão. Para obter mais informações, consulte [alocando um identificador de Conexão](../../../odbc/reference/develop-app/allocating-a-connection-handle-odbc.md).  
  
 O Gerenciador de Driver processa os **SQLAllocHandle** de função e chama o driver **SQLAllocHandle** funcionar quando o aplicativo chama **SQLConnect**, **SQLBrowseConnect**, ou **SQLDriverConnect**. (Para obter mais informações, consulte [função SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md).)  
  
 Se o atributo de ambiente SQL_ATTR_ODBC_VERSION não for definido antes **SQLAllocHandle** é chamado para alocar um identificador de conexão no ambiente, a chamada para alocar a conexão retornará SQLSTATE HY010 (sequência de função Erro).  
  
 Quando um aplicativo chama **SQLAllocHandle** com o *InputHandle* argumento definido como SQL_HANDLE_DBC e também é definido como um identificador de ambiente compartilhado, o Gerenciador de Driver tenta encontrar um compartilhado existente ambiente que corresponde aos atributos de ambiente definidos pelo aplicativo. Se esse ambiente não existe, um será criado, com uma contagem de referência (mantida pelo Gerenciador de Driver) de 1. Se encontrar uma correspondência compartilhado ambiente for encontrado, esse identificador é retornado para o aplicativo e sua contagem de referência é incrementada.  
  
 A conexão real que será usado não é determinado pelo Gerenciador de Driver até **SQLConnect** ou **SQLDriverConnect** é chamado. O Gerenciador de Driver usa as opções de conexão na chamada para **SQLConnect** (ou as palavras-chave de conexão na chamada para **SQLDriverConnect**) e os atributos de conexão definidos após a alocação de conexão para Determine qual conexão no pool deve ser usado. Para obter mais informações, consulte [função SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md).  
  
## <a name="allocating-a-statement-handle"></a>Alocando um identificador de instrução  
 Um identificador de instrução fornece acesso a informações sobre a instrução, como mensagens de erro, o nome de cursor e informações de status para processamento de uma instrução SQL. Para obter informações gerais sobre identificadores de instrução, consulte [identificadores de instrução](../../../odbc/reference/develop-app/statement-handles.md).  
  
 Para solicitar um identificador de instrução, um aplicativo se conecta a uma fonte de dados e, em seguida, chama **SQLAllocHandle** antes de enviar instruções SQL. Nessa chamada *HandleType* deve ser definido como SQL_HANDLE_STMT e *InputHandle* deve ser definido como o identificador de conexão que foi retornado pela chamada para **SQLAllocHandle** que alocado esse identificador. O driver aloca memória para as informações de declaração, associa o identificador de instrução com a conexão especificada e passa o valor do identificador associado de volta no  *\*OutputHandlePtr*. O aplicativo passa o  *\*OutputHandlePtr* valor em todas as chamadas subsequentes que exigem um identificador de instrução. Para obter mais informações, consulte [alocando um identificador de instrução](../../../odbc/reference/develop-app/allocating-a-statement-handle-odbc.md).  
  
 Quando o identificador de instrução é alocado, o driver automaticamente aloca um conjunto de descritores de quatro e atribui as alças para esses descritores das SQL_ATTR_APP_ROW_DESC, SQL_ATTR_APP_PARAM_DESC, SQL_ATTR_IMP_ROW_DESC e SQL_ATTR_IMP_PARAM_DESC atributos de instrução. Esses são denominados *implicitamente* alocado descritores. Para alocar explicitamente um descritor de aplicativo, consulte a seção a seguir, "Alocando um identificador do descritor."  
  
## <a name="allocating-a-descriptor-handle"></a>Alocando um identificador do descritor  
 Quando um aplicativo chama **SQLAllocHandle** com um *HandleType* de SQL_HANDLE_DESC, o driver aloca um descritor de aplicativo. Esses são denominados *explicitamente* alocado descritores. O aplicativo direciona um driver para usar um descritor de aplicativo explicitamente alocados em vez de um alocado automaticamente para um identificador de instrução fornecida por meio da chamada a **SQLSetStmtAttr** função com o SQL_ATTR_APP_ROW_DESC ou o atributo SQL_ATTR_APP_PARAM_DESC. Um descritor de implementação não pode ser alocado explicitamente, nem um descritor de implementação pode ser especificado em uma **SQLSetStmtAttr** chamada de função.  
  
 Descritores explicitamente alocados estão associados com um identificador de conexão em vez de um identificador de instrução (como descritores alocados automaticamente). Descritores permanecem alocados somente quando um aplicativo está realmente conectado ao banco de dados. Porque descritores explicitamente alocados estão associados com um identificador de conexão, um aplicativo pode associar um descritor explicitamente alocado com mais de uma instrução dentro de uma conexão. Por outro lado, um descritor de aplicativo implicitamente alocados, não pode ser associado a mais de um identificador de instrução. (Ele não pode ser associado a qualquer identificador de instrução diferente daquele que ele foi alocado para.) Identificadores de descritor alocado explicitamente podem ser liberados explicitamente pelo aplicativo ou chamando **SQLFreeHandle** com um *HandleType* de SQL_HANDLE_DESC, ou implicitamente quando a conexão é fechado.  
  
 Quando o descritor alocado explicitamente é liberado, o descritor implicitamente alocado novamente está associado com a instrução. (O atributo SQL_ATTR_APP_ROW_DESC ou SQL_ATTR_APP_PARAM_DESC para essa instrução, novamente, é definido como o identificador do descritor alocado implicitamente.) Isso é verdadeiro para todas as instruções que estavam associadas com o descritor alocado explicitamente a conexão.  
  
 Para obter mais informações sobre descritores, consulte [descritores](../../../odbc/reference/develop-app/descriptors.md).  
  
## <a name="code-example"></a>Exemplo de código  
 Ver [programa ODBC de exemplo](../../../odbc/reference/sample-odbc-program.md), [função SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md), [função SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md), e [função SQLSetCursorName](../../../odbc/reference/syntax/sqlsetcursorname-function.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Executar uma instrução SQL|[Função SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Executar uma instrução SQL preparada|[Função SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Liberando um identificador de ambiente, conexão, instrução ou descritor|[Função SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|Como preparar uma instrução para execução|[Função SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|  
|Definir um atributo de conexão|[Função SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|Definir um campo de descritor|[Função SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|Definindo um atributo de ambiente|[Função SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)|  
|Definir um atributo de instrução|[Função SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
