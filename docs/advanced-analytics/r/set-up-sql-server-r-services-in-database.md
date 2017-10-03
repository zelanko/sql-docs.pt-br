---
title: "Configurar serviços de aprendizado de máquina do SQL Server (no banco de dados) | Microsoft Docs"
ms.custom: 
ms.date: 09/28/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
keywords:
- instalando o SQL Server R Services
ms.assetid: 4d773c74-c779-4fc2-b1b6-ec4b4990950d
caps.latest.revision: 36
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: e76675099ab290d29231d434eb74e92b613185b7
ms.openlocfilehash: 9b3449e8c1f19ee69b36107f3530eac80fae0227
ms.contentlocale: pt-br
ms.lasthandoff: 09/29/2017

---
# <a name="set-up-sql-server-machine-learning-services-in-database"></a>Configurar serviços de aprendizado de máquina do SQL Server (no banco de dados)

Este tópico descreve como configurar os serviços de aprendizado de máquina no SQL Server usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Assistente de instalação.

**Aplica-se a:** SQL Server 2016 R Services (apenas R) SQL Server 2017 Machine Learning Services (R e Python)

## <a name="machine-learning-options-in-sql-server-setup"></a>Opções de instalação do SQL Server de aprendizado de máquina

Instalação do SQL Server fornece as seguintes opções para a instalação do aprendizado de máquina:

* Instale o aprendizado de máquina com o banco de dados do SQL Server

  Essa opção permite executar scripts de R ou Python usando um procedimento armazenado. Você também pode usar o computador do SQL Server como um contexto de computação remota para os scripts de R ou Python que são executados em uma conexão externa.

  Para instalar esta opção:
  
  * No SQL Server 2016, selecione **R Services (no banco de dados)**.
  * No SQL Server de 2017, selecione **serviços de aprendizado de máquina (no banco de dados)**.


* Instalar um servidor de aprendizado de máquina autônomo

  Esta opção cria um ambiente de desenvolvimento para soluções que não exigem nem usar o SQL Server de aprendizado de máquina. Portanto, geralmente recomendamos que você instale essa opção em um computador diferente do SQL Server em uma hospedagem. Para obter mais informações sobre essa opção, consulte [criar um Standalone R Server](../r/create-a-standalone-r-server.md).

O processo de instalação requer várias etapas, alguns dos quais são opcionais. Os aspectos opcionais dependem tanto como você planeja usar o aprendizado de máquina e o status do seu ambiente de segurança. 

## <a name="bkmk_prereqs"></a> Pré-requisitos

*  Evite instalar os serviços de R e R Server ao mesmo tempo. Normalmente, você deve instalar o R Server (autônomo) para criar um ambiente em que um cientista de dados ou o desenvolvedor usa para se conectar ao SQL Server e implantar soluções de R. Portanto, não é necessário instalar ambos no mesmo computador.

* Se você usou as versões anteriores do pacotes RevoScaleR ou o ambiente de desenvolvimento do Revolution Analytics, ou se você instalou as versões de pré-lançamento do SQL Server 2016, você deve desinstalá-los. Não há suporte para a instalação lado a lado. Para obter ajuda sobre como remover versões anteriores, consulte [atualização e perguntas frequentes sobre a instalação do SQL Server R Services](../r/upgrade-and-installation-faq-sql-server-r-services.md).

* Você não pode instalar os serviços de aprendizado de máquina em um cluster de failover. O motivo é que o mecanismo de segurança que é usado para isolar processos de script externo não é compatível com um ambiente de cluster de failover do Windows Server. Como alternativa, você pode fazer o seguinte:
    * Use a replicação para copiar tabelas necessárias para uma instância autônoma do SQL Server R Services.
    * Instalar [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] em um computador autônomo que usa o AlwaysOn e é parte de um grupo de disponibilidade.

> [!IMPORTANT]
> Após a conclusão da instalação, algumas etapas adicionais são necessárias para habilitar a recurso de aprendizado de máquina. Você pode também precisa conceder aos usuários permissões para bancos de dados específicos, alterar ou configurar contas de ou configurar um cliente de ciência de dados remotos.

##  <a name="bkmk_installExt"></a>Etapa 1: Instalar os recursos de extensibilidade e escolher uma idioma de aprendizado de máquina

