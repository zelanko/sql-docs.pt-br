---
title: ssbdiagnose (Service Broker) do utilitário | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- Service Broker, runtime reports
- Service Broker, command prompt utilities
- troubleshooting [Service Broker], conversations
- troubleshooting [Service Broker], configurations
- command prompt utilities [Service Broker]
- Service Broker, troubleshooting
- Service Broker, configuration reports
- Service Broker, tools
- troubleshooting [Service Broker], runtime
- conversations [Service Broker], troubleshooting
- troubleshooting [Service Broker], ssbdiagnose utility
- tools [Service Broker], ssbdiagnose
- Service Broker, ssbdiagnose utility
- ssbdiagnose
ms.assetid: 0c1636e8-a3db-438e-be4c-1ea40d1f4877
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0c9d0d1885413e5931f495c6eb5cd711bc0a9106
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48111166"
---
# <a name="ssbdiagnose-utility-service-broker"></a>Utilitário ssbdiagnose (Service Broker)
  O utilitário **ssbdiagnose** relata problemas em conversas do [!INCLUDE[ssSB](../../includes/sssb-md.md)] ou na configuração de serviços do [!INCLUDE[ssSB](../../includes/sssb-md.md)] . É possível fazer verificações de configuração para dois serviços ou um único serviço. Os problemas são reportados na janela de prompt de comando como texto legível ou XML formatado que pode ser redirecionado para um arquivo ou outro programa.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
      ssbdiagnose   
[ [ -XML ]  
    [ -LEVEL { ERROR | WARNING | INFO } ]  
  [-IGNOREerror_id ] [ ...n]  
    [ <baseconnectionoptions> ]  
  { <configurationreport> | <runtimereport> }  
]  
| -?  
  
<configurationreport> ::=  
    CONFIGURATION  
  { [ FROM SERVICEservice_name  
      [ <fromconnectionoptions> ]  
      [ MIRROR <mirrorconnectionoptions> ]  
    ]  
    [ TO SERVICEservice_name[, broker_id ]  
      [ <toconnectionoptions> ]  
      [ MIRROR <mirrorconnectionoptions> ]  
    ]  
  }  
    ON CONTRACTcontract_name  
  [ ENCRYPTION { ON | OFF | ANONYMOUS } ]  
  
<runtime_report> ::=  
    RUNTIME  
    [-SHOWEVENTS ]  
        [ -NEW  
         [ -ID { conversation_handle  
                | conversation_group_id  
                 | conversation_id  
                  }  
        ] [ ...n]  
        ]  
    [ -TIMEOUTtimeout_interval ]  
    [ <runtimeconnectionoptions> ]  
  
<baseconnectionoptions> ::=  
  <connectionoptions>  
  
<fromconnectionoptions> ::=  
  <connectionoptions>  
  
<toconnectionoptions> ::=  
  <connectionoptions>  
  
<mirrorconnectionoptions> ::=  
  <connectionoptions>  
  
<runtimeconnectionoptions> ::=  
  [ CONNECT TO <connectionoptions> ] [ ...n]  
  
<connectionoptions> ::=  
    [ –E | { -Ulogin_id [ -Ppassword ] } ]  
  [ -Sserver_name[\instance_name] ]  
  [ -ddatabase_name ]  
  [ -llogin_timeout ]  
  
