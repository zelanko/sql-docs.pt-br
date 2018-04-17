---
title: Instalar o SQL Server 2016 R Services (no banco de dados) | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 86263158581b92af42a7ad1ce9b538b2c1cdbfa7
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="install-sql-server-2016-r-services-in-database"></a>Instalar o SQL Server 2016 R Services (no banco de dados) 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo explica como instalar e configurar **SQL Server 2016 R Services (no banco de dados)**. Se você tiver o SQL Server 2016, instale esse recurso para habilitar a execução do código R no SQL Server.

## <a name="bkmk_prereqs"> </a> Lista de verificação de pré-instalação

+ A instalação do SQL Server 2016 é necessária se você quiser instalar o R Services. Se, em vez disso, você tem a mídia de instalação do SQL Server 2017, você deve instalar [serviços do aprendizado de máquina 2017 SQL Server (no banco de dados)](sql-machine-learning-services-windows-install.md) para obter a integração do R para essa versão do SQL Server.

+ Uma instância do mecanismo de banco de dados é necessária. Você não pode instalar apenas R, embora você pode adicioná-lo incrementalmente para uma instância existente.

+ Não instale o R Services em um cluster de failover. O mecanismo de segurança usado para isolar processos de R não é compatível com um ambiente de cluster de failover do Windows Server.

+ Não instale o R Services em um controlador de domínio. A parte de serviços de R de instalação falhará.

+ Não instale **recursos compartilhados** > **R Server (autônomo)** no mesmo computador que está executando uma instância no banco de dados. 

+ Instalação lado a lado com outras versões do R e Python são possíveis porque a instância do SQL Server usa suas próprias cópias as distribuições de R e Anaconda do código-fonte aberto. No entanto, executando o código que usa o R e Python no computador do SQL Server fora do SQL Server pode causar vários problemas:
    
  + Usar uma biblioteca diferente e o executável diferente e obter resultados diferentes, que é feito quando você estiver executando no SQL Server.
  + Scripts de R e Python em execução em bibliotecas externas não podem ser gerenciados pelo SQL Server, levando a contenção de recursos.
  
Se você usou as versões anteriores do pacotes RevoScaleR ou o ambiente de desenvolvimento do Revolution Analytics, ou se você instalou as versões de pré-lançamento do SQL Server 2016, você deve desinstalá-los. Não há suporte para que executam versões mais antigas e mais recentes do RevoScaleR e outros pacotes proprietárias. Para obter ajuda sobre como remover versões anteriores, consulte [atualização e perguntas Frequentes de instalação de serviços de aprendizado de máquina do SQL Server](../r/upgrade-and-installation-faq-sql-server-r-services.md).

> [!IMPORTANT]
> Após a conclusão da instalação, certifique-se de concluir as etapas adicionais de pós-configuração descritas neste artigo. Essas etapas incluem a habilitar o SQL Server para usar scripts externos e adicionar contas necessárias para o SQL Server executar trabalhos de R em seu nome. Alterações de configuração geralmente requerem uma reinicialização da instância, ou uma reinicialização do serviço Launchpad.

## <a name="get-the-installation-media"></a>Obtenha a mídia de instalação

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

 ###  <a name="bkmk_ga_instalpatch"></a> Instalar o requisito de patch 