Para usar o aprendizado de máquina, você deve instalar o SQL Server 2016 ou posterior. Para usar [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], pelo menos uma instância do mecanismo de banco de dados é necessária. Você pode usar uma instância padrão ou nomeada.

1. Execute a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .
  
    Para obter informações sobre como fazer instalações autônomas, consulte [autônomo instalado do SQL Server R Services](../r/unattended-installs-of-sql-server-r-services.md).
  
2. Sobre o **instalação** guia, selecione **instalação autônoma do novo SQL Server ou adicionar recursos a uma instalação existente**.
   
3. Sobre o **seleção de recursos** trabalhos de página, para instalar os serviços de banco de dados usados por R e instala as extensões que oferecem suporte a scripts e processos externos, selecione as seguintes opções:
   
   **SQL Server 2016**
   - Selecione **serviços do mecanismo de banco de dados**.
   - Selecione **R Services (no banco de dados)**.

   **SQL Server 2017**
   - Selecione **serviços do mecanismo de banco de dados**.
   - Selecione **Services (no banco de dados) de aprendizado de máquina**.
   - Selecione pelo menos um idioma para habilitar de aprendizado de máquina. Você pode selecionar apenas R, ou você pode adicionar o R e Python.
   
   > [!NOTE]
   > Se você não selecionar opções de idioma de R ou Python, o Assistente de instalação instala apenas o framework de extensibilidade, que inclui confiável Launchpad do SQL Server, mas não instala todos os componentes específicos do idioma. Essa opção é para associação a instância do SQL Server em R ou Python como parte da política de ciclo de vida modernos de Microsoft. Para obter mais informações, consulte [SqlBindR de uso para atualizar uma instância dos serviços do R](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).

4.  Sobre o **consentimento para instalar o Microsoft R Open** página, selecione **aceitar**.
  
     Este contrato de licença é necessário para baixar o Microsoft R Open, que inclui uma distribuição dos pacotes de base de R de código-fonte aberto e ferramentas, junto com pacotes de R aprimorados e provedores de conectividade da equipe de desenvolvimento do Microsoft R.
  
    > [!NOTE]
    >  Se o computador que você está usando não tiver acesso à internet, você pode pausar o programa de instalação neste momento para baixar os instaladores separadamente, conforme descrito em [componentes instalar R sem acesso à internet](installing-ml-components-without-internet-access.md).
  
5. Selecione **Avançar**.

6. Sobre o **pronto para instalar** página, verifique se os seguintes itens são incluídos e, em seguida, selecione **instalar**.

   **SQL Server 2017**
   - Serviços do Mecanismo de Banco de Dados
   - Serviços de Machine Learning (No Banco de Dados)
   - R, Python ou ambos

   **SQL Server 2016**
   - Serviços do Mecanismo de Banco de Dados
   - R Services (no banco de dados)

7. Quando a instalação for concluída, reinicie o computador.

##  <a name="bkmk_enableFeature"></a>Etapa 2: Habilitar serviços de script externo

1. Abra o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Se ele ainda não estiver instalado, execute novamente o assistente de instalação do SQL Server para abrir um link de download e instalá-lo.
  
2. Conecte-se à instância onde você instalou o aprendizado de máquina e, em seguida, execute o seguinte comando:

   ```SQL
   sp_configure
   ```

    O valor para o **scripts externos habilitados** propriedade agora deve ser **0**. Isso ocorre porque o recurso está desativado por padrão para reduzir a área da superfície e ele deve ser habilitado explicitamente por um administrador.
     
3. Para habilitar o recurso de script externo, execute a seguinte instrução:
  
    ```SQL
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    ```
  
4. Reinicie o serviço SQL Server da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Reiniciar o serviço do SQL Server também automaticamente reinicia relacionado [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] serviço.

    Você pode reiniciar o serviço usando o **serviços** painel no painel de controle ou usando o SQL Server Configuration Manager.

## <a name="bkmk_TestScript"></a>Etapa 3: Verifique se a execução do script funciona localmente

Verifique se o serviço de execução do script externo está habilitado.

1. No SQL Server Management Studio, abra uma nova **consulta** janela e, em seguida, execute o seguinte comando:
  
    ```SQL
    EXEC sp_configure  'external scripts enabled'
    ```
    O **run_value** agora deve ser definido como 1.
    
