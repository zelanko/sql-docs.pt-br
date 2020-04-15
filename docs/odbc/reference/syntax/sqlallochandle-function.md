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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 178e3fad1ec062dd7f812125da66b7e21a7a4f4b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81290204"
---
# <a name="sqlallochandle-function"></a>Função SQLAllocHandle
**Conformidade**  
 Versão introduzida: ODBC 3.0 Standards Compliance: ISO 92  
  
 **Resumo**  
 **O SQLAllocHandle** aloca um ambiente, conexão, declaração ou alça descritor.  
  
> [!NOTE]  
>  Esta função é uma função genérica para alocar alças que substitui as funções ODBC 2.0 **SQLAllocConnect,** **SQLAllocEnv**e **SQLAllocStmt**. Para permitir que aplicativos chamados **SQLAllocHandle** funcionem com o ODBC 2. *x* drivers, uma chamada para **SQLAllocHandle** é mapeada no Driver Manager para **SQLAllocConnect,** **SQLAllocEnv**ou **SQLAllocStmt**, conforme apropriado. Para obter mais informações, consulte "Comentários". Para obter mais informações sobre o que o Driver Manager mapeia essa função para quando um ODBC 3. *x* aplicativo está trabalhando com um ODBC 2. *x* driver, consulte [Funções de substituição de mapeamento para compatibilidade retrógrada de aplicativos](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLAllocHandle(  
      SQLSMALLINT   HandleType,  
      SQLHANDLE     InputHandle,  
      SQLHANDLE *   OutputHandlePtr);  
```  
  
## <a name="arguments"></a>Argumentos  
 *Handletype*  
 [Entrada] O tipo de alça a ser alocada pelo **SQLAllocHandle**. Deve ser um dos seguintes valores:   
  
-   SQL_HANDLE_DBC  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV  
  
-   SQL_HANDLE_STMT  
  
 SQL_HANDLE_DBC_INFO_TOKEN alça é usada apenas pelo Driver Manager e pelo motorista. Os aplicativos não devem usar este tipo de alça. Para obter mais informações sobre SQL_HANDLE_DBC_INFO_TOKEN, consulte [Developing Connection-Pool Awareness em um Driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md).  
  
 *InputHandle*  
 [Entrada] A alça de entrada em cujo contexto a nova alça deve ser alocada. Se *handleType* é SQL_HANDLE_ENV, este é SQL_NULL_HANDLE. Se *o HandleType* for SQL_HANDLE_DBC, este deve ser um cabo de ambiente e, se for SQL_HANDLE_STMT ou SQL_HANDLE_DESC, deve ser uma alça de conexão.  
  
 *Handleptr de saída*  
 [Saída] Ponteiro para um buffer no qual para retornar a alça para a estrutura de dados recém-alocada.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_INVALID_HANDLE ou SQL_ERROR.  
  
 Ao alocar uma alça diferente de uma alça de ambiente, se **o SQLAllocHandle retornar** SQL_ERROR, ele define *OutputHandlePtr* para SQL_NULL_HDBC, SQL_NULL_HSTMT ou SQL_NULL_HDESC, dependendo do valor do *HandleType,* a menos que o argumento de saída seja um ponteiro nulo. O aplicativo pode então obter informações adicionais da estrutura de dados de diagnóstico associada à alça no argumento *InputHandle.*  
  
## <a name="environment-handle-allocation-errors"></a>Erros de alocação da manipulação do ambiente  
 A alocação do ambiente ocorre tanto dentro do Driver Manager quanto dentro de cada driver. O erro retornado pelo **SQLAllocHandle** com um *HandleType* de SQL_HANDLE_ENV depende do nível em que o erro ocorreu.  
  
 Se o Gerenciador de driver não puder alocar memória para * \*OutputHandlePtr* quando **o SQLAllocHandle** com um *HandleType* de SQL_HANDLE_ENV for chamado, ou o aplicativo fornecer um ponteiro nulo para *OutputHandlePtr*, **SQLAllocHandle** retorna SQL_ERROR. O Gerenciador de driver define **OutputHandlePtr* para SQL_NULL_HENV (a menos que o aplicativo forneça um ponteiro nulo, que retorna SQL_ERROR). Não há alça com a qual associar informações de diagnóstico adicionais.  
  
 O Driver Manager não chama a função de alocação do ambiente de nível de driver até que o aplicativo chame **SQLConnect,** **SQLBrowseConnect**ou **SQLDriverConnect**. Se ocorrer um erro na função **SQLAllocHandle** no nível do driver, a função **SQLConnect,** **SQLBrowseConnect**ou **SQLDriverConnect,** nível do driver, retorna SQL_ERROR. A estrutura de dados de diagnóstico contém SQLSTATE IM004 (falha no **SQLAllocHandle** do driver). O erro é retornado em uma alça de conexão.  
  
 Para obter mais informações sobre o fluxo de chamadas de função entre o Driver Manager e um driver, consulte [SQLConnect Function](../../../odbc/reference/syntax/sqlconnect-function.md).  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **o SQLAllocHandle** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido ligando para **SQLGetDiagRec** com o *HandleType* e *Handle definidos* para o valor de *InputHandle*. SQL_SUCCESS_WITH_INFO (mas não SQL_ERROR) podem ser devolvidas para o argumento *OutputHandle.* A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLAllocHandle** e explica cada um no contexto desta função; a notação "(DM)" precede as descrições de SQLSTATEs devolvidas pelo Driver Manager. O código de devolução associado a cada valor SQLSTATE é SQL_ERROR, a menos que seja observado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informacional específica do motorista. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|08003|Conexão não aberta|(DM) O argumento *HandleType* foi SQL_HANDLE_STMT ou SQL_HANDLE_DESC, mas a conexão especificada pelo argumento *InputHandle* não estava aberta. O processo de conexão deve ser concluído com sucesso (e a conexão deve estar aberta) para que o motorista aloque uma declaração ou alça descritor.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia SQLSTATE específico e para o qual não foi definido sqlSTATE específico para a implementação. A mensagem de erro retornada pelo **SQLGetDiagRec** no buffer **MessageText* descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|(DM) O Driver Manager não pôde alocar memória para a alça especificada.<br /><br /> O driver não conseguiu alocar memória para a alça especificada.|  
|HY009|Uso inválido do ponteiro nulo|(DM) O argumento *OutputHandlePtr* foi um ponteiro nulo.|  
|HY010|Erro de seqüência de função|(DM) O argumento *HandleType* foi SQL_HANDLE_DBC, e **o SQLSetEnvAttr** não foi chamado para definir o SQL_ODBC_VERSION atributo do ambiente.<br /><br /> (DM) Uma função de execução assíncrona foi chamada para o **InputHandle** e ainda estava sendo executada quando a função **SQLAllocHandle** foi chamada com **HandleType** definido para SQL_HANDLE_STMT ou SQL_HANDLE_DESC.|  
|HY013|Erro de gerenciamento de memória|O argumento *HandleType* foi SQL_HANDLE_DBC, SQL_HANDLE_STMT ou SQL_HANDLE_DESC; e a chamada de função não pôde ser processada porque os objetos de memória subjacentes não podiam ser acessados, possivelmente devido às baixas condições de memória.|  
|HY014|Limite no número de alças excedidas|O limite definido pelo driver para o número de alças que podem ser alocadas para o tipo de alça indicado pelo argumento *HandleType* foi atingido.|  
|HY092|Identificador de atributo/opção inválido|(DM) O argumento *HandleType* não era: SQL_HANDLE_ENV, SQL_HANDLE_DBC, SQL_HANDLE_STMT ou SQL_HANDLE_DESC.|  
|HY117|A conexão está suspensa devido ao estado de transação desconhecido. Somente funções desconectadas e somente leitura são permitidas.|(DM) Para obter mais informações sobre o estado suspenso, consulte [a função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Recurso opcional não implementado|O argumento *handleType* foi SQL_HANDLE_DESC e o motorista era um ODBC 2. *x* driver.|  
|HYT01|Tempo de tempo de conexão expirado|O período de tempo de tempo de conexão expirou antes que a fonte de dados respondesse à solicitação. O período de tempo de tempo de conexão é definido através **de SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não suporta esta função|(DM) O argumento *HandleType* foi SQL_HANDLE_STMT, e o motorista não era um driver ODBC válido.<br /><br /> (DM) O argumento *HandleType* foi SQL_HANDLE_DESC, e o driver não suporta a alocação de uma alça de descritor.|  
  
## <a name="comments"></a>Comentários  
 **O SQLAllocHandle** é usado para alocar alças para ambientes, conexões, declarações e descritores, conforme descrito nas seções a seguir. Para obter informações gerais sobre alças, consulte [Handles](../../../odbc/reference/develop-app/handles.md).  
  
 Mais de um ambiente, conexão ou alça de declaração podem ser alocados por um aplicativo por vez se várias alocações forem suportadas pelo driver. No ODBC, nenhum limite é definido sobre o número de alças de ambiente, conexão, declaração ou descritor que podem ser alocadas a qualquer momento. Os motoristas podem impor um limite ao número de um determinado tipo de alça que pode ser alocado por vez; para obter mais informações, consulte a documentação do motorista.  
  
 Se o aplicativo chamar **SQLAllocHandle** com * \*OutputHandlePtr* definido para um ambiente, conexão, declaração ou manipulador de descritor que já existe, o driver sobregrava as informações associadas ao *cabo,* a menos que o aplicativo esteja usando pooling de conexões (consulte "Alocando um atributo de ambiente para pooling de conexão" mais tarde nesta seção). O Gerenciador de driver não verifica se a *alça* inserida no * \*OutputHandlePtr* já está sendo usada, nem verifica o conteúdo anterior de uma alça antes de sobrescrevê-los.  
  
> [!NOTE]  
>  É incorreto a programação do aplicativo ODBC para chamar **SQLAllocHandle** duas vezes com a mesma variável de aplicativo definida para * \*OutputHandlePtr* sem chamar **SQLFreeHandle** para liberar a alça antes de realocá-la. A substituição de alças ODBC de tal maneira pode levar a comportamentos inconsistentes ou erros por parte dos drivers ODBC.  
  
 Em sistemas operacionais que suportam vários segmentos, os aplicativos podem usar o mesmo ambiente, conexão, instrução ou alça descritor em diferentes segmentos. Os motoristas devem, portanto, suportar acesso seguro e multithread a essas informações; uma maneira de conseguir isso, por exemplo, é usando uma seção crítica ou um semáforo. Para obter mais informações sobre threading, consulte [Multithreading](../../../odbc/reference/develop-app/multithreading.md).  
  
 **O SQLAllocHandle** não define o atributo do ambiente SQL_ATTR_ODBC_VERSION quando é chamado para alocar uma alça de ambiente; o atributo do ambiente deve ser definido pelo aplicativo, ou SQLSTATE HY010 (erro de seqüência de função) será devolvido quando **o SQLAllocHandle** for chamado para alocar uma alça de conexão.  
  
 Para aplicativos compatíveis com padrões, **o SQLAllocHandle** é mapeado para **SQLAllocHandleStd** no momento da compilação. A diferença entre essas duas funções é que **o SQLAllocHandleStd** define o SQL_ATTR_ODBC_VERSION atributo do ambiente para SQL_OV_ODBC3 quando é chamado com o argumento *HandleType* definido para SQL_HANDLE_ENV. Isso é feito porque os aplicativos compatíveis com padrões são sempre ODBC 3. *x* aplicações. Além disso, as normas não exigem que a versão do aplicativo seja registrada. Esta é a única diferença entre essas duas funções; caso contrário, eles são idênticos. **SQLAllocHandleStd** é mapeado para **SQLAllocHandle** dentro do gerenciador do driver. Portanto, os drivers de terceiros não têm que implementar **o SQLAllocHandleStd**.  
  
 Os aplicativos ODBC 3.8 devem usar:  
  
-   **SQLAllocHandle e não SQLAllocHandleStd** para alocar uma alça de ambiente.  
  
-   **SQLSetEnvAttr** para definir o atributo do ambiente SQL_ATTR_ODBC_VERSION para SQL_OV_ODBC3_80.  
  
## <a name="allocating-an-environment-handle"></a>Alocando um identificador de ambiente  
 Um cabo de ambiente fornece acesso a informações globais, como alças de conexão válidas e alças ativas de conexão. Para obter informações gerais sobre as alças do ambiente, consulte [Environment Handles](../../../odbc/reference/develop-app/environment-handles.md).  
  
 Para solicitar um cabo de ambiente, um aplicativo chama **SQLAllocHandle** com um *HandleType* de SQL_HANDLE_ENV e um *InputHandle* de SQL_NULL_HANDLE. O driver aloca a memória para as informações do ambiente e passa o valor da alça associada de volta no * \*argumento OutputHandlePtr.* O aplicativo * \** passa o valor OutputHandle em todas as chamadas subseqüentes que requerem um argumento de controle de ambiente. Para obter mais informações, consulte [Alocando a alça do ambiente](../../../odbc/reference/develop-app/allocating-the-environment-handle.md).  
  
 Sob a alça de ambiente do Driver Manager, se já existe uma alça de ambiente do driver, então **o SQLAllocHandle** com um *HandleType* de SQL_HANDLE_ENV não é chamado nesse driver quando uma conexão é feita, apenas **SQLAllocHandle** com um *HandleType* de SQL_HANDLE_DBC. Se a alça do ambiente do driver não existir sob a alça do ambiente do Driver Manager, tanto o SQLAllocHandle com um HandleType de SQL_HANDLE_ENV quanto o SQLAllocHandle com um HandleType de SQL_HANDLE_DBC são chamados no driver quando a primeira alça de conexão do ambiente estiver conectada ao driver.  
  
 Quando o Driver Manager processa a função **SQLAllocHandle** com um *HandleType* de SQL_HANDLE_ENV, ele verifica a palavra-chave **Trace** na seção [ODBC] das informações do sistema. Se estiver definido como 1, o Driver Manager habilita o rastreamento para o aplicativo atual. Se o sinalizador de rastreamento estiver definido, o rastreamento será iniciado quando a primeira alça do ambiente estiver alocada e terminar quando a última alça do ambiente estiver liberada. Para obter mais informações, consulte [Configurando fontes de dados](../../../odbc/reference/install/configuring-data-sources.md).  
  
 Depois de alocar uma alça de ambiente, um aplicativo deve chamar **SQLSetEnvAttr** na alça do ambiente para definir o SQL_ATTR_ODBC_VERSION atributo do ambiente. Se esse atributo não for definido antes **do SQLAllocHandle** ser chamado para alocar uma alça de conexão no ambiente, a chamada para alocar a conexão retornará SQLSTATE HY010 (erro de seqüência de função). Para obter mais informações, consulte [Declarando a versão ODBC do aplicativo](../../../odbc/reference/develop-app/declaring-the-application-s-odbc-version.md).  
  
## <a name="allocating-shared-environments-for-connection-pooling"></a>Alocar ambientes compartilhados para pooling de conexões  
 Ambientes podem ser compartilhados entre vários componentes em um único processo. Um ambiente compartilhado pode ser usado por mais de um componente ao mesmo tempo. Quando um componente usa um ambiente compartilhado, ele pode usar conexões agrupadas, que permitem que ele aloque e use uma conexão existente sem recriar essa conexão.  
  
 Antes de alocar um ambiente compartilhado que possa ser usado para pooling de conexões, um aplicativo deve chamar **sqlsetenvAttr** para definir o atributo do ambiente SQL_ATTR_CONNECTION_POOLING para SQL_CP_ONE_PER_DRIVER ou SQL_CP_ONE_PER_HENV. **SQLSetEnvAttr** neste caso é chamado com *EnvironmentHandle* definido como nulo, o que torna o atributo um atributo de nível de processo.  
  
 Depois que o pool de conexões foi ativado, um aplicativo chama **SQLAllocHandle** com o argumento *HandleType* definido para SQL_HANDLE_ENV. O ambiente alocado por esta chamada será um ambiente compartilhado implícito porque o pool de conexões foi ativado.  
  
 Quando um ambiente compartilhado é alocado, o ambiente que será usado não é determinado até que **o SQLAllocHandle** com um *HandleType* de SQL_HANDLE_DBC seja chamado. Nesse ponto, o Driver Manager tenta encontrar um ambiente existente que corresponda aos atributos de ambiente solicitados pelo aplicativo. Se esse ambiente não existe, um deles é criado como um ambiente compartilhado. O Driver Manager mantém uma contagem de referência para cada ambiente compartilhado; a contagem é definida como 1 quando o ambiente é criado pela primeira vez. Se um ambiente correspondente for encontrado, a alça desse ambiente é devolvida ao aplicativo e a contagem de referência é incrementada. Um manuseamento de ambiente alocado dessa maneira pode ser usado em qualquer função ODBC que aceite uma alça de ambiente como argumento de entrada.  
  
## <a name="allocating-a-connection-handle"></a>Alocando um identificador de conexão  
 Uma alça de conexão fornece acesso a informações como a declaração válida e as alças do descritor sobre a conexão e se uma transação está aberta no momento. Para obter informações gerais sobre as alças de conexão, consulte [Alças de conexão](../../../odbc/reference/develop-app/connection-handles.md).  
  
 Para solicitar uma alça de conexão, um aplicativo chama **SQLAllocHandle** com um *HandleType* de SQL_HANDLE_DBC. O argumento *InputHandle* é definido para o cabo de ambiente que foi retornado pela chamada para **SQLAllocHandle** que alocou essa alça. O driver aloca a memória para as informações de conexão e passa o valor da alça associada de volta no * \*OutputHandlePtr*. O aplicativo passa o * \*valor OutputHandlePtr* em todas as chamadas subseqüentes que requerem uma alça de conexão. Para obter mais informações, consulte [Alocando uma alça de conexão .](../../../odbc/reference/develop-app/allocating-a-connection-handle-odbc.md)  
  
 O Driver Manager processa a função **SQLAllocHandle** e chama a função **SQLAllocHandle** do driver quando o aplicativo chama **SQLConnect,** **SQLBrowseConnect**ou **SQLDriverConnect**. (Para obter mais informações, consulte [SQLConnect Function](../../../odbc/reference/syntax/sqlconnect-function.md).)  
  
 Se o atributo do ambiente SQL_ATTR_ODBC_VERSION não for definido antes **do SQLAllocHandle** ser chamado para alocar uma alça de conexão no ambiente, a chamada para alocar a conexão retornará SQLSTATE HY010 (erro de seqüência de função).  
  
 Quando um aplicativo chama **o SQLAllocHandle** com o argumento *InputHandle* definido como SQL_HANDLE_DBC e também definido como um cabo de ambiente compartilhado, o Gerenciador de drivertenta tenta encontrar um ambiente compartilhado existente que corresponda aos atributos de ambiente definidos pelo aplicativo. Se esse ambiente não existir, um deles é criado, com uma contagem de referência (mantida pelo Driver Manager) de 1. Se um ambiente compartilhado correspondente for encontrado, essa alça será devolvida ao aplicativo e sua contagem de referência será incrementada.  
  
 A conexão real que será usada não é determinada pelo Driver Manager até que **o SQLConnect** ou **o SQLDriverConnect** sejam chamados. O Driver Manager usa as opções de conexão na chamada para **SQLConnect** (ou as palavras-chave de conexão na chamada para **SQLDriverConnect**) e os atributos de conexão definidos após a alocação da conexão para determinar qual conexão no pool deve ser usada. Para obter mais informações, consulte [SQLConnect Function](../../../odbc/reference/syntax/sqlconnect-function.md).  
  
## <a name="allocating-a-statement-handle"></a>Alocando um identificador de instrução  
 Uma alça de declaração fornece acesso a informações de declaração, como mensagens de erro, o nome do cursor e informações de status para o processamento da declaração SQL. Para obter informações gerais sobre as alças de declaração, consulte ['Alças de declaração'](../../../odbc/reference/develop-app/statement-handles.md)  
  
 Para solicitar uma alça de declaração, um aplicativo se conecta a uma fonte de dados e, em seguida, chama **sqlAllocHandle** antes de enviar instruções SQL. Nesta chamada, *handleType* deve ser definido como SQL_HANDLE_STMT e *InputHandle* deve ser definido para o cabo de conexão que foi retornado pela chamada para **SQLAllocHandle** que alocou essa alça. O driver aloca a memória para as informações da declaração, associa a alça da declaração com a conexão especificada e passa o valor da alça associada de volta no * \*OutputHandlePtr*. O aplicativo passa o * \*valor OutputHandlePtr* em todas as chamadas subseqüentes que requerem uma alça de declaração. Para obter mais informações, consulte [Alocando uma alça de declaração](../../../odbc/reference/develop-app/allocating-a-statement-handle-odbc.md).  
  
 Quando a alça da declaração é alocada, o driver aloca automaticamente um conjunto de quatro descritores e atribui as alças desses descritores aos atributos de declaração SQL_ATTR_APP_ROW_DESC, SQL_ATTR_APP_PARAM_DESC, SQL_ATTR_IMP_ROW_DESC e SQL_ATTR_IMP_PARAM_DESC. Estes são referidos como descritores *implicitamente* alocados. Para alocar explicitamente um descritor de aplicativo, consulte a seção a seguir: "Alocando uma alça de descritor".  
  
## <a name="allocating-a-descriptor-handle"></a>Alocando uma alça do descritor  
 Quando um aplicativo chama **SQLAllocHandle** com um *HandleType* de SQL_HANDLE_DESC, o driver aloca um descritor de aplicativo. Estes são referidos como descritores *explicitamente* alocados. O aplicativo orienta um motorista a usar um descritor de aplicativo explicitamente alocado em vez de um alocado automaticamente para uma alça de declaração dada, chamando a função **SQLSetStmtAttr** com o atributo SQL_ATTR_APP_ROW_DESC ou SQL_ATTR_APP_PARAM_DESC. Um descritor de implementação não pode ser alocado explicitamente, nem um descritor de implementação pode ser especificado em uma chamada de função **SQLSetStmtAttr.**  
  
 Descritores alocados explicitamente estão associados a uma alça de conexão em vez de uma alça de instrução (como os descritores alocados automaticamente são). Os descritores permanecem alocados somente quando um aplicativo está realmente conectado ao banco de dados. Como os descritores explicitamente alocados estão associados a uma alça de conexão, um aplicativo pode associar um descritor explicitamente alocado com mais de uma instrução dentro de uma conexão. Um descritor de aplicativo implicitamente alocado, por outro lado, não pode ser associado a mais de uma alça de declaração. (Não pode ser associado a qualquer alça de declaração que não seja a que foi alocada.) As alças de descritor explicitamente alocadas podem ser liberadas explicitamente pelo aplicativo ou ligando para **SQLFreeHandle** com um *HandleType* de SQL_HANDLE_DESC ou implicitamente quando a conexão estiver fechada.  
  
 Quando o descritor explicitamente alocado é liberado, o descritor implicitamente alocado é novamente associado à instrução. (O atributo SQL_ATTR_APP_ROW_DESC ou SQL_ATTR_APP_PARAM_DESC para essa afirmação é novamente definido para a alça descritor implicitamente alocada.) Isso é verdade para todas as declarações que foram associadas ao descritor explicitamente alocado na conexão.  
  
 Para obter mais informações sobre descritores, consulte [Descritores](../../../odbc/reference/develop-app/descriptors.md).  
  
## <a name="code-example"></a>Exemplo de código  
 Consulte [O Programa Amostra ODBC,](../../../odbc/reference/sample-odbc-program.md)Função [SQLBrowseConnect,](../../../odbc/reference/syntax/sqlbrowseconnect-function.md) [Função SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)e [Função SQLSetCursorName](../../../odbc/reference/syntax/sqlsetcursorname-function.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Executando uma declaração SQL|[Função SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Executando uma declaração SQL preparada|[Função SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Liberando um ambiente, conexão, declaração ou alça descritor|[Função SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|Preparando uma declaração para execução|[Função SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|  
|Definindo um atributo de conexão|[Função SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|Definindo um campo descritor|[Função SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|Definindo um atributo de ambiente|[Função SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)|  
|Definindo um atributo de declaração|[Função SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API oDBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
