---
title: Instalar o SQL Server 2016 R Services (no banco de dados) | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 75e962b9be2acb1d44451081f0aef2bccd5a09fc
ms.sourcegitcommit: 9528843359cc43b9c66afac363f542ae343266e9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/22/2018
ms.locfileid: "40437615"
---
# <a name="install-sql-server-2016-r-services-in-database"></a>Instalar o SQL Server 2016 R Services (no banco de dados) 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo explica como instalar e configurar **SQL Server 2016 R Services (no banco de dados)**. Se você tiver o SQL Server 2016, instale esse recurso para permitir a execução de código do R no SQL Server.

## <a name="bkmk_prereqs"> </a> Lista de verificação de pré-instalação

+ Instalação do SQL Server 2016 é necessária se você quiser instalar o R Services. Se em vez disso, você tiver a mídia de instalação do SQL Server 2017, você deve instalar [serviços SQL Server 2017 Machine Learning (no banco de dados)](sql-machine-learning-services-windows-install.md) para obter a integração do R para essa versão do SQL Server.

+ Uma instância do mecanismo de banco de dados é necessária. Você não pode instalar apenas R, embora você possa adicioná-lo incrementalmente a uma instância existente.

+ Não instale o R Services em um cluster de failover. O mecanismo de segurança usado para isolar processos do R não é compatível com um ambiente de cluster de failover do Windows Server.

+ Não instale o R Services em um controlador de domínio. A parte de serviços de R da instalação falhará.

+ Não instale **recursos compartilhados** > **R Server (autônomo)** no mesmo computador que está executando uma instância no banco de dados. 

+ Instalação lado a lado com outras versões do R e Python são possíveis porque a instância do SQL Server usa suas próprias cópias das distribuições de R e Anaconda do código-fonte aberto. No entanto, a execução de código que usa o R e Python no computador do SQL Server fora do SQL Server pode levar a vários problemas:
    
  + Você usa uma biblioteca diferente e executável diferente e obter resultados diferentes, do que quando você estiver executando no SQL Server.
  + Scripts de R e Python em execução em bibliotecas externas não podem ser gerenciados pelo SQL Server, levando à contenção de recursos.
  
Se você tiver usado todas as versões anteriores do ambiente de desenvolvimento do Revolution Analytics ou os pacotes RevoScaleR ou se você instalou todas as versões de pré-lançamento do SQL Server 2016, você deve desinstalá-los. Não há suporte para que executam versões mais antigas e mais recentes do RevoScaleR e outros pacotes de proprietários. Para obter ajuda sobre como remover versões anteriores, consulte [atualização e perguntas frequentes sobre a instalação do SQL Server Machine Learning Services](../r/upgrade-and-installation-faq-sql-server-r-services.md).

> [!IMPORTANT]
> Após a conclusão da instalação, certifique-se de concluir as etapas adicionais de pós-configuração descritas neste artigo. Essas etapas incluem a habilitação do SQL Server usar scripts externos e adicionando as contas necessárias para o SQL Server executar trabalhos do R em seu nome. Alterações de configuração geralmente requerem uma reinicialização da instância ou uma reinicialização do serviço Launchpad.

## <a name="get-the-installation-media"></a>Obtenha a mídia de instalação

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

 ###  <a name="bkmk_ga_instalpatch"></a> Instalar o requisito de patch 