2. Abra o **serviços** painel e verificar se o serviço barra inicial para a instância está em execução. Se você instalar várias instâncias, cada instância terá seu próprio serviço Launchpad.
   
3. Abra uma nova **consulta** janela no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], e, em seguida, executar um script R simples como o seguinte:
  
    ```SQL
    EXEC sp_execute_external_script  @language =N'R',
    @script=N'
    OutputDataSet <- InputDataSet;
    ',
    @input_data_1 =N'SELECT 1 AS hello'
    WITH RESULT SETS (([hello] int not null));
    GO
    ```
  
    **Resultados**
  
    *Olá* *1*
  
   Se o comando for executado sem erro, vá para as próximas etapas. Se você receber um erro, para obter uma lista de alguns problemas comuns, consulte [perguntas frequentes sobre atualização e instalação](../r/upgrade-and-installation-faq-sql-server-r-services.md).

## <a name="bkmk_FollowUp"></a>Etapa 4: Configuração adicional

Dependendo de seu caso de uso para R ou Python, você precisará fazer alterações adicionais para o servidor, o firewall, as contas usadas pelo serviço ou permissões de banco de dados. As alterações que você deve fazer variam de acordo com o caso.

Cenários comuns que exigem alterações adicionais incluem:

* Alterando regras de firewall para permitir conexões de entrada para o SQL Server.
* Habilitando protocolos de rede adicionais.
* Garantir que o servidor oferece suporte a conexões remotas.
* Habilitando *autenticação implícita*, se os usuários acessem dados do SQL Server de um terminal de desenvolvimento R remoto e executar código R usando o pacote RODBC ou outro provedor do Microsoft ODBC Open Database Connectivity ().
* Dando aos usuários permissões para executar o script R ou usar bancos de dados.
* Corrigindo problemas de segurança que impede a comunicação com o serviço Launchpad.
* Garantir que os usuários têm permissão para executar o código R ou instalar pacotes.

> [!NOTE]
> Nem todas as alterações listadas podem ser necessárias. No entanto, é recomendável que você examine todos os itens para ver se elas forem aplicáveis ao seu cenário.

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

Se você instalou [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e executam scripts R em sua própria instância, normalmente você está executando scripts como administrador, ou pelo menos um proprietário de banco de dados, e, portanto, têm permissões implícitas para várias operações, todos os dados no banco de dados e a capacidade Para instalar novos pacotes de R como necessário.

No entanto, em um cenário de enterprise, a maioria dos usuários, incluindo os usuários que acessam o banco de dados usando os logons do SQL Server, não tem tais permissões elevadas. Portanto, para cada usuário que serão executados scripts de R ou Python, você deve conceder as permissões de usuário para executar scripts em cada banco de dados onde scripts externos serão usados.

```SQL
USE <database_name>
GO
GRANT EXECUTE ANY EXTERNAL SCRIPT  TO [UserName]
```

> [!TIP]
> Precisa de ajuda com a instalação? Não tem certeza de que executou todas as etapas? Use esses relatórios personalizados para verificar o status de instalação do R Services. Para obter mais informações, consulte [Monitorar o R Services usando relatórios personalizados](monitor-r-services-using-custom-reports-in-management-studio.md).

### <a name="ensure-that-the-sql-server-computer-supports-remote-connections"></a>Certifique-se de que o computador do SQL Server oferece suporte a conexões remotas

Se você não pode conectar-se de um computador remoto, verifique se o servidor permite conexões remotas. Conexões remotas às vezes são desabilitadas por padrão.

Também verifique se o firewall permite o acesso ao SQL Server. Por padrão, a porta usada pelo SQL Server geralmente é bloqueada pelo firewall. Se você estiver usando o Firewall do Windows, consulte [configurar o Firewall do Windows para acesso ao mecanismo de banco de dados](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md).

### <a name="give-your-users-read-write-or-ddl-permissions-to-the-database"></a>Dar aos usuários de leitura, gravação ou permissões de DDL para o banco de dados

Enquanto ele estiver em execução de scripts R, a conta de usuário ou logon SQL pode precisar para ler dados de outros bancos de dados, criar novas tabelas para armazenar os resultados e gravar dados em tabelas.

Para cada conta de usuário ou logon SQL que estará executando scripts de R, não se esqueça de que a conta ou logon tem as permissões apropriadas no banco de dados: *db_datareader*, *db_datawriter*, ou  *db_ddladmin*.

Por exemplo, a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] a seguir concede ao logon SQL *MySQLLogin* os direitos para executar consultas T-SQL no banco de dados *RSamples* . Para executar essa instrução, o logon SQL já deve existir no contexto de segurança do servidor.

