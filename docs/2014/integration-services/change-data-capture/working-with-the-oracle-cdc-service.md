---
title: Trabalhar com o serviço Oracle CDC | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 04be5896-2301-45f5-a8ce-5f4ef2b69aa5
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2f8854dba3c1d998d572481c285ee75dc933e480
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62771162"
---
# <a name="working-with-the-oracle-cdc-service"></a>Trabalhando com o Serviço Oracle CDC
  Esta seção descreve alguns conceitos importantes do Serviço Oracle CDC. Os conceitos incluídos nesta seção são:  
  
-   [O banco de dados MSXDBCDC](#BKMK_MSXDBCDC)  
  
     Esta seção descreve as tabelas que estão incluídas neste banco de dados e como ele é importante para o CDC.  
  
-   [Os bancos de dados CDC](#BKMK_CDCdatabase)  
  
     Essa seção fornece uma descrição breve dos bancos de dados CDC. Estes bancos de dados são criados usando o Console de Designer do Oracle CDC. Consulte a documentação incluída com sua instalação do CDC Designer Console para obter mais informações sobre os bancos de dados CDC.  
  
-   [Usando a linha de comando para configurar o Serviço CDC](#BKMK_CommandConfigCDC)  
  
     Esta seção descreve os comandos da linha de comando que podem ser usados para configurar o Serviço Oracle CDC.  
  
##  <a name="the-msxdbcdc-database"></a><a name="BKMK_MSXDBCDC"></a> O banco de dados MSXDBCDC  
 O banco de dados MSXDBCDC (Microsoft External-Database CDC) é um banco de dados especial que é necessário ao usar o Serviço CDC para Oracle com uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 O nome desse banco de dados não pode ser alterado. Se um banco de dados chamado MSXDBCDC existir na instância de host do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e contiver tabelas diferentes das definidas pelo Serviço CDC para Oracle, a instância de host do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não poderá ser usada.  
  
 Os usos principais para este banco de dados são:  
  
-   Servir como um registro de Serviços Oracle CDC associado a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Estas informações são usadas para a configuração de serviço e componentes de design, e para dar suporte à coordenação de vários serviços CDC pelo mesmo nome em diferentes nós sobre os quais um é o ativo.  
  
-   Servir como um registro das instâncias do Oracle CDC contidas em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , o serviço CDC que trata cada instância, e a versão de configuração que cada uma usa. Essas informações são equivalentes à coluna **is_cdc_enabled** na tabela **sys.databases** do banco de dados mestre. O serviço CDC periodicamente examina a tabela **dbo.xdbcdc_databases** para identificar alterações feitas à configuração de CDC ou à lista de instâncias capturadas.  
  
-   Manter os procedimentos armazenados de propriedade do **sysadmin**que ajudam a criar e manter instâncias de CDC. Estes são semelhantes aos procedimentos de sistema que são usados para a implementação do recurso do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CDC.  
  
### <a name="creating-the-msxdbcdc-database"></a>Criando o banco de dados MSXDBCDC  
 Um banco de dados MSXDBCDC deve ser criado antes que o Serviço Oracle CDC possa ser definido. Você só pode criar um banco de dados MSXDBCDC em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . O banco de dados MSXDBCDC é criado quando você prepara um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para o Oracle CDC. Isto pode ser feito usando o Console de Configuração do Serviço Oracle CDC ou executando um script de criação que é gerado pelo Console de Configuração do Serviço CDC.  
  
 O proprietário deste banco de dados é Administrador do Serviço Oracle CDC, que pode controlar todas as instâncias do Oracle CDC hospedadas sob a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **Consulte também:**  
  
 [Como preparar o SQL Server para CDC](prepare-sql-server-for-cdc.md)  
  
### <a name="the-msxdbcdc-database-tables"></a>As tabelas do banco de dados MSXDBCDC  
 Essa seção descreve as seguintes tabelas no banco de dados MSXDBCDC.  
  
-   [dbo.xdbcdc_trace](#BKMK_dboxdbcdc_trace)  
  
-   [dbo.xdbcdc_databases](#BKMK_dboxdbcdc_databases)  
  
-   [dbo.xdbcdc_services](#BKMK_dboxdbcdc_services)  
  
###  <a name="dboxdbcdc_trace"></a><a name="BKMK_dboxdbcdc_trace"></a> dbo.xdbcdc_trace  
 Esta tabela armazena informações de rastreamento para o Serviço Oracle CDC. As informações armazenadas nesta tabela incluem alterações de status notáveis e registros de rastreamento.  
  
 O Serviço Oracle CDC grava registros de erro e alguns registros de informações no log de eventos do Windows e na tabela de rastreamento. Em alguns casos, a tabela de rastreamento pode não estar acessível. No caso, as informações de erro estarão acessíveis do log de eventos.  
  
 A tabela a seguir descreve os itens incluídos na tabela **dbo.xdbcdc_trace** .  
  
|Item|DESCRIÇÃO|  
|----------|-----------------|  
|timestamp|O carimbo de data/hora UTC exato quando o registro de rastreamento foi gravado.|  
|type|Contém um dos seguintes valores.<br /><br /> ERROR<br /><br /> INFO<br /><br /> RASTREAMENTO|  
|nó|O nome do nó no qual o registro foi gravado.|  
|status|O código de status que é usado pela tabela de estado.|  
|sub_status|O código de substatus que é usado pela tabela de estado.|  
|status_message|A mensagem de status que é usada pela tabela de estado.|  
|source|O nome do componente do Oracle CDC que produziu o registro de rastreamento.|  
|text_data|Os dados de texto adicionais para casos em que o erro ou registro de rastreamento contém uma carga textual.|  
|binary_data|Os dados binários adicionais para casos em que o erro ou registro de rastreamento contém uma carga binária.|  
  
 A instância do Oracle CDC excluirá linhas de tabela de rastreamento antigas de acordo com a política de retenção de tabelas de alteração.  
  
###  <a name="dboxdbcdc_databases"></a><a name="BKMK_dboxdbcdc_databases"></a> dbo.xdbcdc_databases  
 Esta tabela contém os nomes de Serviço CDC para bancos de dados do Oracle CDC na instância atual do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Cada banco de dados corresponde a uma instância do Oracle CDC. O Serviço Oracle CDC usa esta tabela para determinar quais instâncias iniciar ou parar e quais instâncias reconfigurar.  
  
 A tabela a seguir descreve os itens incluídos na tabela **dbo.xdbcdc_databases** .  
  
|Item|DESCRIÇÃO|  
|----------|-----------------|  
|name|O nome do banco de dados Oracle na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|config_version|O carimbo de data/hora (UTC) para a última alteração na tabela **xdbcdc_config** correspondente do banco de dados CDC ou o carimbo de data/hora (UTC) para a linha atual nesta tabela.<br /><br /> O gatilho UPDATE impõe um valor de GETUTCDATE() para este item. **config_version** deixa o serviço CDC identificar a instância CDC que precisa ser verificada para alteração de configuração ou para habilitar/desabilitar.|  
|cdc_service_name|Este item determina qual Serviço Oracle CDC trata o banco de dados Oracle selecionado.|  
|Habilitado|Indica se a instância do Oracle CDC está ativa (1) ou desabilitada (0). Quando o Serviço Oracle CDC inicia, somente as instâncias marcadas como habilitadas (1) são iniciadas.<br /><br /> **Observação**: uma instância do Oracle CDC pode ser desabilitada devido a um erro não reproduzível. Neste caso, a instância deverá ser reiniciada manualmente depois que o erro for resolvido.|  
  
###  <a name="dboxdbcdc_services"></a><a name="BKMK_dboxdbcdc_services"></a> dbo.xdbcdc_services  
 Esta tabela lista os serviços CDC associados com a instância de host do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Esta tabela é usada pelo CDC Designer Console para determinar a lista de serviços CDC que são configurados para a instância local do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Ela também é usada pelo serviço CDC para garantir que somente um serviço em execução do Windows trate um determinado nome de serviço do Oracle CDC.  
  
 A tabela a seguir descreve os itens do estado de captura incluídos na tabela **dbo.xdbcdc_databases** .  
  
|Item|DESCRIÇÃO|  
|----------|-----------------|  
|cdc_service_name|O nome do Serviço Oracle CDC (o nome de serviço do Windows).|  
|cdc_service_sql_login|O nome do logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usado pelo Serviço Oracle CDC para conectar-se à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Um novo usuário de SQL chamado cdc_service é criado e associado com este nome de logon e é, em seguida, adicionado como membro das funções de banco de dados fixas db_ddladmin, db_datareader e db_datawriter para cada banco de dados CDC tratado pelo serviço.|  
|ref_count|Este item conta o número de computadores em que o mesmo Serviço Oracle CDC está instalado. Ele é incrementado com cada adição de serviço Oracle CDC de mesmo nome e é decrementado quando este serviço é removido. Quando o contador chegar a zero, esta linha será excluída.|  
|active_service_node|O nome do nó de Windows que atualmente trata o serviço CDC. Quando o serviço é parado corretamente, esta coluna é definida como nulo, indicando que não há mais um serviço ativo.|  
|active_service_heartbeat|Este item acompanha o serviço CDC atual para determinar se ele ainda está ativo.<br /><br /> Este item é atualizado com o carimbo de data/hora UTC do banco de dados atual para o serviço CDC ativo em intervalos regulares. O intervalo padrão é de 30 segundos; porém, o intervalo é configurável.<br /><br /> Quando um serviço CDC pendente detecta que a pulsação não foi atualizada depois que o intervalo configurado foi transmitido, o serviço pendente tenta assumir a função de serviço do CDC ativo.|  
|opções|Este item especifica as opções secundárias, como rastreamento ou ajuste. Ele é gravado no formato de **nome[=value][; ]** . A cadeia de caracteres de opções usa a mesma semântica que a cadeia de conexão ODBC. Se a opção for Booliana (com um valor de sim/não), o valor só poderá incluir o nome.<br /><br /> o rastreamento tem os seguintes valores possíveis:<br /><br /> true<br /><br /> on<br /><br /> false<br /><br /> Desligar<br /><br /> \<nome de classe>,[nome de classe>]<br /><br /> O valor padrão é **false**.<br /><br /> <br /><br /> **service_heartbeat_interval** é o intervalo de tempo (em segundos) para o serviço atualizar a coluna active_service_heartbeat. O valor padrão é **30**. O valor máximo é **3600**.<br /><br /> **service_config_polling_interval** é o intervalo de sondagem (em segundos) para o serviço CDC verificar as alterações de configuração. O valor padrão é **30**. O valor máximo é **3600**.<br /><br /> **sql_command_timeout** é o tempo limite de comando que funciona com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O valor padrão é **1**. O valor máximo é **3600**.|  
||  
  
### <a name="the-msxdbcdc-database-stored-procedures"></a>Os procedimentos armazenados do banco de dados MSXDBCDC  
 Essa seção descreve os seguintes procedimentos armazenados no banco de dados MSXDBCDC.  
  
-   [dbo.xcbcdc_reset_db(Database Name)](#BKMK_dboxcbcdc_reset_db)  
  
-   [dbo.xdbcdc_disable_db(dbname)](#BKMK_dboxdbcdc_disable_db)  
  
-   [dbo.xcbcdc_add_service(svcname,sqlusr)](#BKMK_dboxcbcdc_add_service)  
  
-   [dbo.xdbcdc_start(dbname)](#BKMK_dboxdbcdc_start)  
  
-   [dbo.xdbcdc_stop(dbname)](#BKMK_dboxdbcdc_stop)  
  
###  <a name="dboxcbcdc_reset_dbdatabase-name"></a><a name="BKMK_dboxcbcdc_reset_db"></a> dbo.xcbcdc_reset_db(Database Name)  
 Este procedimento desmarca os dados de uma instância do Oracle CDC. Ele é usado:  
  
-   Para reiniciar a captura de dados desconsiderando dados anteriores, por exemplo, após a recuperação de banco de dados de origem ou após inatividade em que alguns logs de transação do Oracle não estão disponíveis.  
  
-   Quando há danos no estado de CDC (especificamente nos dados de qualquer cdc.*tables).  
  
 O procedimento **dbo.xcbcdc_reset_db** executa as tarefas a seguir:  
  
-   Para a instância CDC (se ativo).  
  
-   Trunca as tabelas de alteração, a tabela **cdc_lsn_mapping** e a tabela **cdc_ddl_history** .  
  
-   Apaga a tabela **cdc_xdbcdc_state** .  
  
-   Apaga a coluna start_lsn para cada linha de **cdc_change_table**.  
  
 Para usar o procedimento **dbo.xcbcdc_reset_db** , o usuário deve ser membro da função de banco de dados **db_owner** para o banco de dados da Instância CDC que está sendo nomeada ou outro membro da função de servidor fixa **sysadmin** ou **serveradmin** .  
  
 Para obter mais informações sobre as tabelas de CDC, consulte *Os bancos de dados CDC* no sistema de ajuda no CDC Designer Console.  
  
###  <a name="dboxdbcdc_disable_dbdbname"></a><a name="BKMK_dboxdbcdc_disable_db"></a> dbo.xdbcdc_disable_db(dbname)  
 O procedimento **dbo.xcbcdc_disable_db** executa a tarefa a seguir:  
  
-   Remove a entrada para o banco de dados CDC selecionado na tabela MSXDBCDC.xdbcdc_databases.  
  
 Para usar o procedimento **dbo.xcbcdc_disable_db** , o usuário deve ser um membro da função de banco de dados **db_owner** para a instância CDC que está sendo nomeada ou membro da função de servidor fixa **sysadmin** ou **serveradmin** .  
  
 Para obter mais informações sobre as tabelas de CDC, consulte Os bancos de dados CDC no sistema de ajuda no CDC Designer Console.  
  
###  <a name="dboxcbcdc_add_servicesvcnamesqlusr"></a><a name="BKMK_dboxcbcdc_add_service"></a> dbo.xcbcdc_add_service(svcname,sqlusr)  
 O procedimento **dbo.xcbcdc_add_service** adiciona uma entrada à tabela **MSXDBCDC.xdbcdc_services** e adiciona um incremento de um à coluna ref_count para o nome de serviço na tabela **MSXDBCDC.xdbcdc_services** . Quando **ref_count** é 0, exclui a linha.  
  
 Para usar o procedimento **dbo.xcbcdc_add_service\<nome do serviço, nome do usuário>** , o usuário deve ser um membro da função de banco de dados **db_owner** para o banco de dados da instância CDC que está sendo nomeada ou membro da função de servidor fixa **sysadmin** ou **serveradmin**.  
  
###  <a name="dboxdbcdc_startdbname"></a><a name="BKMK_dboxdbcdc_start"></a> dbo.xdbcdc_start(dbname)  
 O procedimento **dbo.xdbcdc_start** envia uma solicitação de início ao serviço CDC que trata a instância CDC selecionada para iniciar o processamento de alteração.  
  
 Para usar o procedimento **dbo.xcdcdc_start** , o usuário deve ser membro da função de banco de dados **db_owner** para o banco de dados de CDC ou ser membro das funções **sysadmin** ou **serveradmin** para a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
###  <a name="dboxdbcdc_stopdbname"></a><a name="BKMK_dboxdbcdc_stop"></a> dbo.xdbcdc_stop(dbname)  
 O procedimento **dbo.xdbcdc_stop** envia uma solicitação de parada ao serviço CDC que trata a instância CDC selecionada para parar o processamento de alteração.  
  
 Para usar o procedimento **dbo.xcdcdc_stop** , o usuário deve ser membro da função de banco de dados **db_owner** para o banco de dados de CDC ou ser membro das funções **sysadmin** ou **serveradmin** para a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
##  <a name="the-cdc-databases"></a><a name="BKMK_CDCdatabase"></a> Os bancos de dados CDC  
 Cada instância do Oracle CDC usada em um serviço CDC está associada a um banco de dados específico do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] chamado de Banco de dados CDC. Este banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está hospedado na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] associada ao Serviço Oracle CDC.  
  
 O banco de dados CDC contém um esquema cdc especial. O Serviço Oracle CDC usa este esquema com nomes de tabela com o prefixo **xdbcdc_** . Este esquema é usado para fins de segurança e consistência.  
  
 A instância do Oracle CDC e os bancos de dados CDC são criados usando o Console de Designer do Oracle CDC. Para obter mais informações sobre os bancos de dados CDC, consulte a documentação incluída com sua instalação do Console de Designer do Oracle CDC.  
  
##  <a name="using-the-command-line-to-configure-the-cdc-service"></a><a name="BKMK_CommandConfigCDC"></a> Usando a linha de comando para configurar o Serviço CDC  
 Você pode operar o programa do Serviço Oracle CDC (xdbcdcsvc.exe) da linha de comando. O programa de serviço CDC é um arquivo executável do Windows de 32 bits/64 bits nativo.  
  
 **Consulte também**  
  
 [Como usar a interface de linha de comando do serviço CDC](how-to-use-the-cdc-service-command-line-interface.md)  
  
### <a name="service-program-commands"></a>Comandos do programa de serviço  
 A seção descreve os seguintes comandos que são usados para configurar o serviço CDC.  
  
-   [Config](#BKMK_config)  
  
-   [Criar](#BKMK_create)  
  
-   [Delete (excluir)](#BKMK_delete)  
  
###  <a name="config"></a><a name="BKMK_config"></a> Config  
 Use `Config` para atualizar uma configuração do Serviço de CDC Oracle de um script. O comando pode ser usado para atualizar somente partes específicas da configuração de serviço CDC (por exemplo, somente a cadeia de conexão sem saber a senha chave assimétrica). O comando deve ser executado por um administrador do computador. O item seguinte é um exemplo do comando `Config` :  
  
```  
"<path>xdbcdcsvc.exe" config  
     <cdc-service-name>  
     [connect= <sql-server-connection-string>]  
     [key= <asym-key-password>]  
     [svcacct= <windows-account> <windows-password>]  
     [sqlacct= <sql-username> <sql-password>]  
  
```  
  
 Em que:  
  
 **cdc-service-name** é o nome do serviço CDC a ser atualizado. Esse é um parâmetro necessário.  
  
 **sql-server-connection-string** é a cadeia de conexão a ser atualizada. Se a cadeia de conexão contiver espaços ou aspas, ela deverá ser envolvida em aspas duplas ("). As aspas inseridas são ignoradas dobrando-se os aspas.  
  
 **asym-key-password** é a senha a ser atualizada.  
  
 **windows-account**, **windows-password** são as credenciais de conta do Windows para o serviço que está sendo atualizado.  
  
 **sql-username**, **sql-password** são as credenciais de autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que estão sendo atualizadas. Se sqlacct tiver um nome de usuário vazio e senha vazia, o Serviço Oracle CDC se conectará ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando a autenticação do Windows.  
  
 **Observação**: qualquer parâmetro que contém espaços ou aspas duplas deve ser envolvido com aspas duplas ("). As marcas de aspas duplas inseridas devem ser dobradas (por exemplo, para usar **"A#B" D** como senha, insira **""A#B"" D"** ).  
  
###  <a name="create"></a><a name="BKMK_create"></a> Criar  
 Use `Create` para criar um Serviço Oracle CDC de um script. O comando deve ser executado por um administrador do computador. O item seguinte é um exemplo do comando `Create` :  
  
```  
"<path>xdbcdcsvc.exe" create  
     <cdc-service-name>  
     [connect= "<sql-server-connection-string>"]  
     [key= <asym-key-password>]  
     [svcacct <windows-account> <windows-password>]  
     [sqlacct <sql-username> <sql-password>]  
```  
  
 Em que:  
  
 **cdc-service-name** é o nome do serviço recém-criado. Se já houver um serviço com este nome, o programa retornará um erro. Você não deve usar nomes longos ou nomes com espaços. Os caracteres "/" e "\\" não são válidos em um nome de serviço. Esse é um parâmetro necessário.  
  
 **sql-server-connection-string** é a cadeia de conexão a ser usada para conectar à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está associada ao novo Serviço Oracle CDC.  
  
 **asym-key-password** é a senha que protege a chave assimétrica usada para armazenar as credenciais de mineração de logs do banco de dados de origem.  
  
 **windows-account**, **windows-password** são o nome da conta e senha associados ao Serviço Oracle CDC que está sendo criado.  
  
 **sql-username**, **sql-password** são o nome da conta e senha do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usados para conectar à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se esses dois parâmetros estiverem vazios, o Serviço CDC para Oracle se conectará ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando autenticação do Windows.  
  
 **Observação**: qualquer parâmetro que contém espaços ou aspas duplas deve ser envolvido com aspas duplas ("). As marcas de aspas duplas inseridas devem ser dobradas (por exemplo, para usar **"A#B" D** como senha, insira **""A#B"" D"** ).  
  
###  <a name="delete"></a><a name="BKMK_delete"></a> Delete (excluir)  
 Use `Delete` para excluir corretamente o Serviço Oracle CDC de um script. Este comando deve ser executado por um administrador do computador. O item seguinte é um exemplo do comando `Delete` :  
  
```  
"<path>xdbcdcsvc.exe" delete  
    <cdc-service-name>  
  
```  
  
 Em que:  
  
 **cdc-service-name** é o nome do serviço CDC a ser excluído.  
  
 **Observação**: qualquer parâmetro que contém espaços ou aspas duplas deve ser envolvido com aspas duplas ("). As marcas de aspas duplas inseridas devem ser dobradas (por exemplo, para usar **"A#B" D** como senha, insira **""A#B"" D"** ).  
  
## <a name="see-also"></a>Consulte Também  
 [Como usar a interface de linha de comando do Serviço CDC](how-to-use-the-cdc-service-command-line-interface.md)   
 [Como preparar o SQL Server para CDC](prepare-sql-server-for-cdc.md)  