A Microsoft identificou um problema com a versão específica dos binários do Tempo de Execução Microsoft VC++ 2013 que são instalados como um pré-requisito pelo SQL Server. Se essa atualização para os binários do Tempo de Execução de VC não for instalada, o SQL Server poderá apresentar problemas de estabilidade em determinados cenários. Antes de instalar o SQL Server, siga as instruções em [Notas de Versão do SQL Server](../../sql-server/sql-server-2016-release-notes.md#bkmk_ga_instalpatch) para ver se seu computador precisa de um patch para os binários de tempo de execução do VC.  

## <a name="bkmk2016top"></a>Execute a instalação

Para instalações locais, você deve executar a Instalação como um administrador. Se você instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de um compartilhamento remoto, deverá usar uma conta de domínio que tenha permissões de leitura e de execução no compartilhamento remoto.

1. Inicie o Assistente de instalação do SQL Server 2016.

2. Sobre o **instalação** guia, selecione **instalação autônoma do novo SQL Server ou adicionar recursos a uma instalação existente**.
    
   ![Instalar o R Services (no banco de dados)](media/2016-setup-installation-rsvcs.png "iniciar a instalação do mecanismo de banco de dados com os serviços de R")
   
3. Sobre o **seleção de recursos** , selecione as seguintes opções:

   - Selecione **serviços do mecanismo de banco de dados**. O mecanismo de banco de dados é necessário em cada instância que usa o aprendizado de máquina.
   - Selecione **R Services (no banco de dados)**. Instala o suporte para uso no banco de dados de R.
    
     ![Seleção de recursos de serviços de R](media/2016setup-rsvcs-features.png "selecione esses recursos para R Services no banco de dados")

    > [!IMPORTANT]
    > Não instale os serviços de R e R Server ao mesmo tempo. Normalmente, você deve instalar o R Server (autônomo) para criar um ambiente em que um cientista de dados ou o desenvolvedor usa para se conectar ao SQL Server e implantar soluções de R. Portanto, não é necessário instalar ambos no mesmo computador.

4.  Sobre o **consentimento para instalar o Microsoft R Open** , clique em **aceitar**.
  
    Este contrato de licença é necessário para baixar o Microsoft R Open, que inclui uma distribuição dos pacotes de base de R de código-fonte aberto e ferramentas, junto com pacotes de R aprimorados e provedores de conectividade da equipe de desenvolvimento do Microsoft R.
  
5. Depois que você aceitou o contrato de licença, há uma pequena pausa enquanto o instalador está preparado. Clique em **próximo** quando o botão ficará disponível.

6. Sobre o **pronto para instalar** página, verifique se os seguintes itens são incluídos e, em seguida, selecione **instalar**.

   + Serviços do Mecanismo de Banco de Dados
   + R Services (no Banco de Dados)

    Anote o local da pasta no caminho `..\Setup Bootstrap\Log` onde os arquivos de configuração são armazenados. Quando a instalação for concluída, você pode examinar os componentes instalados no arquivo de resumo.

7. Quando a instalação for concluída, reinicie o computador.

##  <a name="bkmk_enableFeature"></a>Habilitar a execução do script externo

1. Abra o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. 

    > [!TIP]
    > Você pode baixar e instalar a versão apropriada nesta página: [baixar o SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).
    > 
    > Você também pode testar a versão de visualização de [Studio de operações SQL](https://docs.microsoft.com/sql/sql-operations-studio/what-is), que oferece suporte a tarefas administrativas e consultas no SQL Server.
  
2. Conecte-se à instância onde você instalou os serviços de aprendizado de máquina, clique em **nova consulta** para abrir uma janela de consulta e execute o seguinte comando:

   ```SQL
   sp_configure
   ```
    O valor da propriedade `external scripts enabled`, deve ser **0** neste momento. Isso ocorre porque o recurso está desativado por padrão. O recurso deve ser habilitado explicitamente por um administrador antes de executar scripts R ou Python.
     
3. Para habilitar o recurso de script externo, execute a seguinte instrução:
  
    ```SQL
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    ```
  
## <a name="restart-the-service"></a>Reinicie o serviço.

Quando a instalação for concluída, reinicie o mecanismo de banco de dados antes de prosseguir para a próxima, permitindo a execução do script.

Reiniciar o Nom automaticamente reinicia relacionado [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] serviço.

Você pode reiniciar o serviço usando o botão direito do mouse **reiniciar** comando para a instância no SSMS, ou usando o **serviços** painel no painel de controle ou usando [SQL Server Configuration Manager ](../../relational-databases/sql-server-configuration-manager.md).

## <a name="verify-installation"></a>Verifique a instalação

Use as etapas a seguir para verificar se todos os componentes usados para iniciar o script externo estão em execução.

1. No SQL Server Management Studio, abra uma nova janela de consulta e execute o seguinte comando:
    
    ```SQL
    EXEC sp_configure  'external scripts enabled'
    ```

    O **run_value** agora deve ser definido como 1.

2. Abra o **serviços** painel ou o SQL Server Configuration Manager e verifique se **serviço Launchpad do SQL Server** está em execução. Você deve ter um serviço para cada instância do mecanismo de banco de dados que tem o R ou Python instalado. Reinicie o serviço se não estiver em execução. Para obter mais informações, consulte [componentes para dar suporte à integração do Python](../python/new-components-in-sql-server-to-support-python-integration.md).

7. Se estiver executando a barra inicial, você poderá executar R simple para verificar se os tempos de execução de script externos podem se comunicar com o SQL Server. 

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

    O script pode demorar um pouco enquanto para ser executado na primeira vez que o tempo de execução do script externo é carregado. Os resultados devem ser algo assim:

    | hello |
    |----|
    | 1|

## <a name="bkmk_FollowUp"></a> Configuração adicional

Se a etapa de verificação de script externo foi bem-sucedida, você pode executar comandos de Python do SQL Server Management Studio, o código do Visual Studio ou qualquer outro cliente que pode enviar instruções T-SQL para o servidor.

Se você receber um erro ao executar o comando, examine as etapas de configuração adicionais nesta seção. Talvez seja necessário fazer configurações adicionais de apropriado para o serviço ou o banco de dados.

Cenários comuns que exigem alterações adicionais incluem:

* [Configurar o firewall do Windows para conexões de entrada](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)
* [Habilitar protocolos de rede adicionais](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)
* [Habilitar conexões remotas](../../database-engine/configure-windows/configure-the-remote-access-server-configuration-option.md)
* [Estender permissões internas para usuários remotos](#bkmk_configureAccounts)
* [Conceder permissão para executar scripts externos](#bkmk_AllowLogon)
* [Conceder acesso a bancos de dados individuais](#permissions-db)

> [!NOTE]
> Nem todas as alterações listadas são necessárias, e nenhum pode ser necessária. Requisitos dependem de seu esquema de segurança, onde você instalou o SQL Server e como você espera que os usuários a se conectar ao banco de dados e executar scripts externos. Dicas de solução de problemas adicionais podem ser encontradas aqui: [perguntas frequentes sobre atualização e instalação](../r/upgrade-and-installation-faq-sql-server-r-services.md)

### <a name="bkmk_configureAccounts"></a>Habilitar autenticação implícita para o grupo de contas da barra inicial

Durante a instalação, algumas novas contas de usuário do Windows são criadas para executar tarefas nas quais o token de segurança do [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] service. Quando um usuário envia um script R de um cliente externo, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ativa uma conta de trabalho disponível, ele é mapeado para a identidade do usuário da chamada e executa o script de R em nome do usuário. Esse novo serviço do mecanismo de banco de dados oferece suporte à execução segura de scripts externos, chamado *autenticação implícita*.

Você pode exibir essas contas no grupo de usuário do Windows **SQLRUserGroup**. Por padrão, 20 contas de trabalho são criadas, que geralmente é mais do que suficiente para a execução de R trabalhos.

No entanto, se você precisa executar scripts R de um cliente de ciência de dados remoto e estiver usando a autenticação do Windows, você deve conceder essas contas de trabalho permissão para entrar para a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância em seu nome.

1. No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], no Pesquisador de Objetos, expanda **Segurança**, clique com o botão direito do mouse em **Logons**e selecione **Novo Logon**.
2. No **logon - novo** caixa de diálogo, selecione **pesquisa**.
3. Selecione o **tipos de objeto** e **grupos** caixas de seleção e desmarque todas as outras caixas de seleção.
4. Clique em **avançado**, verifique se o local de pesquisa é o computador atual e clique **Localizar agora**.
5. Percorra a lista de contas de grupo no servidor até encontrar um que começa com `SQLRUserGroup`.
    
    + O nome do grupo associada com o serviço barra inicial para o _instância padrão_ é sempre apenas **SQLRUserGroup**. Selecione esta conta somente para a instância padrão.
    + Se você estiver usando um _instância nomeada_, o nome da instância é acrescentado ao nome padrão, `SQLRUserGroup`. Portanto, se a instância é chamada "MLTEST", o nome do grupo de usuário padrão para esta instância seria **SQLRUserGroupMLTest**.
5. Clique em **Okey** para fechar a caixa de diálogo de pesquisa avançada e verifique se você selecionou a conta correta para a instância. Cada instância pode usar seu próprio serviço de barra inicial e o grupo criado para esse serviço.
6. Clique em **Okey** mais uma vez para fechar o **Selecionar usuário ou grupo** caixa de diálogo.
7. No **logon - novo** caixa de diálogo, clique em **Okey**. Por padrão, o logon é atribuído à função **pública** e tem permissão para se conectar ao mecanismo de banco de dados.

### <a name="bkmk_AllowLogon"></a>Conceder aos usuários permissão para executar scripts externos

> [!NOTE]
> Se você usar um logon do SQL para executar scripts R em um contexto de computação do SQL Server, esta etapa não será necessária.

Se você instalou [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em sua própria instância, normalmente você está executando scripts como administrador, ou pelo menos um proprietário de banco de dados, e, portanto, têm permissões implícitas para várias operações, todos os dados no banco de dados e a capacidade de instalar novos pacotes conforme necessário.

No entanto, em um cenário de enterprise, a maioria dos usuários, incluindo os usuários que acessam o banco de dados usando os logons do SQL Server, não tem tais permissões elevadas. Portanto, para cada usuário que executará scripts R, você deve conceder as permissões de usuário para executar scripts em cada banco de dados onde scripts externos serão usados.

```SQL
USE <database_name>
GO
GRANT EXECUTE ANY EXTERNAL SCRIPT  TO [UserName]
```

> [!TIP]
> Precisa de ajuda com a instalação? Não tem certeza de que executou todas as etapas? Use esses relatórios personalizados para verificar o status da instalação e executar etapas adicionais. 
> 
> [Monitorar os serviços de aprendizado de máquina usando relatórios personalizados](../r/monitor-r-services-using-custom-reports-in-management-studio.md).

### <a name="permissions-db"></a> Dar aos usuários de leitura, gravação ou permissões de DDL para o banco de dados

A conta de usuário que é usada para executar R pode precisar para ler dados de outros bancos de dados, criar novas tabelas para armazenar os resultados e gravar dados em tabelas. Portanto, para cada usuário que estará executando scripts de R, certifique-se de que o usuário tem as permissões apropriadas no banco de dados: *db_datareader*, *db_datawriter*, ou *db_ddladmin*.

Por exemplo, a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] a seguir concede ao logon SQL *MySQLLogin* os direitos para executar consultas T-SQL no banco de dados *RSamples* . Para executar essa instrução, o logon SQL já deve existir no contexto de segurança do servidor.

```SQL
USE RSamples
GO
EXEC sp_addrolemember 'db_datareader', 'MySQLLogin'
```

Para obter mais informações sobre as permissões incluídas em cada função, consulte [funções de nível de banco de dados](../../relational-databases/security/authentication-access/database-level-roles.md).


### <a name="create-an-odbc-data-source-for-the-instance-on-your-data-science-client"></a>Criar uma fonte de dados ODBC para a instância no cliente de ciência de dados

Se você cria uma solução R em um computador de cliente de ciência de dados e precisa executar o código usando o computador do SQL Server como o contexto de computação, você pode usar um logon do SQL ou a autenticação integrada do Windows.

* Para logons SQL: certifique-se de que o logon tenha as permissões apropriadas no banco de dados em que os dados serão lidos. Você pode fazer isso adicionando *se conectem* e *selecione* permissões, ou adicionando o logon para o *db_datareader* função. Para logons que precisa para criar objetos, adicionar *funções DDL_admin* direitos. Para logons que devem salvar dados em tabelas, adicione o logon para o *db_datawriter* função.

* Para autenticação do Windows: talvez seja necessário configurar uma fonte de dados ODBC no cliente de ciência de dados que especifica o nome da instância e outras informações de conexão. Para obter mais informações, consulte [administrador de fonte de dados ODBC](https://docs.microsoft.com/sql/odbc/admin/odbc-data-source-administrator).

## <a name="suggested-optimizations"></a>Otimizações sugeridas

Agora que você tem que tudo funcione, você também poderá otimizar o servidor para suportar o aprendizado de máquina ou modelos de classificação de instalação.

### <a name="add-more-worker-accounts"></a>Adicionar mais contas de trabalho

Se você achar que você pode usar o R muito ou se você espera que muitos usuários scripts em execução ao mesmo tempo, você pode aumentar o número de contas de trabalho que são atribuídos ao serviço barra inicial. Para obter mais informações, consulte [modificar o pool de conta de usuário para serviços de aprendizado de máquina do SQL Server](../r/modify-the-user-account-pool-for-sql-server-r-services.md).

### <a name="bkmk_optimize"></a>Otimizar o servidor para execução de scripts externos

As configurações padrão para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalação destinam-se para otimizar o equilíbrio do servidor para uma variedade de serviços que são suportados pelo mecanismo de banco de dados, que pode incluir a extração, transformação e carregamento (ETL) processos, relatórios, auditoria, e aplicativos que usam [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dados. Portanto, as configurações padrão, você pode encontrar recursos de aprendizagem de máquina, às vezes, são restritos ou limitados, especialmente em operações com uso intensivo de memória.

Para garantir que os trabalhos de aprendizado de máquina são priorizados e recursos adequadamente, é recomendável que você use o administrador de recursos do SQL Server para configurar um pool de recursos externos. Você também poderá alterar a quantidade de memória alocada para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mecanismo de banco de dados ou aumentar o número de contas que são executados sob o [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] service.

- Para configurar um pool de recursos de gerenciamento de recursos externos, consulte [criar um pool de recursos externos](../../t-sql/statements/create-external-resource-pool-transact-sql.md).
  
- Para alterar a quantidade de memória reservada para o banco de dados, consulte [opções de configuração de memória do servidor](../../database-engine/configure-windows/server-memory-server-configuration-options.md).
  
- Para alterar o número de contas de R que pode ser iniciado por [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)], consulte [modificar o pool de conta de usuário para o aprendizado de máquina](../r/modify-the-user-account-pool-for-sql-server-r-services.md).

Se você estiver usando a Standard Edition e não possuem o administrador de recursos, você pode usar eventos estendidos e exibições de gerenciamento dinâmico (DMVs), bem como eventos do Windows monitoramento, para ajudar a gerenciar os recursos de servidor que são usados por R. Para obter mais informações, consulte [monitoramento e gerenciamento de serviços de R](../r/managing-and-monitoring-r-solutions.md).

### <a name="install-additional-r-packages"></a>Instalar pacotes R adicionais

As soluções de R que você criar para o SQL Server podem chamar funções básicas de R, funções do packes properietary instalado com o SQL Server e pacotes de R de terceiros compatíveis com a versão do código-fonte aberto R instalado pelo SQL Server.

Pacotes que você desejar usar do SQL Server deverão ser instalados na biblioteca padrão usada pela instância. Se você tiver uma instalação separada do R no computador, ou se você instalou pacotes nas bibliotecas do usuário, você não poderá usar esses pacotes do T-SQL.

O processo de instalação e gerenciamento de pacotes de R é diferente no SQL Server 2016 e 2017 do SQL Server. No SQL Server 2016, um administrador de banco de dados deve instalar os pacotes de R que os usuários precisam. No SQL Server de 2017, você pode configurar grupos de usuários para compartilhar pacotes em um nível por banco de dados ou configurar as funções de banco de dados para permitir que os usuários instalem seus próprios pacotes. Para obter mais informações, consulte [pacote de gerenciamento](../r/r-package-management-for-sql-server-r-services.md).


## <a name="get-help"></a>Obter ajuda

Precisa de ajuda com a instalação ou atualização? Para obter respostas a perguntas comuns e problemas conhecidos, consulte o seguinte artigo:

* [Atualização e instalação perguntas Frequentes – serviços de aprendizado de máquina](../r/upgrade-and-installation-faq-sql-server-r-services.md)

Para verificar o status da instalação da instância e corrigir problemas comuns, tente esses relatórios personalizados.

* [Relatórios personalizados do SQL Server R Services](../r/monitor-r-services-using-custom-reports-in-management-studio.md)

## <a name="next-steps"></a>Próximas etapas

Os desenvolvedores de R podem começar com alguns exemplos simples e conheça os fundamentos de como funciona o R com o SQL Server. Para a próxima etapa, consulte os links a seguir:

+ [Tutorial: Executar R no T-SQL](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [Tutorial: Análise de no banco de dados para os desenvolvedores de R](../tutorials/sqldev-in-database-r-for-sql-developers.md)

Para exibir exemplos de aprendizado de máquina com base em cenários do mundo real, consulte [tutoriais de aprendizado de máquina](../tutorials/machine-learning-services-tutorials.md).