```SQL
USE RSamples
GO
EXEC sp_addrolemember 'db_datareader', 'MySQLLogin'
```

Para obter mais informações sobre as permissões incluídas em cada função, consulte [funções de nível de banco de dados](../../relational-databases/security/authentication-access/database-level-roles.md).

### <a name="use-machine-learning-in-an-azure-vm"></a>Usar o aprendizado de máquina em uma VM do Azure

Se você instalou os serviços de aprendizado de máquina (ou R Services) em uma máquina virtual do Azure, você precisará alterar alguns padrões adicionais. Para obter mais informações, consulte [instalar o aprendizado de máquina do SQL Server em uma máquina virtual do Azure](installing-sql-server-r-services-on-an-azure-virtual-machine.md).

### <a name="create-an-odbc-data-source-for-the-instance-on-your-data-science-client"></a>Criar uma fonte de dados ODBC para a instância no cliente de ciência de dados

Se você cria uma solução R em um computador de cliente de ciência de dados e precisa executar o código usando o computador do SQL Server como o contexto de computação, você pode usar um logon do SQL ou a autenticação integrada do Windows.

* Para logons SQL: certifique-se de que o logon tenha as permissões apropriadas no banco de dados em que os dados serão lidos. Você pode fazer isso adicionando *se conectem* e *selecione* permissões, ou adicionando o logon para o *db_datareader* função. Para logons que precisa para criar objetos, adicionar *funções DDL_admin* direitos. Para logons que devem salvar dados em tabelas, adicione o logon para o *db_datawriter* função.

