---
title: "Configurar serviços de aprendizado de máquina do SQL Server (no banco de dados) | Microsoft Docs"
ms.custom: 
ms.date: 11/15/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
keywords:
- instalando o SQL Server R Services
- "Instalando serviços de aprendizado de máquina do SQL Server"
- "Configurar os serviços de R"
- "instalar o aprendizado de máquina do SQL"
ms.assetid: 4d773c74-c779-4fc2-b1b6-ec4b4990950d
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Active
ms.openlocfilehash: 4d18a45b40c7f80ae2b46514f6c8245b80f6b142
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2018
---
# <a name="set-up-sql-server-machine-learning-services-in-database"></a>Configurar serviços de aprendizado de máquina do SQL Server (no banco de dados)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este tópico descreve como instalar e configurar a seguinte recursos que oferecem suporte à análise no banco de dados no SQL Server de aprendizado de máquina:

+ **SQL Server 2016 R Services (no banco de dados)**. Se você tiver o SQL Server 2016, instale esse recurso para habilitar a execução do código R no SQL Server. Requer o mecanismo de banco de dados.

    [Configurar o aprendizado de máquina no SQL Server 2016](#bkmk_2016top)

+ **Serviços de aprendizado de máquina do SQL Server de 2017 (no banco de dados)**. Se você tiver o SQL Server 2017, instalá-lo para executar código R (ou Python) no SQL Server. Requer o mecanismo de banco de dados. 

    [Configurar o aprendizado de máquina no SQL Server 2017](#bkmk_2017top)

+ Um servidor de aprendizado de máquina com **sem** do SQL Server

    [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a instalação também inclui a opção para instalar uma versão de "autônomo" da componentes de aprendizado de máquina que não exigem o mecanismo de banco de dados e não será executado no SQL Server.  Geralmente, é recomendável que você instale essa opção em um computador diferente do computador que hospeda o SQL Server.
    
    [Configurar um servidor autônomo aprendizado de máquina](create-a-standalone-r-server.md).

Este artigo descreve o processo de instalação que usa o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Assistente de instalação. Para a instalação de linha de comando, ou para baixar os instaladores para usar em servidores offline, consulte estes artigos:

+ [Instalar o R para o SQL Server na linha de comando](unattended-installs-of-sql-server-r-services.md)
+ [Instalar o Python para o SQL Server na linha de comando](../python/unattended-installs-of-sql-server-python-services.md)
+ [Instalar um servidor de aprendizado de máquina autônomo da linha de comando](install-microsoft-r-server-from-the-command-line.md)
+ [Instalar componentes de aprendizado de máquina em um servidor sem ACEs de internet](installing-ml-components-without-internet-access.md)

**Aplica-se a:** do SQL Server 2016, SQL Server de 2017

## <a name="bkmk_prereqs"></a> Pré-instalação

+ Machine learning no banco de dados requer o SQL Server 2016 ou posterior. 

+ Idiomas com suporte: 

    + SQL Server 2016 dá suporte a R somente. 

    + R também está disponível como um recurso de visualização no banco de dados SQL Azure, com algumas limitações. Para obter mais informações, consulte [usando R no banco de dados do SQL Azure](using-r-in-azure-sql-database.md)

    + Para usar o Python requer o SQL Server 2017 ou posterior.

+ Se você usou as versões anteriores do pacotes RevoScaleR ou o ambiente de desenvolvimento do Revolution Analytics, ou se você instalou as versões de pré-lançamento do SQL Server 2016, você deve desinstalá-los. Não há suporte para a instalação lado a lado. Para obter ajuda sobre como remover versões anteriores, consulte [atualização e perguntas Frequentes de instalação de serviços de aprendizado de máquina do SQL Server](../r/upgrade-and-installation-faq-sql-server-r-services.md).

+ Não é possível instalar o SQL Server 2016 R Services ou serviços de aprendizado de máquina do SQL Server 2017 em um controlador de domínio. A parte de R Services ou serviços de aprendizado de máquina do programa de instalação falhará.

+ Você não pode instalar a recursos em um cluster de failover do aprendizado de máquina. O mecanismo de segurança que é usado para isolar processos de script externo não é compatível com um ambiente de cluster de failover do Windows Server. Como alternativa, você pode fazer o seguinte:
    * Use a replicação para copiar tabelas necessárias para uma instância do SQL Server com o aprendizado de máquina habilitado.
    * Instale o aprendizado de máquina em um computador autônomo que usa o AlwaysOn e é parte de um grupo de disponibilidade.

+ A estrutura de aprendizado de máquina requer configuração adicional após a conclusão da instalação. As etapas exatas dependem de sua organização e políticas de segurança, configuração do servidor e os usuários pretendidos. É recomendável que você examine todas as etapas e determinar a configuração adicional que pode ser necessário em seu ambiente.

## <a name="bkmk2016top"></a>Instalar o SQL Server 2016 R Services (no banco de dados)

> [!div class="checklist"]
> * Instalar o mecanismo de banco de dados e recursos de aprendizado de máquina
> * Necessárias etapas de pós-instalação: habilitar o aprendizado de máquina e reiniciar
> * Etapas de pós-instalação opcionais: adicionar regras de firewall, os usuários de adicionar, alterar ou configurar contas de serviço, configurar um cliente de ciência de dados remotos

**Usando o Assistente de instalação do SQL Server 2016**

1. Execute o assistente de instalação do SQL Server.

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
  
    Se o computador que você está usando não tiver acesso à internet, você pode pausar o programa de instalação neste momento para baixar os instaladores separadamente, conforme descrito em [componentes instalar R sem acesso à internet](installing-ml-components-without-internet-access.md).
  
5. Depois que você aceitou o contrato de licença, há uma pequena pausa enquanto o instalador está preparado. Clique em **próximo** quando o botão ficará disponível.

6. Sobre o **pronto para instalar** página, verifique se os seguintes itens são incluídos e, em seguida, selecione **instalar**.

   + Serviços do Mecanismo de Banco de Dados
   + R Services (no Banco de Dados)

7. Quando a instalação for concluída, reinicie o computador.


## <a name="bkmk2017top"></a>Instale os serviços de aprendizado de máquina do SQL Server de 2017 (no banco de dados)

> [!div class="checklist"]
> * Instalar o mecanismo de banco de dados e recursos de aprendizado de máquina
> * Necessárias etapas de pós-instalação: habilitar o aprendizado de máquina e reiniciar
> * Etapas de pós-instalação opcionais: adicionar regras de firewall, os usuários de adicionar, alterar ou configurar contas de serviço, configurar um cliente de ciência de dados remotos.

**Introdução**

1. Execute a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .
  
2. Sobre o **instalação** guia, selecione **instalação autônoma do novo SQL Server ou adicionar recursos a uma instalação existente**.

     ![Instalar serviços de aprendizado de máquina (no banco de dados)](media/2017setup-installation-page-mlsvcs.png "Iniciar instalação do mecanismo de banco de dados com serviços de aprendizado de máquina")

3. Sobre o **seleção de recursos** , selecione as seguintes opções:
   
    + Selecione **serviços do mecanismo de banco de dados**. O mecanismo de banco de dados é necessário em cada instância que usa o aprendizado de máquina.

    + Selecione **Services (no banco de dados) de aprendizado de máquina**. Esta opção instala o suporte para uso no banco de dados de R. Depois de selecionar essa opção, você pode selecionar a idioma de aprendizado de máquina. Você pode selecionar apenas R, ou você pode adicionar o R e Python.
   
    ![Seleção de recursos de serviços de aprendizado de máquina](media/2017setup-features-page-mls-rpy.png "selecione esses recursos para R Services no banco de dados")

    Se você não selecionar opções de idioma de R ou Python, o Assistente de instalação instala apenas o framework de extensibilidade, que inclui a barra inicial do SQL Server confiável e não instala todos os componentes específicos do idioma.  Em geral, recomendamos que você instale pelo menos um idioma inicial. No entanto, você pode usar essa opção se você pretende usar imediatamente o processo de ligação para atualizar a componentes de aprendizado de máquina. Para obter mais informações, consulte [SqlBindR de uso para atualizar uma instância dos serviços do R](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).

    É recomendável que você **não** instalar os recursos autônomo e no banco de dados no mesmo computador e nunca instalá-los ao mesmo tempo. Normalmente instalaria Server de aprendizado de máquina (autônomo) para criar um ambiente em que um cientista de dados ou o desenvolvedor usa para se conectar ao SQL Server durante a implantação de soluções. Portanto, não é necessário instalar ambos no mesmo computador.

4.  Contratos de aprendizado de máquina de licença: dependendo de quais idiomas que você está instalando, você deve aceitar os contratos de licença para R, Python ou ambos.

    + Termos de licença para este contrato de licença de r: abrange Microsoft R Open, que inclui uma distribuição das ferramentas, junto com pacotes de R aprimorados e provedores de conectividade da equipe de desenvolvimento da Microsoft e pacotes de base de R de código-fonte aberto.
  
    + Termos de licença para Python. O contrato de licença de software livre de Python também aborda Anaconda e ferramentas relacionadas, além de algumas novas bibliotecas Python da equipe de desenvolvimento da Microsoft.

    Clique em **aceitar** para indicar seu contrato. Há uma pequena pausa, enquanto os componentes são preparados, em seguida, o **próximo** botão fica disponível.

    Se o computador que você está usando não tiver acesso à internet, você pode pausar o programa de instalação neste momento para baixar os instaladores separadamente, conforme descrito aqui: [instalar componentes de aprendizado de máquina sem acesso à internet](installing-ml-components-without-internet-access.md).

6. Sobre o **pronto para instalar** página, verifique se os seguintes itens são incluídos e, em seguida, selecione **instalar**.

   - Serviços do Mecanismo de Banco de Dados
   - Serviços de Machine Learning (No Banco de Dados)
   - R, Python ou ambos

7. Quando a instalação for concluída, anote o local do log de instalação e, em seguida, reinicie o computador.

###  <a name="bkmk_enableFeature"></a>Etapa pós-instalação necessária

Por motivos de segurança, o recurso de aprendizado de máquina não é habilitado por padrão mesmo que o recurso foi instalado. Um administrador de servidor deve habilitar o recurso e reinicie a instância. 

Esta seção descreve como reconfigurar a instância para o aprendizado de máquina. Configuração define as contas de serviço externo e inicia o serviço barra inicial.

1. Abra o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Se ele ainda não estiver instalado, execute novamente o assistente de instalação do SQL Server para abrir um link de download e instalá-lo.
  
2. Conecte-se à instância onde você instalou o aprendizado de máquina e, em seguida, execute o seguinte comando:

   ```SQL
   sp_configure
   ```

    Procure o valor da **scripts externos habilitados** propriedade, que deve ser **0**. Isso ocorre porque o recurso está desativado por padrão para reduzir a área da superfície.
     
3. Para habilitar o recurso de script externo, execute a seguinte instrução:
  
    ```SQL
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    ```
  
4. Reinicie o serviço SQL Server da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Reiniciar o serviço do SQL Server também automaticamente reinicia relacionado [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] serviço.

    Você pode reiniciar o serviço usando o **serviços** painel no painel de controle ou usando o SQL Server Configuration Manager.

5. Para verificar se o serviço de execução do script externo está habilitado no SQL Server Management Studio, abra uma nova **consulta** janela e, em seguida, execute o seguinte comando:
  
    ```SQL
    EXEC sp_configure  'external scripts enabled'
    ```
    O **run_value** agora deve ser definido como 1.
    
6. Abra o **serviços** painel e verificar se o serviço barra inicial para a instância está em execução. Se você instalar várias instâncias, cada instância terá seu próprio serviço Launchpad.

7. É recomendável executar um script simple para verificar se os tempos de execução de script externos podem se comunicar com o SQL Server. 

    Abra uma nova **consulta** janela no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], e, em seguida, executar um script como o seguinte:
    
    + Para R
    
    ```SQL
    EXEC sp_execute_external_script  @language =N'R',
    @script=N'
    OutputDataSet <- InputDataSet;
    ',
    @input_data_1 =N'SELECT 1 AS hello'
    WITH RESULT SETS (([hello] int not null));
    GO
    ```

    + Para Python
    
    ```SQL
    EXEC sp_execute_external_script  @language =N'Python',
    @script=N'
    OutputDataSet = InputDataSet;
    ',
    @input_data_1 =N'SELECT 1 AS hello'
    WITH RESULT SETS (([hello] int not null));
    GO
    ```

    O script pode demorar um pouco enquanto para ser executado na primeira vez que o tempo de execução do script externo é carregado. Os resultados devem ser algo assim:

    | hello |
    |----|
    | 1|


8. Se você obtiver erros, vá para a seção que descreve as alterações de outros, opcionais que você talvez precise fazer após a conclusão da instalação, ou consulte o guia de solução de problemas:

    + [Etapas de pós-instalação opcionais: configurar o serviço e permissões](#bkmk_FollowUp) 
    + [Solucionando problemas de aprendizado de máquina no SQL Server](upgrade-and-installation-faq-sql-server-r-services.md)

## <a name="bkmk_FollowUp"></a>Etapas de pós-instalação opcionais

Dependendo de seu caso de uso para o aprendizado de máquina, você precisará fazer alterações adicionais para o servidor, o firewall, as contas usadas pelo serviço ou permissões de banco de dados. As alterações que você deve fazer variam de acordo com o caso.

Cenários comuns que exigem alterações adicionais incluem:

* Alterando regras de firewall para permitir conexões de entrada para o SQL Server.
* Habilitando protocolos de rede adicionais.
* Garantir que o servidor oferece suporte a conexões remotas.
* Habilitando *autenticação implícita*, se os usuários acessem dados do SQL Server de um cliente de ciência de dados remoto e executar código usando o pacote RODBC ou outro provedor ODBC.
* Dando aos usuários acesso a bancos de dados individuais.
* Corrigindo problemas de segurança que impede a comunicação com o serviço Launchpad.
* Garantir que os usuários têm permissão para executar o código ou instalar pacotes.

> [!NOTE]
> Nem todas as alterações listadas podem ser necessárias. No entanto, é recomendável que você examine todos os itens para ver se elas forem aplicáveis ao seu cenário.

Dicas de solução de problemas adicionais podem ser encontradas aqui: [perguntas frequentes sobre atualização e instalação](../r/upgrade-and-installation-faq-sql-server-r-services.md)

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

No entanto, em um cenário de enterprise, a maioria dos usuários, incluindo os usuários que acessam o banco de dados usando os logons do SQL Server, não tem tais permissões elevadas. Portanto, para cada usuário que serão executados scripts de R ou Python, você deve conceder as permissões de usuário para executar scripts em cada banco de dados onde scripts externos serão usados.

```SQL
USE <database_name>
GO
GRANT EXECUTE ANY EXTERNAL SCRIPT  TO [UserName]
```

> [!TIP]
> Precisa de ajuda com a instalação? Não tem certeza de que executou todas as etapas? Use esses relatórios personalizados para verificar o status da instalação e executar etapas adicionais. 
> 
> [Monitorar os serviços de aprendizado de máquina usando relatórios personalizados](monitor-r-services-using-custom-reports-in-management-studio.md).

### <a name="ensure-that-the-sql-server-computer-supports-remote-connections"></a>Certifique-se de que o computador do SQL Server oferece suporte a conexões remotas

Se você não pode conectar-se de um computador remoto, verifique se o servidor permite conexões remotas. Conexões remotas às vezes são desabilitadas por padrão.

Também verifique se o firewall permite o acesso ao SQL Server. Por padrão, a porta usada pelo SQL Server geralmente é bloqueada pelo firewall. Se você estiver usando o Firewall do Windows, consulte [configurar o Firewall do Windows para acesso ao mecanismo de banco de dados](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md).

### <a name="give-your-users-read-write-or-ddl-permissions-to-the-database"></a>Dar aos usuários de leitura, gravação ou permissões de DDL para o banco de dados

A conta de usuário que é usada para executar R ou Python pode precisar para ler dados de outros bancos de dados, criar novas tabelas para armazenar os resultados e gravar dados em tabelas. Portanto, para cada usuário que estará executando scripts de R ou Python, certifique-se de que o usuário tem as permissões apropriadas no banco de dados: *db_datareader*, *db_datawriter*, ou *DB _ ddladmin*.

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

Após ter verificado que o recurso de execução do script funciona no SQL Server, você pode executar comandos de R e Python do SQL Server Management Studio, o código do Visual Studio ou qualquer outro cliente que pode enviar instruções T-SQL para o servidor. Antes de fazer isso, talvez você queira fazer algumas alterações à configuração do sistema para dar suporte a um uso intenso do aprendizado de máquina, ou adicionar novos pacotes de R.

Esta seção lista algumas otimizações comuns e atividades de aprendizado para aprendizado de máquina.

### <a name="add-more-worker-accounts"></a>Adicionar mais contas de trabalho

Se você achar que você pode usar o R muito ou se você espera que muitos usuários scripts em execução ao mesmo tempo, você pode aumentar o número de contas de trabalho que são atribuídos ao serviço barra inicial. Para obter mais informações, consulte [modificar o pool de conta de usuário para serviços de aprendizado de máquina do SQL Server](modify-the-user-account-pool-for-sql-server-r-services.md).

### <a name="bkmk_optimize"></a>Otimizar o servidor para execução de scripts externos

As configurações padrão para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalação destinam-se para otimizar o equilíbrio do servidor para uma variedade de serviços que são suportados pelo mecanismo de banco de dados, que pode incluir a extração, transformação e carregamento (ETL) processos, relatórios, auditoria, e aplicativos que usam [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dados. Portanto, as configurações padrão, você pode encontrar recursos de aprendizagem de máquina, às vezes, são restritos ou limitados, especialmente em operações com uso intensivo de memória.

Para garantir que os trabalhos de aprendizado de máquina são priorizados e recursos adequadamente, é recomendável que você use o administrador de recursos do SQL Server para configurar um pool de recursos externos. Você também poderá alterar a quantidade de memória alocada para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mecanismo de banco de dados ou aumentar o número de contas que são executados sob o [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] service.

- Para configurar um pool de recursos de gerenciamento de recursos externos, consulte [criar um pool de recursos externos](../../t-sql/statements/create-external-resource-pool-transact-sql.md).
  
- Para alterar a quantidade de memória reservada para o banco de dados, consulte [opções de configuração de memória do servidor](../../database-engine/configure-windows/server-memory-server-configuration-options.md).
  
- Para alterar o número de contas de R que pode ser iniciado por [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)], consulte [modificar o pool de conta de usuário para o aprendizado de máquina](modify-the-user-account-pool-for-sql-server-r-services.md).

Se você estiver usando a Standard Edition e não possuem o administrador de recursos, você pode usar eventos estendidos e exibições de gerenciamento dinâmico (DMVs), bem como eventos do Windows monitoramento, para ajudar a gerenciar os recursos de servidor que são usados por R. Para obter mais informações, consulte [monitoramento e gerenciamento de serviços de R](managing-and-monitoring-r-solutions.md).

### <a name="install-additional-r-packages"></a>Instalar pacotes R adicionais

Reserve um minuto para instalar quaisquer pacotes R adicionais que você está usando.

Pacotes que você desejar usar do SQL Server deverão ser instalados na biblioteca padrão usada pela instância. Se você tiver uma instalação separada do R no computador, ou se você instalou pacotes nas bibliotecas do usuário, você não poderá usar esses pacotes do T-SQL.

O processo de instalação e gerenciamento de pacotes de R é diferente no SQL Server 2016 e 2017 do SQL Server. Por exemplo, no SQL Server de 2017, você pode configurar grupos de usuários para compartilhar pacotes em um nível por banco de dados ou configurar as funções de banco de dados para permitir que os usuários instalem seus próprios pacotes. Para obter mais informações, consulte [pacote de gerenciamento](r-package-management-for-sql-server-r-services.md).

No SQL Server 2016, um administrador de banco de dados deve instalar os pacotes de R que os usuários precisam.

Acesso administrativo também é necessário para instalar os pacotes de Python adicionais na biblioteca de instância.

### <a name="upgrade-the-machine-learning-components"></a>Atualizar a componentes de aprendizado de máquina

Quando você instala os recursos de aprendizado de máquina no SQL Server, você pode obter a versão dos componentes de R ou Python mais atualizada quando a versão ou service pack foi publicado. Cada vez que você corrigir ou atualiza o servidor, os componentes de aprendizado de máquina são atualizados também.

No entanto, você pode atualizar a componentes em um agendamento mais rápido do que há suporte para de aprendizado de máquina por versões do SQL Server, usando um processo conhecido como _associação_. Quando você associa uma instância do SQL Server, você atualiza as versões de R ou Python, tanto alterar para uma política de suporte a diferentes que oferece suporte a atualizações mais frequentes. 

Essas atualizações podem incluir:

* Novos pacotes de R
+ Novas APIs para a Microsoft, como pacotes [MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package).
* [Modelos de classificação](https://docs.microsoft.com/r-server/install/microsoftml-install-pretrained-models) para análise de texto e de classificação de imagem.

Para obter informações sobre como atualizar uma instância do SQL Server, consulte [atualizar componentes de aprendizado de máquina por meio da associação](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).


### <a name="tutorials"></a>Tutoriais

Para começar com alguns exemplos simples e conheça os fundamentos de como funciona o R com o SQL Server, consulte [código R usando Transact-SQL](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md).

Para exibir exemplos de aprendizado de máquina com base em cenários do mundo real, consulte [tutoriais de aprendizado de máquina](../tutorials/machine-learning-services-tutorials.md).

### <a name="troubleshooting"></a>Solução de problemas

Está tendo problemas? Tentando atualizar? Para obter respostas a perguntas comuns e problemas conhecidos, consulte o seguinte artigo:

* [Atualização e instalação perguntas Frequentes – serviços de aprendizado de máquina](upgrade-and-installation-faq-sql-server-r-services.md)

Para verificar o status da instalação da instância e corrigir problemas comuns, tente esses relatórios personalizados.

* [Relatórios personalizados do SQL Server R Services](\r\monitor-r-services-using-custom-reports-in-management-studio.md)