A Microsoft identificou um problema com a versão específica dos binários do Tempo de Execução Microsoft VC++ 2013 que são instalados como um pré-requisito pelo SQL Server. Se essa atualização para os binários do Tempo de Execução de VC não for instalada, o SQL Server poderá apresentar problemas de estabilidade em determinados cenários. Antes de instalar o SQL Server, siga as instruções em [Notas de Versão do SQL Server](../../sql-server/sql-server-2016-release-notes.md#bkmk_ga_instalpatch) para ver se seu computador precisa de um patch para os binários de tempo de execução do VC.  

## <a name="bkmk2016top"></a>Execute a instalação

Para instalações locais, você deve executar a Instalação como um administrador. Se você instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de um compartilhamento remoto, deverá usar uma conta de domínio que tenha permissões de leitura e de execução no compartilhamento remoto.

1. Inicie o Assistente de instalação do SQL Server 2016.

2. Sobre o **instalação** guia, selecione **instalação autônoma do novo SQL Server ou adicionar recursos a uma instalação existente**.
    
   ![Instalar o R Services (no banco de dados)](media/2016-setup-installation-rsvcs.png "Iniciar instalação do mecanismo de banco de dados com R Services")
   
3. Sobre o **seleção de recursos** , selecione as opções a seguir:

   - Selecione **serviços de mecanismo de banco de dados**. O mecanismo de banco de dados é necessário em cada instância que usa o aprendizado de máquina.
   - Selecione **R Services (no banco de dados)**. Instala o suporte para uso no banco de dados do R.
    
     ![Seleção de recursos de R Services](media/2016setup-rsvcs-features.png "selecione esses recursos para R Services no banco de dados")

    > [!IMPORTANT]
    > Não instale o servidor R e R Services ao mesmo tempo. Normalmente você deve instalar o R Server (autônomo) para criar um ambiente que um desenvolvedor ou cientista de dados usa para se conectar ao SQL Server e implantar soluções de R. Portanto, não é necessário instalar ambos no mesmo computador.

4.  Sobre o **consentimento para instalar o Microsoft R Open** , clique em **Accept**.
  
    Este contrato de licença é necessária para baixar o Microsoft R Open, que inclui uma distribuição de pacotes de base de R de código-fonte aberto e ferramentas, junto com pacotes de R aprimorados e provedores de conectividade da equipe de desenvolvimento do Microsoft R.
  
5. Depois que você aceitou o contrato de licença, há uma pequena pausa enquanto o instalador está preparado. Clique em **próxima** quando o botão fica disponível.

6. Sobre o **pronto para instalar** página, verifique se os itens a seguir estão incluídos e, em seguida, selecione **instalar**.

   + Serviços do Mecanismo de Banco de Dados
   + R Services (no Banco de Dados)

    Anote o local da pasta no caminho `..\Setup Bootstrap\Log` onde os arquivos de configuração são armazenados. Quando a instalação for concluída, você pode examinar os componentes instalados no arquivo de resumo.

7. Após a instalação for concluída, se você for instruído a reiniciar o computador, faça isso agora. É importante ler a mensagem do Assistente de Instalação ao concluir a Instalação. Para obter mais informações, consulte [View and Read SQL Server Setup Log Files](https://docs.microsoft.com/sql/database-engine/install-windows/view-and-read-sql-server-setup-log-files).


##  <a name="bkmk_enableFeature"></a>Habilitar a execução do script externo

1. Abra o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. 

    > [!TIP]
    > Você pode baixar e instalar a versão apropriada nesta página: [baixar o SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).
    > 
    > Você também pode experimentar a versão de visualização da [SQL Operations Studio](https://docs.microsoft.com/sql/sql-operations-studio/what-is), que oferece suporte a tarefas administrativas e consultas no SQL Server.
  
2. Conecte-se à instância onde você instalou os serviços de Machine Learning, clique em **nova consulta** para abrir uma janela de consulta e execute o seguinte comando:

   ```SQL
   sp_configure
   ```
    O valor da propriedade `external scripts enabled`, deve ser **0** neste momento. Isso ocorre porque o recurso é desativado por padrão. O recurso deve ser habilitado explicitamente por um administrador antes de executar scripts R ou Python.
     
3. Para habilitar o recurso de script externo, execute a seguinte instrução:
  
    ```SQL
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    ```
  
## <a name="restart-the-service"></a>Reinicie o serviço.

Quando a instalação for concluída, reinicie o mecanismo de banco de dados antes de continuar para a próxima, permitindo a execução do script.

Reiniciar o serviço também automaticamente reinicia relacionado [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] service.

Você pode reiniciar o serviço usando o botão direito do mouse **reinicie** comando para a instância no SSMS ou usando o **Services** painel no painel de controle ou usando [SQL Server Configuration Manager ](../../relational-databases/sql-server-configuration-manager.md).

## <a name="verify-installation"></a>Verifique a instalação

Use as etapas a seguir para verificar se todos os componentes usados para iniciar o script externo estão em execução.

1. No SQL Server Management Studio, abra uma nova janela de consulta e execute o seguinte comando:
    
    ```SQL
    EXEC sp_configure  'external scripts enabled'
    ```

    O **run_value** agora deve ser definido como 1.

2. Abra o **Services** painel ou o SQL Server Configuration Manager e verifique se **Launchpad do SQL Server service** está em execução. Você deve ter um serviço para cada instância do mecanismo de banco de dados que tem o R ou Python instalado. Para obter mais informações, consulte [componentes para dar suporte à integração de Python](../python/new-components-in-sql-server-to-support-python-integration.md).

7. Se o Launchpad estiver em execução, você poderá executar R simple para verificar se os tempos de execução de scripts externos podem se comunicar com o SQL Server. 

    Abra uma nova **consulta** janela no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], e, em seguida, executar um script como o seguinte:
    
    ```SQL
    EXEC sp_execute_external_script  @language =N'R',
    @script=N'
    OutputDataSet <- InputDataSet;
    ',
    @input_data_1 =N'SELECT 1 AS hello'
    WITH RESULT SETS (([hello] int not null));
    GO
    ```

    O script pode demorar um pouco enquanto executar na primeira vez que o tempo de execução do script externo é carregado. Os resultados devem ser algo parecido com isto:

    | hello |
    |----|
    | 1|

## <a name="bkmk_FollowUp"></a> Configuração adicional

Se a etapa de verificação de script externo foi bem-sucedida, você pode executar comandos de Python do SQL Server Management Studio, Visual Studio Code ou qualquer outro cliente que pode enviar instruções T-SQL para o servidor.

Se você obteve um erro ao executar o comando, examine as etapas de configuração adicionais nesta seção. Talvez seja necessário fazer configurações adicionais de apropriado para o serviço ou o banco de dados.

Cenários comuns que requerem alterações adicionais incluem:

* [Configurar o firewall do Windows para conexões de entrada](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)
* [Habilite os protocolos de rede adicionais](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)
* [Habilitar conexões remotas](../../database-engine/configure-windows/configure-the-remote-access-server-configuration-option.md)
* [Estender permissões internas para usuários remotos](#bkmk_configureAccounts)
* [Conceder permissão para executar scripts externos](#bkmk_AllowLogon)
* [Conceder acesso a bancos de dados individuais](#permissions-db)

> [!NOTE]
> Nem todas as alterações listadas são necessárias e nenhum pode ser necessária. Os requisitos dependem de seu esquema de segurança, onde você instalou o SQL Server e como você espera que os usuários para se conectar ao banco de dados e executar scripts externos. Dicas de solução de problemas adicionais podem ser encontradas aqui: [perguntas frequentes sobre atualização e instalação](../r/upgrade-and-installation-faq-sql-server-r-services.md)

### <a name="bkmk_configureAccounts"></a>Habilitar a autenticação implícita para o grupo de contas do Launchpad

Durante a instalação, algumas novas contas de usuário do Windows são criadas para execução de tarefas no token de segurança do [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] service. Quando um usuário envia um script R de um cliente externo, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ativa uma conta de trabalho disponível, mapeia-os para a identidade do usuário da chamada e, em seguida, executa o script de R em nome do usuário. Esse novo serviço do mecanismo de banco de dados oferece suporte à execução segura de scripts externos, chamado *autenticação implícita*.

Você pode exibir essas contas no grupo de usuários do Windows **SQLRUserGroup**. Por padrão, são criadas 20 contas de trabalho, que geralmente é mais do que suficiente para a execução de R de trabalhos.

No entanto, se você precisa executar scripts de R de um cliente de ciência de dados remoto e estiver usando a autenticação do Windows, você deve conceder essas contas de trabalho permissão para entrar para a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância em seu nome.

1. No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], no Pesquisador de Objetos, expanda **Segurança**, clique com o botão direito do mouse em **Logons**e selecione **Novo Logon**.
2. No **logon - novo** caixa de diálogo, selecione **pesquisa**.
3. Selecione o **tipos de objetos** e **grupos** caixas de seleção e desmarque todas as outras caixas de seleção.
4. Clique em **Advanced**, verifique se o local de pesquisa é o computador atual e clique **Localizar agora**.
5. Percorra a lista de contas de grupo no servidor até encontrar uma que começa com `SQLRUserGroup`.
    
    + O nome do grupo que está associada com o serviço Launchpad a _instância padrão_ é sempre apenas **SQLRUserGroup**. Selecione essa conta somente para a instância padrão.
    + Se você estiver usando um _instância nomeada_, o nome da instância é acrescentado ao nome padrão, `SQLRUserGroup`. Portanto, se a instância é denominada "MLTEST", o nome do grupo de usuário padrão para essa instância seria **SQLRUserGroupMLTest**.
5. Clique em **Okey** para fechar a caixa de diálogo de pesquisa avançada e verifique se você selecionou a conta correta para a instância. Cada instância pode usar apenas seu próprio serviço Launchpad e o grupo criado para o serviço.
6. Clique em **Okey** mais uma vez para fechar o **Selecionar usuário ou grupo** caixa de diálogo.
7. No **logon - novo** caixa de diálogo, clique em **Okey**. Por padrão, o logon é atribuído à função **pública** e tem permissão para se conectar ao mecanismo de banco de dados.

### <a name="bkmk_AllowLogon"></a>Conceder aos usuários permissão para executar scripts externos

> [!NOTE]
> Se você usar um logon do SQL para executar scripts R em um contexto de computação do SQL Server, essa etapa não é necessária.

Se você instalou o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em sua própria instância, normalmente, execução de scripts como administrador, ou pelo menos um proprietário de banco de dados, e, portanto, têm permissões implícitas para várias operações, todos os dados no banco de dados e a capacidade de instalar novos pacotes conforme o necessário.

No entanto, em um cenário empresarial, a maioria dos usuários, incluindo os usuários que acessam o banco de dados usando logons do SQL Server, não tem permissões elevadas desse tipo. Portanto, para cada usuário que executará scripts R, você deve conceder as permissões de usuário para executar scripts em cada banco de dados em scripts externos serão usados.

```SQL
USE <database_name>
GO
GRANT EXECUTE ANY EXTERNAL SCRIPT  TO [UserName]
```

> [!TIP]
> Precisa de ajuda com a instalação? Não tem certeza de que executou todas as etapas? Use esses relatórios personalizados para verificar o status da instalação e executar etapas adicionais. 
> 
> [Monitorar serviços do Machine Learning usando relatórios personalizados](../r/monitor-r-services-using-custom-reports-in-management-studio.md).

### <a name="permissions-db"></a> Dar a seus usuários de leitura, gravação ou permissões de DDL para o banco de dados

A conta de usuário que é usada para executar o R pode precisar para ler dados de outros bancos de dados, criar novas tabelas para armazenar os resultados e gravar dados em tabelas. Portanto, para cada usuário que executar scripts R, certifique-se de que o usuário tem as permissões apropriadas no banco de dados: *db_datareader*, *db_datawriter*, ou *db_ddladmin*.

Por exemplo, a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] a seguir concede ao logon SQL *MySQLLogin* os direitos para executar consultas T-SQL no banco de dados *RSamples* . Para executar essa instrução, o logon SQL já deve existir no contexto de segurança do servidor.

```SQL
USE RSamples
GO
EXEC sp_addrolemember 'db_datareader', 'MySQLLogin'
```

Para obter mais informações sobre as permissões incluídas em cada função, consulte [funções de nível de banco de dados](../../relational-databases/security/authentication-access/database-level-roles.md).


### <a name="create-an-odbc-data-source-for-the-instance-on-your-data-science-client"></a>Criar uma fonte de dados ODBC para a instância no cliente de ciência de dados

Se você criar uma solução de R em um computador de cliente de ciência de dados e precisa executar código usando o computador do SQL Server como o contexto de computação, você pode usar um logon SQL ou a autenticação integrada do Windows.

* Para logons SQL: certifique-se de que o logon tenha as permissões apropriadas no banco de dados em que os dados serão lidos. Você pode fazer isso adicionando *se conectar ao* e *selecionar* permissões, ou adicionando o logon para o *db_datareader* função. Para logons que precisa para criar objetos, adicione *DDL_admin* direitos. Para logons que devem salvar dados em tabelas, adicione o logon para o *db_datawriter* função.

* Para a autenticação do Windows: talvez você precise configurar uma fonte de dados ODBC no cliente de ciência de dados que especifica o nome da instância e outras informações de conexão. Para obter mais informações, consulte [administrador de fonte de dados ODBC](https://docs.microsoft.com/sql/odbc/admin/odbc-data-source-administrator).

## <a name="suggested-optimizations"></a>Otimizações sugeridas

Agora que você tem tudo funcionando, você também poderá otimizar o servidor para oferecer suporte ao aprendizado de máquina ou modelos pré-treinados de instalação.

### <a name="add-more-worker-accounts"></a>Adicionar mais contas de trabalho

Se você achar que você pode usar o R muito ou se você espera que vários usuários executando scripts simultaneamente, você pode aumentar o número de contas de trabalho que são atribuídos ao serviço Launchpad. Para obter mais informações, consulte [modificar o pool de conta de usuário para serviços do SQL Server Machine Learning](../r/modify-the-user-account-pool-for-sql-server-r-services.md).

### <a name="bkmk_optimize"></a>Otimizar o servidor para execução de scripts externos

As configurações padrão para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalação destinam-se para otimizar o equilíbrio entre o servidor para uma variedade de serviços que têm suporte pelo mecanismo de banco de dados, que pode incluir a extração, transformação e carregamento (ETL) de processos, relatórios, auditoria, e aplicativos que usam [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dados. Portanto, sob as configurações padrão, você pode encontrar recursos de aprendizagem de máquina, às vezes, são restritos ou limitados, especialmente em operações com uso intensivo de memória.

Para garantir que os trabalhos de aprendizado de máquina são priorizados e tenham os recursos apropriados, é recomendável que você use o administrador de recursos do SQL Server para configurar um pool de recursos externos. Você também poderá alterar a quantidade de memória alocada para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mecanismo de banco de dados ou aumentar o número de contas que são executados sob o [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] service.

- Para configurar um pool de recursos para gerenciamento de recursos externos, consulte [criar um pool de recursos externos](../../t-sql/statements/create-external-resource-pool-transact-sql.md).
  
- Para alterar a quantidade de memória reservada para o banco de dados, consulte [opções de configuração de memória do servidor](../../database-engine/configure-windows/server-memory-server-configuration-options.md).
  
- Para alterar o número de contas do R que pode ser iniciado por [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)], consulte [modificar o pool de conta de usuário para o machine learning](../r/modify-the-user-account-pool-for-sql-server-r-services.md).

Se você estiver usando o Standard Edition e tiver o Resource Governor, você pode usar eventos estendidos e exibições de gerenciamento dinâmico (DMVs), bem como eventos do Windows de monitoramento, para ajudar a gerenciar os recursos de servidor que são usados pelo R. Para obter mais informações, consulte [monitoramento e gerenciamento de serviços de R](../r/managing-and-monitoring-r-solutions.md).

### <a name="install-additional-r-packages"></a>Instalar pacotes R adicionais

As soluções de R que você cria para o SQL Server podem chamar funções básicas de R, funções de pacotes de proprietários instalados com o SQL Server e pacotes de R de terceiros compatível com a versão de software livre R instalado pelo SQL Server.

Pacotes que você desejar usar do SQL Server deverão ser instalados na biblioteca padrão usada pela instância. Se você tiver uma instalação separada do R no computador, ou se você tiver instalado pacotes em bibliotecas do usuário, você não poderá usar os pacotes do T-SQL.

O processo para instalar e gerenciar pacotes de R é diferente no SQL Server 2016 e SQL Server 2017. No SQL Server 2016, um administrador de banco de dados deve instalar os pacotes de R que os usuários precisam. No SQL Server 2017, você pode configurar grupos de usuários para compartilhar pacotes em um nível por banco de dados ou configurar as funções de banco de dados para permitir que os usuários instalem seus próprios pacotes. Para obter mais informações, consulte [instalar novos pacotes de R](../r/install-additional-r-packages-on-sql-server.md).


## <a name="get-help"></a>Obter ajuda

Precisa de ajuda com a instalação ou atualização? Para obter respostas a perguntas comuns e problemas conhecidos, consulte o artigo a seguir:

* [Atualização e instalação perguntas Frequentes - serviços de Machine Learning](../r/upgrade-and-installation-faq-sql-server-r-services.md)

Para verificar o status da instalação da instância e corrigir problemas comuns, experimente estes relatórios personalizados.

* [Relatórios personalizados para o SQL Server R Services](../r/monitor-r-services-using-custom-reports-in-management-studio.md)

## <a name="next-steps"></a>Próximas etapas

Os desenvolvedores do R podem começar com alguns exemplos simples e aprender os fundamentos de como o R funciona com o SQL Server. Para a próxima etapa, consulte os links a seguir:

+ [Tutorial: Executar R no T-SQL](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [Tutorial: Análise de no banco de dados para os desenvolvedores do R](../tutorials/sqldev-in-database-r-for-sql-developers.md)

Para exibir exemplos de aprendizado de máquina com base em cenários do mundo real, consulte [tutoriais de aprendizado de máquina](../tutorials/machine-learning-services-tutorials.md).