* Para autenticação do Windows: talvez seja necessário configurar uma fonte de dados ODBC no cliente de ciência de dados que especifica o nome da instância e outras informações de conexão. Para obter mais informações, consulte [administrador de fonte de dados ODBC](https://docs.microsoft.com/sql/odbc/admin/odbc-data-source-administrator).

## <a name="next-steps"></a>Próximas etapas

Após ter verificado que o recurso de execução do script funciona no SQL Server, você pode executar comandos de R e Python do SQL Server Management Studio, o código do Visual Studio ou qualquer outro cliente que pode enviar instruções T-SQL para o servidor.

No entanto, você talvez queira fazer algumas alterações à configuração do sistema para dar suporte a um uso intenso do aprendizado de máquina, ou adicionar novos pacotes de R.

Esta seção lista algumas modificações comuns que você pode fazer para dar suporte ao aprendizado de máquina.

### <a name="add-more-worker-accounts"></a>Adicionar mais contas de trabalho

Se você achar que você pode usar o R muito ou se você espera que muitos usuários scripts em execução ao mesmo tempo, você pode aumentar o número de contas de trabalho que são atribuídos ao serviço barra inicial. Para obter mais informações, consulte [modificar o pool de conta de usuário do SQL Server R Services](modify-the-user-account-pool-for-sql-server-r-services.md).

### <a name="bkmk_optimize"></a>Otimizar o servidor para execução de scripts externos

As configurações padrão para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalação destinam-se para otimizar o equilíbrio do servidor para uma variedade de serviços que são suportados pelo mecanismo de banco de dados, que pode incluir a extração, transformação e carregamento (ETL) processos, relatórios, auditoria, e aplicativos que usam [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dados. Portanto, as configurações padrão, você pode encontrar recursos de aprendizagem de máquina, às vezes, são restritos ou limitados, especialmente em operações com uso intensivo de memória.

Para garantir que os trabalhos de aprendizado de máquina são priorizados e recursos adequadamente, é recomendável que você use o administrador de recursos do SQL Server para configurar um pool de recursos externos. Você também poderá alterar a quantidade de memória alocada para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mecanismo de banco de dados ou aumentar o número de contas que são executados sob o [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] service.

- Para configurar um pool de recursos de gerenciamento de recursos externos, consulte [criar um pool de recursos externos](../../t-sql/statements/create-external-resource-pool-transact-sql.md).
  
- Para alterar a quantidade de memória reservada para o banco de dados, consulte [opções de configuração de memória do servidor](../../database-engine/configure-windows/server-memory-server-configuration-options.md).
  
- Para alterar o número de contas de R que pode ser iniciado por [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)], consulte [modificar o pool de conta de usuário para o aprendizado de máquina](modify-the-user-account-pool-for-sql-server-r-services.md).

Se você estiver usando a Standard Edition e não possuem o administrador de recursos, você pode usar eventos estendidos e exibições de gerenciamento dinâmico (DMVs), bem como eventos do Windows monitoramento, para ajudar a gerenciar os recursos de servidor que são usados por R. Para obter mais informações, consulte [monitoramento e gerenciamento de serviços de R](managing-and-monitoring-r-solutions.md).

### <a name="install-additional-r-packages"></a>Instalar pacotes R adicionais

Reserve um minuto para instalar quaisquer pacotes R adicionais que você está usando.

Pacotes que você desejar usar do SQL Server deverão ser instalados na biblioteca padrão usada pela instância. Se você tiver uma instalação separada do R no computador, ou se você instalou pacotes nas bibliotecas do usuário, você não poderá usar esses pacotes do T-SQL. Para obter mais informações, consulte [instalar pacotes R adicionais no SQL Server](../../advanced-analytics/r-services/install-additional-r-packages-on-sql-server.md).

Você também pode configurar grupos de usuários para compartilhar pacotes em um nível por banco de dados ou configurar as funções de banco de dados para permitir que os usuários instalem seus próprios pacotes. Para obter mais informações, consulte [pacote de gerenciamento](r-package-management-for-sql-server-r-services.md).

### <a name="upgrade-the-machine-learning-components"></a>Atualizar a componentes de aprendizado de máquina

Quando você instala os serviços de R usando o SQL Server 2016, você pode obter a versão dos componentes de R que foi atualizada quando a versão ou service pack foi publicado. Cada vez que você corrigir ou atualiza o servidor, os componentes de aprendizado de máquina são atualizados também.

No entanto, você pode atualizar a componentes em um agendamento mais rápido do que há suporte para de aprendizado de máquina por versões do SQL Server, instalando o Microsoft R Server e a instância de associação. Ao atualizar, você também obtém os seguintes recursos novos, que têm suporte em versões recentes do Microsoft R Server:

* Novos pacotes de R, incluindo [sqlrutils](https://docs.microsoft.com/r-server/r-reference/sqlrutils/sqlrutils), [olapR](https://docs.microsoft.com/r-server/r-reference/olapr/olapr), e [MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package).
* [Modelos de classificação](https://docs.microsoft.com/r-server/install/microsoftml-install-pretrained-models) para análise de texto e de classificação de imagem.

Para obter informações sobre como atualizar uma instância do SQL Server 2016, consulte [componentes de R de atualização por meio da associação](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).

Se você não tiver certeza de qual versão do R está associado com a instância, você pode executar um comando como o seguinte:

```SQL
EXEC sp_execute_external_script  @language =N'R',
@script=N'
myvar <- version$version.string
OutputDataSet <- as.data.frame(myvar);'
```

> [!NOTE]
> Atualizações através do processo de associação terá suporte para SQL Server 2017 também. No entanto, atualmente há suporte para atualizações somente para instâncias do SQL Server 2016.

### <a name="tutorials"></a>Tutoriais

Para começar com alguns exemplos simples e conheça os fundamentos de como funciona o R com o SQL Server, consulte [código R usando Transact-SQL](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md).

Para exibir exemplos de aprendizado de máquina com base em cenários do mundo real, consulte [tutoriais de aprendizado de máquina](../tutorials/machine-learning-services-tutorials.md).

### <a name="troubleshooting"></a>Solução de problemas

Está tendo problemas? Tentando atualizar? Para obter respostas a perguntas comuns e problemas conhecidos, consulte o seguinte artigo:

* [Atualização e instalação perguntas Frequentes – serviços de aprendizado de máquina](upgrade-and-installation-faq-sql-server-r-services.md)

Para verificar o status da instalação da instância e corrigir problemas comuns, tente esses relatórios personalizados.

* [Relatórios personalizados do SQL Server R Services](monitor-r-services-using-custom-reports-in-management-studio.md)