```  
  
## <a name="command-line-options"></a>Opções da linha de comando  
 **-XML**  
 Especifica que a saída de **ssbdiagnose** será gerada como XML formatado. Essa saída pode ser redirecionado para um arquivo ou outro aplicativo. Se **-XML** não for especificado, a saída de **ssbdiagnose** será formatada como texto legível.  
  
 **-LEVEL** { **ERROR** | **WARNING** | **INFO**}  
 Especifica o nível das mensagens a serem reportadas.  
  
 **ERRO**: relata apenas mensagens de erro.  
  
 **AVISO**: relata mensagens de erro e de aviso.  
  
 **INFORMAÇÃO**: relata mensagens de erro, aviso e informações.  
  
 A configuração padrão é **AVISO**.  
  
 **-IGNORE** *error_id*  
 Especifica que os erros ou as mensagens com a *error_id* especificada não serão incluídos em relatórios. Você pode especificar **-IGNORE** várias vezes para suprimir IDs de mensagens múltiplas.  
  
 **\<baseconnectionoptions >**  
 Especifica as informações de conexão base usadas por **ssbdiagnose** quando opções de conexão não estão incluídas em uma cláusula específica. A informações de conexão atribuídas em uma cláusula específica substituem as informações de **baseconnectionoption** . Essa operação é executada separadamente para cada parâmetro. Por exemplo, se **-S** e **-d** estiverem especificados no **baseconnetionoptions**, e somente **-d** estiver especificado no **toconnetionoptions**, o **ssbdiagnose** usará -S do **baseconnetionoptions** e -d do **toconnetionoptions**.  
  
 **CONFIGURATION**  
 Solicita um relatório de erros de configuração entre um par de serviços [!INCLUDE[ssSB](../../includes/sssb-md.md)] ou para um único serviço.  
  
 **FROM SERVICE** *service_name*  
 Especifica o serviço que inicia as conversas.  
  
 **\<fromconnectionoptions >**  
 Especifica as informações necessárias para se conectar ao banco de dados que contém o serviço iniciador. Se **fromconnectionoptions** não for especificado, o **ssbdiagnose** usará as informações de conexão de **baseconnectionoptions** para se conectar ao banco de dados do iniciador. Se **fromconnectionoptions** for especificado, essa opção deverá incluir o banco de dados que contém o serviço iniciador. Se **fromconnectionoptions** não for especificado, o **baseconnectionoptions** deverá especificar o banco de dados do iniciador.  
  
 **TO SERVICE** *service_name*[, *broker_id* ]  
 Especifica o serviço que é o destino das conversas.  
  
 *service_name*: especifica o nome do serviço de destino.  
  
 *broker_id*: especifica a ID do [!INCLUDE[ssSB](../../includes/sssb-md.md)] que identifica o banco de dados de destino. *broker_id* é um GUID. Você pode executar a seguinte consulta no banco de dados destino para encontrar esse item:  
  
```  
SELECT service_broker_guid  
FROM sys.databases  
WHERE database_id = DB_ID();  
```  
  
 **\<toconnectionoptions >**  
 Especifica as informações necessárias para se conectar ao banco de dados que contém o serviço de destino. Se **toconnectionoptions** não for especificado, o **ssbdiagnose** usará as informações de conexão de **baseconnectionoptions** para se conectar ao banco de dados de destino.  
  
 **MIRROR**  
 Especifica que o serviço [!INCLUDE[ssSB](../../includes/sssb-md.md)] associado é hospedado em um banco de dados espelhado. **ssbdiagnose** verifica se a rota para o serviço é uma rota espelhada, em que MIRROR_ADDRESS foi especificado em CREATE ROUTE.  
  
 **\<mirrorconnectionoptions>**  
 Especifica as informações necessárias para se conectar ao banco de dados espelho. Se **mirrorconnectionoptions** não for especificado, o **ssbdiagnose** usará as informações de conexão de **baseconnectionoptions** para se conectar ao banco de dados de espelho.  
  
 **ON CONTRACT** *contract_name*  
 Solicita que **ssbdiagnose** verifique apenas as configurações que usam o contrato especificado. Se ON CONTRACT não for especificado, **ssbdiagnose** relatará o contrato denominado DEFAULT.  
  
 **ENCRYPTION** { **ON** | **OFF** | **ANONYMOUS** }  
 Solicita verificação se o diálogo está configurado corretamente para o nível especificado de criptografia:  
  
 **ON**: sem configuração padrão. A segurança de diálogo total está configurada. Certificados foram implantados nos dois lados do diálogo, uma associação de serviço remoto está presente e a instrução GRANT SEND do serviço de destino especificou o usuário iniciador.  
  
 **OFF**: nenhuma segurança de diálogo está configurada. Nenhum certificado foi implantado, nenhuma associação de serviço remoto foi criada e a instrução GRANT SEND do serviço iniciador especificou a função **public** .  
  
 **ANONYMOUS**: a segurança de diálogo anônima está configurada. Um certificado foi implantado, a associação de serviço remoto especificou a cláusula anônima e a instrução GRANT SEND do serviço de destino especificou a função **public** .  
  
 **RUNTIME**  
 Solicita um relatório de problemas que causam erros de tempo de execução para uma conversa do [!INCLUDE[ssSB](../../includes/sssb-md.md)] . Se nem **-NEW** ou **-ID** forem especificadas, o **ssbdiagnose** monitorará todas as conversas em todos os bancos de dados especificados nas opções de conexão. Se **-NEW** ou **-ID** forem especificadas, o **ssbdiagnose** criará uma lista de IDs especificadas nos parâmetros.  
  
 Durante a execução de **ssbdiagnose** , todos os eventos do [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] que indicam erros em tempo de execução são registrados. Registra os eventos que ocorrem para as ID especificadas, além de eventos de nível de sistema. Se forem encontrados erros em tempo de execução, **ssbdiagnose** executará um relatório de configuração sobre a configuração associada.  
  
 Por padrão, os erros em tempo de execução não são incluídos no relatório de saída, somente os resultados da análise de configuração. Use **-SHOWEVENTS** para que os erros em tempo de execução sejam incluídos no relatório.  
  
 **-SHOWEVENTS**  
 Especifica que **ssbdiagnose** relata eventos do [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] durante um relatório RUNTIME. Somente eventos considerados condições de erro são reportados. Por padrão, **ssbdiagnose** monitora apenas eventos de erro; não os relata na saída.  
  
 **-NEW**  
 Solicita o monitoramento no tempo de execução da primeira conversa iniciada após o começo da execução de **ssbdiagnose** .  
  
 **-ID**  
 Solicita o monitoramento de tempo de execução dos elementos de conversa especificados. Você pode especificar **-ID** várias vezes.  
  
 Se você especificar um identificador de conversa, somente os eventos associados ao ponto de extremidade da conversa associada serão reportados. Se você especificar uma ID de conversa, todos os eventos dessa conversa e seus pontos de extremidade iniciador e de destino serão reportados. Se uma ID de grupo de conversa for especificada, todos os eventos de todas as conversas e pontos de extremidade no grupo de conversa serão reportados.  
  
 *conversation_handle*  
 Um identificador exclusivo que identifica um ponto de extremidade de conversa em um aplicativo. Os identificadores de conversa são exclusivos para um ponto de extremidade de uma conversa; os pontos de extremidade iniciador e de destino têm identificadores de conversa separados.  
  
 Identificadores de conversa são retornados aos aplicativos pelo *@dialog_handle* parâmetro do **BEGIN DIALOG** instrução e o `conversation_handle` conjunto de coluna no resultado de uma **RECEIVE**  instrução.  
  
 Identificadores de conversa são relatados na `conversation_handle` coluna do **transmission_queue** e **sys. conversation_endpoints** exibições do catálogo.  
  
 *conversation_group_id*  
 O identificador exclusivo que identifica um grupo de conversa.  
  
 Identificadores de grupo conversa são retornados aos aplicativos pelo *@conversation_group_id* parâmetro do **GET CONVERSATION GROUP** instrução e o `conversation_group_id` coluna no conjunto de resultados de uma **RECEIVE** instrução.  
  
 Identificadores de grupo conversa são relatados na `conversation_group_id` colunas do **sys. conversation_groups** e **sys. conversation_endpoints** exibições do catálogo.  
  
 *conversation_id*  
 O identificador exclusivo que identifica uma conversa. As IDs de conversa são iguais para os pontos de extremidade iniciador e de destino de uma conversa.  
  
 Identificadores de conversa são relatados na `conversation_id` coluna do **sys. conversation_endpoints** exibição do catálogo.  
  
 **-TIMEOUT** *timeout_interval*  
 Especifica o número de segundos para a execução de um relatório **RUNTIME** . Se **-TIMEOUT** não for especificado, o relatório de tempo de execução será executado indefinidamente. **-TIMEOUT** é usado somente em relatórios de **RUNTIME** , não relatórios de **CONFIGURATION** . Use ctrl + C para sair de **ssbdiagnose** if **-TIMEOUT** não foi especificado ou para encerrar um relatório de tempo de execução antes de o intervalo**-** limite expirar. *timeout_interval* deve ser um número entre 1 e 2.147.483.647.  
  
 **\<runtimeconnectionoptions>**  
 Especifica as informações de conexão para os bancos de dados que contêm os serviços associados aos elementos de conversa sendo monitorados. Se todos os serviços estiverem no mesmo banco de dados, você terá de especificar apenas uma cláusula **CONNECT TO** . Se os serviços estiverem em bancos de dados separados, você deverá fornecer uma cláusula **CONNECT TO** para cada banco de dados. Se **runtimeconnectionoptions** não for especificado, **ssbdiagnose** usará as informações de conexão de **baseconnectionoptions**.  
  
 **–E**  
 Abra uma conexão de Autenticação do Windows com uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] usando sua conta atual do Windows como ID de logon. O logon deve ser membro da função de servidor fixa **sysadmin** .  
  
 A opção -E ignora as configurações de usuário e senha das variáveis de ambiente SQLCMDUSER e SQLCMDPASSWORD.  
  
 Se **-E** ou **-U** não for especificado, **ssbdiagnose** usará o valor da variável de ambiente SQLCMDUSER. Se SQLCMDUSER também não for definido, **ssbdiagnose** usará a Autenticação do Windows.  
  
 Se a opção **-E** for usada com as opções **-U** ou **-P**, uma mensagem de erro será gerada.  
  
 **-U** *login_id*  
 Abra uma conexão de Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando a ID de logon especificada. O logon deve ser membro da função de servidor fixa **sysadmin**.  
  
 Se **-E** ou **-U** não for especificado, **ssbdiagnose** usará o valor da variável de ambiente SQLCMDUSER. Se SQLCMDUSER também não for definido, **ssbdiagnose** tentará se conectar usando o modo de Autenticação do Windows com base na conta do Windows do usuário que está executando **ssbdiagnose**.  
  
 Se a opção **-U** for usada junto com **-E** , uma mensagem de erro será gerada. Será gerada uma mensagem de erro e o programa será encerrado se a opção **–U** for seguida por mais de um argumento.  
  
 **-P** *password*  
 Especifica a senha para a ID de logon **-U** . Senhas diferenciam maiúsculas e minúsculas. Se a opção **-U** for usada e **-P** não, **ssbdiagnose** usará o valor da variável de ambiente SQLCMDPASSWORD. Se SQLCMDPASSWORD também não for definido, **ssbdiagnose** solicitará uma senha ao usuário.  
  
> [!IMPORTANT]  
>  Quando você digitar um comando SET SQLCMDPASSWORD, sua senha ficará visível para qualquer pessoa que possa ver seu monitor.  
  
 Se a opção **-P** for especificada sem uma senha, **ssbdiagnose** usará o valor padrão (NULL).  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)] Para obter mais informações, confira [Senhas fortes](../../relational-databases/security/strong-passwords.md).  
  
 O prompt de senha é exibido imprimindo-se o prompt de senha no console, como a seguir: `Password:`  
  
 A entrada do usuário está oculta. Isso significa que nada é exibido e o cursor fica em posição.  
  
 Será gerada uma mensagem de erro se a opção **-P** for usada com a opção **-E**.  
  
 Se a opção **-P** for seguida por mais de um argumento, uma mensagem de erro será gerada.  
  
 **-S** *server_name*[\\*instance_name*]  
 Especifica a instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] que contém os serviços do [!INCLUDE[ssSB](../../includes/sssb-md.md)] a serem analisados.  
  
 Especifica *server_name* para conexão com a instância padrão do [!INCLUDE[ssDE](../../includes/ssde-md.md)] naquele servidor. Especifique *server_name***\\***instance_name* para conectar-se a uma instância nomeada do [!INCLUDE[ssDE](../../includes/ssde-md.md)] nesse servidor. Se **-S** não for especificado, **ssbdiagnose** usará o valor da variável de ambiente SQLCMDSERVER. Se SQLCMDSERVER também não for definido, **ssbdiagnose** se conectará à instância padrão do [!INCLUDE[ssDE](../../includes/ssde-md.md)] no computador local.  
  
 **-d** *database_name*  
 Especifica o banco de dados que contém os serviços do [!INCLUDE[ssSB](../../includes/sssb-md.md)] a serem analisados. Se o banco de dados não existir, uma mensagem de erro será gerada. Se **-d** não for especificado, o padrão será o banco de dados especificado na propriedade default-database para o seu logon.  
  
 **-l** *login_timeout*  
 Especifica o número de segundos que devem decorrer antes que o tempo limite de uma tentativa de conexão com um servidor seja alcançada. Se **-l** não for especificado, **ssbdiagnose** usará o valor definido para a variável de ambiente SQLCMDLOGINTIMEOUT. Se SQLCMDLOGINTIMEOUT também não for definida, o tempo limite padrão será de trinta segundos. O tempo limite do logon deve ser um número entre 0 e 65534. Se o valor fornecido não for numérico ou não estiver nesse intervalo, **ssbdiagnose** vai gerar uma mensagem de erro. Um valor de 0 especifica o tempo limite como infinito.  
  
 **-?**  
 Exibe a ajuda de linha de comando.  
  
## <a name="remarks"></a>Comentários  
 Use **ssbdiagnose** para fazer o seguinte:  
  
-   Confirmar que não há erros de configuração em um aplicativo [!INCLUDE[ssSB](../../includes/sssb-md.md)] recém-configurado.  
  
-   Confirmar que não há erros de configuração depois que você alterar a configuração de um aplicativo [!INCLUDE[ssSB](../../includes/sssb-md.md)] existente.  
  
-   Confirmar que não há erros de configuração após a desanexação de um banco de dados [!INCLUDE[ssSB](../../includes/sssb-md.md)] nova anexação a uma nova instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
-   Pesquise se há erros de configuração quando mensagens de erro não são transmitidas com êxito entre serviços.  
  
-   Obtenha um relatório de quaisquer erros que ocorram em um conjunto de elementos de conversa de [!INCLUDE[ssSB](../../includes/sssb-md.md)] .  
  
## <a name="configuration-reporting"></a>Relatório de configuração  
 Para analisar corretamente a configuração usada por uma conversa, execute um relatório de configuração **ssbdiagnose** que use as mesmas opções utilizadas pela conversa. Se você especificar um nível mais baixo de opções para **ssbdiagnose** do que o utilizado pela conversa, **ssbdiagnose** talvez não reporte as condições necessárias para a conversa. Se você especificar um nível mais alto de opções para **ssbdiagnose**, talvez o utilitário reporte itens desnecessários para a conversa. Por exemplo, uma conversa entre dois serviços no mesmo banco de dados pode ser executada com ENCPRYPTION OFF. Se você executar **ssbdiagnose** para validar a configuração entre os dois serviços, mas utilizar a configuração ENCRYPTION ON padrão, **ssbdiagnose** relatará que uma chave mestra está faltando no banco de dados. Uma chave mestra não é necessária para a conversa.  
  
 O relatório de configuração **ssbdiagnose** analisa apenas um serviço do [!INCLUDE[ssSB](../../includes/sssb-md.md)] ou um único par de serviços cada vez que é executado. Para obter relatórios sobre vários pares de serviços do [!INCLUDE[ssSB](../../includes/sssb-md.md)] , crie um arquivo de comando .cmd que chame **ssbdiagnose** várias vezes.  
  
## <a name="runtime-reporting"></a>Relatório de tempo de execução  
 Quando -RUNTIME é especificado, o **ssbdiagnose** procura todos os bancos de dados especificados no **runtimeconnectionoptions** e no **baseconnectionoptions** para criar uma lista de IDs do [!INCLUDE[ssSB](../../includes/sssb-md.md)] . A lista completa de IDs criada depende dos itens especificados para - NEW e - ID:  
  
-   Se **-NEW** ou **-ID** não for especificado, a lista conterá todas as conversas de todos os bancos de dados especificados nas opções de conexão.  
  
-   Se **-NEW** for especificado, **ssbdiagnose** incluirá os elementos da primeira conversa iniciada após a execução de **ssbdiagnose** . Isso inclui a ID e os identificadores de conversa dos pontos de extremidade de destino e iniciador da conversa.  
  
-   Se **-ID** for especificado com um identificador de conversa, somente esse identificador será incluído na lista.  
  
-   Se **-ID** for especificado com uma ID de conversa, essa ID e os identificadores dos dois pontos de extremidade da conversa serão adicionados à lista.  
  
-   Se **-ID** for especificado com uma ID de grupo de conversa, todas as IDs e identificadores de conversa nesse grupo serão adicionados à lista.  
  
 A lista não inclui elementos de bancos de dados que não são cobertos pelas opções de conexão. Por exemplo, suponhamos que você use **-ID** para especificar uma ID de conversa, mas forneça somente uma cláusula **runtimeconnectionoptions** para o banco de dados iniciador e não para o banco de dados de destino. **ssbdiagnose** não incluirá o identificador de conversa de destino em sua lista de IDs, somente a ID da conversa e o identificador da conversa do iniciador.  
  
 O**ssbdiagnose** monitora os eventos de [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] dos bancos de dados cobertos por **runtimeconnectionoptions** e **baseconnectionoptions**. Ele procura eventos do [!INCLUDE[ssSB](../../includes/sssb-md.md)] que indicam que um erro foi encontrado por um ou mais IDs do [!INCLUDE[ssSB](../../includes/sssb-md.md)] na lista de tempo de execução. O**ssbdiagnose** também procura eventos de erro do [!INCLUDE[ssSB](../../includes/sssb-md.md)] no nível do sistema não especificamente associados a nenhum grupo de conversa.  
  
 Se **ssbdiagnose** localizar erros na conversa, o utilitário relatar a causa raiz dos eventos executando também um relatório de configuração. **ssbdiagnose** usa os metadados dos bancos de dados para tentar determinar as instâncias, as IDs do [!INCLUDE[ssSB](../../includes/sssb-md.md)] , os bancos de dados, os serviços e os contratos usados pela conversa. Em seguida, executa um relatório de configuração que usa todas as informações disponíveis.  
  
 Por padrão, **ssbdiagnose** não relata eventos de erro. O utilitário só reporta os problemas subjacentes encontrados durante a verificação de configuração. Isso minimiza a quantidade de informações reportadas e lhe ajuda a enfatizar os problemas de configuração subjacentes. Você pode especificar **-SHOWEVENTS** para ver os eventos de erro encontrados por **ssbdiagnose**.  
  
## <a name="issues-reported-by-ssbdiagnose"></a>Problemas reportados por ssbdiagnose  
 **ssbdiagnose** relata três classes de problemas. No arquivo de saída XML, cada classe de problema é reportada como um tipo separado de elemento Issue. Os três tipos de problemas relatados por **ssbdiagnose** são os seguintes:  
  
 **Diagnóstico**  
 Reporta um problema de configuração. Isso inclui os problemas encontrados durante a execução de relatório **CONFIGURATION** ou na fase de configuração de um relatório **RUNTIME** . **ssbdiagnose** relata cada problema de configuração uma vez.  
  
 **Evento**  
 Relata um evento [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] que indica que um problema foi encontrado por uma conversa monitorada durante um relatório **RUNTIME** . **ssbdiagnose** relata eventos toda vez que eles são gerados. Os eventos poderão ser reportados várias vezes se várias conversas encontrarem o problema.  
  
 **Problema**  
 Relata um problema que está impedindo o **ssbdiagnose** de concluir uma análise de configuração ou de monitorar conversas.  
  
## <a name="sqlcmd-environment-variables"></a>Variáveis de ambiente sqlcmd  
 O utilitário **ssbdiagnose** dá suporte às variáveis de ambiente SQLCMDSERVER, SQLCMDUSER, SQLCMDPASSWORD e SQLCMDLOGINTIMOUT que também são usadas pelo utilitário **sqlcmd** . Você pode definir as variáveis de ambiente usando o comando SET de prompt de comando ou o comando **setvar** em scripts [!INCLUDE[tsql](../../includes/tsql-md.md)] que executa com o uso de **sqlcmd**. Para obter mais informações sobre como usar **setvar** no **sqlcmd**, veja [Usar sqlcmd com variáveis de script](../../relational-databases/scripting/sqlcmd-use-with-scripting-variables.md).  
  
## <a name="permissions"></a>Permissões  
 Em cada cláusula **connectionoptions** , o logon especificado com **-E** ou **-U** deve ser membro da função de servidor fixa **sysadmin** na instância especificada em **-S**.  
  
## <a name="examples"></a>Exemplos  
 Esta seção contém exemplos do uso de **ssbdiagnose** em um prompt de comando.  
  
### <a name="a-checking-the-configuration-of-two-services-in-the-same-database"></a>A. Verificando a configuração de dois serviços no mesmo banco de dados  
 O exemplo a seguir mostra como solicitar um relatório de configuração quando estas condições são verdadeiras:  
  
-   Os serviços iniciador e de destino estão no mesmo banco de dados.  
  
-   O banco de dados está na instância padrão do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
-   As instâncias estão no mesmo computador em que **ssbdiagnose** é executado.  
  
 O utilitário **ssbdiagnose** relata a configuração que usa o contrato DEFAULT porque ON CONTRACT não foi especificado.  
  
```  
ssbdiagnose -E -d MyDatabase CONFIGURATION FROM SERVICE /test/initiator TO SERVICE /test/target  
```  
  
### <a name="b-checking-the-configuration-of-two-services-on-separate-computers-that-use-one-login"></a>B. Verificando a configuração de dois serviços em computadores separados que não usam logon  
 O exemplo a seguir mostra como solicitar um relatório de configuração quando os serviços iniciador e de destino estão em computadores separados, mas podem ser acessados com o uso do mesmo logon de Autenticação do Windows.  
  
```  
ssbdiagnose -E CONFIGURATION FROM SERVICE /text/initiator -S InitiatorComputer -d InitiatorDatabase TO SERVICE /test/target -S TargetComputer -d TargetDatabase ON CONTRACT TestContract  
```  
  
### <a name="c-checking-the-configuration-of-two-services-on-separate-computers-that-use-separate-logins"></a>C. Verificando a configuração de dois serviços em computadores separados que usam logons diferentes  
 O exemplo a seguir mostra como solicitar um relatório de configuração quando os serviços iniciador e de destino estão em computadores separados, e logons de Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] diferentes são necessários para cada instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
```  
ssbdiagnose CONFIGURATION FROM SERVICE /text/initiator   
-S InitiatorComputer -U InitiatorLogin -p !wEx23Dvb   
-d InitiatorDatabase TO SERVICE /test/target -S TargetComputer   
-U TargetLogin -p ER!49jiy -d TargetDatabase ON CONTRACT TestContract  
```  
  
### <a name="d-checking-mirrored-service-configurations-on-separate-computers-with-anonymous-encryption"></a>D. Verificando configurações de serviços espelhados em computadores separados com criptografia anônima  
 O exemplo a seguir mostra como solicitar um relatório de configuração quando os serviços iniciador e de destino estão em computadores separados e o iniciador é espelhado para uma instância nomeada. O relatório também verifica se os serviços estão configurados para usar criptografia anônima.  
  
```  
ssbdiagnose -E CONFIGURATION FROM SERVICE /text/initiator   
-S InitiatorComputer -d InitiatorDatabase MIRROR   
-S MirrorComputer/MirrorInstance TO SERVICE /test/target   
-S TargetComputer -d TargetDatabase ON CONTRACT TestContract ENCRYPTION ANONYMOUS  
```  
  
### <a name="e-checking-the-configuration-of-two-contracts"></a>E. Verificando a configuração de dois contratos  
 O exemplo a seguir mostra como criar um arquivo de comando que solicite relatórios de configuração quando estas condições forem verdadeiras:  
  
-   Os serviços iniciador e de destino estão no mesmo banco de dados.  
  
-   O banco de dados está na instância padrão do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
-   A instância está no mesmo computador em que **ssbdiagnose** é executado.  
  
 Cada vez que **ssbdiagnose** é executado, o utilitário relata a configuração de um contrato diferente entre os mesmos serviços.  
  
```  
ssbdiagnose -E -d MyDatabase CONFIGURATION FROM SERVICE   
/test/initiator TO SERVICE /test/target ON CONTRACT PayRaiseContract  
ssbdiagnose -E -d MyDatabase CONFIGURATION FROM SERVICE /test/initiator   
TO SERVICE /test/target ON CONTRACT PromotionContract  
```  
  
### <a name="f-monitor-the-status-of-a-specific-conversation-on-the-local-computer-with-a-time-out"></a>F. Monitorar o status de uma conversa específica no computador local com um tempo limite  
 O exemplo a seguir mostra como monitorar uma conversa específica em que os serviços iniciador e de destino estão no mesmo banco de dados na instância padrão do mesmo computador que está executando **ssbdiagnose**. O intervalo de tempo limite é definido como 20 segundos.  
  
```  
ssbdiagnose -E -d TestDatabase RUNTIME -ID D68D77A9-B1CF-41BF-A5CE-279ABCAB140D -TIMEOUT 20  
```  
  
### <a name="g-monitor-the-status-of-a-conversation-that-spans-two-computers"></a>G. Monitorar o status de uma conversa que abrange dois computadores  
 O exemplo a seguir mostra como monitorar uma conversa específica na qual os serviços iniciador e de destino estão em computadores separados.  
  
```  
ssbdiagnose RUNTIME -ID D68D77A9-B1CF-41BF-A5CE-279ABCAB140D   
-TIMEOUT 10 CONNECT TO -E -S InitiatorComputer/InitiatorInstance   
-d InitiatorDatabase CONNECT TO -E -S TargetComputer/TargetInstance   
-d TargetDatabase  
```  
  
### <a name="h-monitor-the-status-of-a-conversation-in-two-databases-in-the-same-instance"></a>H. Monitorar o status de uma conversa em dois bancos de dados na mesma instância  
 O exemplo a seguir mostra como monitorar uma conversa específica na qual os serviços iniciador e de destino estão em bancos de dados separados na mesma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)]. O exemplo usa **baseconnectionoptions** para especificar as informações de instância e logon e duas cláusulas CONNECT TO para especificar os bancos de dados. -SHOWEVENTS é especificada para que todos os eventos de tempo de execução sejam incluídos na saída do relatório.  
  
```  
ssbdiagnose -E -S TestComputer/DevTestInstance RUNTIME -SHOWEVENTS   
-ID 5094d4a7-e38c-4c37-da37-1d58b1cb8455 -TIMEOUT 10 CONNECT TO   
-d InitiatorDatabase CONNECT TO -d TargetDatabase  
```  
  
### <a name="i-monitor-the-status-of-two-conversations-between-two-databases"></a>I. Monitorar o status de duas conversas entre dois bancos de dados  
 O exemplo a seguir mostra como monitorar duas conversas nas quais os serviços iniciador e de destino estão em bancos de dados separados na mesma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)]. O exemplo usa **baseconnectionoptions** para especificar as informações de instância e logon e duas cláusulas CONNECT TO para especificar os bancos de dados.  
  
```  
ssbdiagnose -E -S TestComputer/DevTestInstance RUNTIME   
-ID 5094d4a7-e38c-4c37-da37-1d58b1cb8455   
-ID 9b293be9-226b-4e22-e169-1d2c2c15be86 -TIMEOUT 10 CONNECT TO   
-d InitiatorDatabase CONNECT TO -d TargetDatabase  
```  
  
### <a name="j-monitor-the-status-of-all-conversations-between-two-databases"></a>J. Monitorar o status de todas as conversas entre dois bancos de dados  
 O exemplo a seguir mostra como monitorar todas as conversas entre dois bancos de dados na mesma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)]. O exemplo usa **baseconnectionoptions** para especificar as informações de instância e logon e duas cláusulas CONNECT TO para especificar os bancos de dados.  
  
```  
ssbdiagnose -E -S TestComputer/DevTestInstance RUNTIME   
-TIMEOUT 10 CONNECT TO -d InitiatorDatabase CONNECT TO   
-d TargetDatabase  
```  
  
### <a name="k-ignore-specific-errors"></a>K. Ignorar erros específicos  
 O exemplo a seguir mostra como ignorar erros conhecidos (303 e 304) no modo com a ativação está configurada atualmente em um sistema de teste.  
  
```  
ssbdiagnose -IGNORE 303 -IGNORE 304 -E -d TestDatabase   
CONFIGURATION FROM SERVICE /test/initiator TO SERVICE /test/target   
ON CONTRACT TextContract  
```  
  
### <a name="l-redirecting-ssbdiagnose-xml-output"></a>L. Redirecionando a saída XML de ssbdiagnose  
 O exemplo a seguir mostra como solicitar que o **ssbdiagnose** gere sua saída como um arquivo XML redirecionado para um arquivo. O arquivo TestDiag.xml pode ser aberto por um aplicativo para analisar ou relatar arquivos XML do **ssbdiagnose** . Se preferir, você pode exibi-lo de um editor de XML geral como o Bloco de Notas XML.  
  
```  
ssbdiagnose -XML -E -d MyDatabase CONFIGURATION FROM SERVICE   
/test/initiator TO SERVICE /test/target > c:\MyDiagnostics\TestDiag.xml  
```  
  
### <a name="m-using-an-environment-variable"></a>M. Usando uma variável de ambiente  
 O exemplo a seguir define primeiramente a variável de ambiente SQLCMDSERVER para conter o nome do servidor e executa **ssbdiagnose** sem especificar **-S**.  
  
```  
SET SQLCMDSERVER=MyComputer  
ssbdiagnose -XML -E -d MyDatabase CONFIGURATION FROM SERVICE   
/test/initiator TO SERVICE /test/target  
```  
  
## <a name="see-also"></a>Consulte também  
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)   
 [BEGIN DIALOG CONVERSATION &#40;Transact-SQL&#41;](/sql/t-sql/statements/begin-dialog-conversation-transact-sql)   
 [CREATE BROKER PRIORITY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-broker-priority-transact-sql)   
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-certificate-transact-sql)   
 [CREATE CONTRACT &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-contract-transact-sql)   
 [CREATE ENDPOINT &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-endpoint-transact-sql)   
 [CREATE MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-master-key-transact-sql)   
 [CREATE MESSAGE TYPE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-message-type-transact-sql)   
 [CREATE QUEUE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-queue-transact-sql)   
 [CREATE REMOTE SERVICE BINDING &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-remote-service-binding-transact-sql)   
 [CREATE ROUTE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-route-transact-sql)   
 [CREATE SERVICE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-service-transact-sql)   
 [RECEIVE &#40;Transact-SQL&#41;](/sql/t-sql/statements/receive-transact-sql)   
 [sys.transmission_queue &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-transmission-queue-transact-sql)   
 [sys.conversation_endpoints &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-conversation-endpoints-transact-sql)   
 [sys.conversation_groups &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-conversation-groups-transact-sql)  
  
  
