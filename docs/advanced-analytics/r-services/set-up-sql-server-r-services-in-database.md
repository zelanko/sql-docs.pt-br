---
title: "Configurar o SQL Server R Services (no banco de dados) | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
keywords: 
  - "instalando o SQL Server R Services"
ms.assetid: 4d773c74-c779-4fc2-b1b6-ec4b4990950d
caps.latest.revision: 35
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 30
---
# Configurar o SQL Server R Services (no banco de dados)
  No [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e posterior, instale todos os componentes relacionados ao [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] usando o assistente de instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
 
 
 Após a conclusão da instalação, talvez algumas etapas adicionais sejam necessárias para habilitar o recurso do R Services, configurar contas e conceder permissões aos usuários a bancos de dados específicos.   
  
Caso você tenha problemas com o acesso ao banco de dados depois de concluir a instalação ou precise desinstalar versões anteriores, consulte [Perguntas frequentes sobre atualização e instalação &#40;SQL Server R Services&#41;](../../advanced-analytics/r-services/upgrade-and-installation-faq-sql-server-r-services.md).  

> [!NOTE]
> Para instalar o R Services (no Banco de Dados), a unidade em que o recurso está instalado deve dar suporte à criação de nomes de arquivos curtos usando a notação 8dot3. Caso contrário, os processos que iniciam o R por meio do SQL Server poderão não ser iniciados. Lembre-se de habilitar a notação 8dot3 no volume antes de instalar o R Services. Essa restrição será removida em uma versão posterior.

  
##  <a name="a-namebkmkinstallrservicesindatabasea-step-1-install-r-services-in-database-on-sql-server-2016-or-later"></a><a name="bkmk_installRServicesInDatabase"></a> Etapa 1: Instalar o R Services (no Banco de Dados) no SQL Server 2016 ou posterior  
   
  
1.  Execute a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
    Para obter informações sobre como fazer instalações autônomas, consulte [Unattended Installs of SQL Server R Services](../../advanced-analytics/r-services/unattended-installs-of-sql-server-r-services.md).  
  
2.  Na guia **Instalação** , clique em **Nova instalação autônoma do SQL Server ou adicionar recursos a uma instalação existente**.  
  
    > [!NOTE]  
    >  Não é possível instalar o [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] em um cluster de failover. No entanto, é possível instalar o [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] em um computador autônomo que usa o AlwaysOn e que faz parte de um grupo de disponibilidade. Para obter mais informações sobre como usar o R Services em um grupo de disponibilidade AlwaysOn, consulte [Grupos de Disponibilidade AlwaysOn: interoperabilidade](../../database-engine/availability-groups/windows/always-on-availability-groups-interoperability-sql-server.md).  
  
3.  Na página **Seleção de Recursos** , selecione estas opções:  
  
    -   **Serviços do Mecanismo de Banco de Dados**  
  
         Pelo menos uma instância do mecanismo de banco de dados é necessária para usar o [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]. Você pode usar uma instância padrão ou nomeada.  
  
    -   **R Services (no Banco de Dados)**  
  
         Essa opção configura os serviços de banco de dados usados pelos trabalhos em R e instala as extensões que oferecem suporte a scripts e processos externos.  
    > [!NOTE]
    > 
    > Se precisar executar o código R no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], lembre-se de instalar o **[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]**. 
    > 
    > Por outro lado, o Microsoft R Server (Autônomo) é uma opção que permite usar as bibliotecas do Scale R em um computador Windows que não executa o SQL Server. Sugerimos que você instale o Microsoft R Server (Autônomo) em um laptop ou outro computador usado para o desenvolvimento do R, a fim de criar soluções do R que, mais tarde, possam ser implantadas em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que executa o R Services (no Banco de Dados).
 
  
4.  Na página **Consentimento para instalar o Microsoft R Open**, clique em **Aceitar**.  
  
     Este contrato de licença é necessário para baixar o Microsoft R Open, que inclui uma distribuição de pacotes e ferramentas base do R de software livre, junto com pacotes avançados do R e provedores de conectividade da Revolution Analytics.  
  
    > [!NOTE]  
    >  Se o computador usado não tiver acesso à Internet, pause a instalação neste ponto para baixar os instaladores separadamente, conforme descrito aqui: [Instalando os componentes do R sem acesso à Internet](../../advanced-analytics/r-services/installing-r-components-without-internet-access.md)  
  
     Clique em **Aceitar**, aguarde até que o botão **Avançar** fique ativo e clique em **Avançar**.  
  
5.  Na página **Pronto para instalar**, verifique se essas seleções estão incluídas e clique em **Instalar**.  
  
     **Recursos**  
  
     Serviços do Mecanismo de Banco de Dados  
  
     R Services (no banco de dados)  
  
6.  Quando a instalação for concluída, reinicie o computador.   
  
  
##  <a name="a-namebkmkenablefeaturea-step-2-enable-r-services-and-verify-that-local-r-script-execution-works"></a><a name="bkmk_enableFeature"></a> Etapa 2: Habilitar o R Services e verificar o funcionamento da execução de script do R local  
  
  
1. Abra o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Se ele ainda não estiver instalado, execute novamente o assistente de instalação do SQL Server para abrir um link de download e instalá-lo.  
  
2. Conecte-se à instância em que você instalou o R Services (no Banco de Dados) e execute o comando a seguir para habilitar explicitamente o recurso do R Services; caso contrário, não será possível invocar scripts do R, mesmo se o recurso tiver sido instalado pela instalação.  
  
   ```    
   Exec sp_configure  'external scripts enabled', 1  
   Reconfigure  with override    
   ```  
  
10. Reinicie o serviço SQL Server da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Isso reiniciará automaticamente o serviço [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] relacionado também. Reinicie o serviço usando o painel Serviços no Painel de Controle ou o SQL Server Configuration Manager.  
  
9. Depois que o serviço SQL Server estiver disponível, verifique se o recurso do R está habilitado executando o seguinte comando e verificando se *run_value* está definido como 1:  
  
    ```    
    Exec sp_configure  'external scripts enabled'    
    ```  
   Opcionalmente, abra o painel **Serviços** e verifique se o serviço Launchpad da instância está em execução. Cada instância tem seu próprio serviço Launchpad.
   
10. Agora, você deve conseguir executar scripts simples do R no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] parecidos com este:  
  
    ```  
    exec sp_execute_external_script  @language =N'R',  
    @script=N'OutputDataSet<-InputDataSet',    
    @input_data_1 =N'select 1 as hello'  
    with result sets (([hello] int not null));  
    go  
    ```  
  
    **Resultados**  
  
    *hello*  
    *1*   
  
> [!IMPORTANT]  Algumas etapas adicionais serão necessárias se você precisar acessar os dados do SQL Server ou executar comandos do R em um cliente remoto de ciência de dados. As etapas a seguir descrevem esses requisitos adicionais detalhadamente.
 
  
##  <a name="a-namebkmkconfigureaccountsa-step-3-enable-implied-authentication-for-launchpad-accounts"></a><a name="bkmk_configureAccounts"></a> Etapa 3: Habilitar a autenticação implícita para contas do Launchpad  
   
  
Durante a instalação, 20 novas contas de usuário do Windows são criadas com a finalidade de executar tarefas no token de segurança do serviço [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]. Quando um usuário enviar um script do R por meio de um cliente externo, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ativará uma conta de trabalho disponível, mapeará essa conta para a identidade do usuário que fez a chamada e executará o script do R em nome do usuário. Esse é um novo serviço do mecanismo de banco de dados que dá suporte à execução segura de scripts externos, chamado *autenticação implícita*. 

Exiba essas contas no grupo de usuários do Windows, **SQLRUserGroup**.  Se precisar executar scripts do R por meio de um cliente remoto de ciência de dados e estiver usando a autenticação do Windows, essas contas de trabalho deverão receber permissão para fazer logon na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em seu nome.  
  
1. No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], no Pesquisador de Objetos, expanda **Segurança**, clique com o botão direito do mouse em **Logons** e selecione **Novo Logon**.  
2. Na caixa de diálogo **Logon – Novo**, clique em **Pesquisar**.  
3. Clique em **Tipos de Objeto** e selecione **Grupos**. Desmarque todas as outras opções.  
4. Em Inserir o nome do objeto a ser selecionado, digite *SQLRUserGroup* e clique em **Verificar Nomes**.  
5. O nome do grupo local associado ao serviço Launchpad da instância deverá ser resolvido para algo como *instancename\SQLRUserGroup*. Clique em **OK**.  
6. Por padrão, o logon é atribuído à função **pública** e tem permissão para se conectar ao mecanismo de banco de dados. 
7. Clique em **OK**.  
  
> [!NOTE] Se você usar um logon SQL para executar scripts do R em um contexto de computação do SQL Server, essa etapa adicional não será necessária.
  
  
## <a name="step-4-give-non-admin-users-r-script-permissions"></a>Etapa 4: Conceder permissões a usuários não administradores ao script do R  
  
Se você instalou o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por conta própria e está executando scripts do R em sua própria instância, em geral, você executa scripts como administrador e, portanto, tem permissão implícita em várias operações e em todos os dados no banco de dados, bem como a capacidade de instalar novos pacotes do R, conforme necessário.  
  
No entanto, em um cenário corporativo, a maioria dos usuários, incluindo aqueles que acessam o banco de dados usando logons SQL, não tem permissões elevadas desse tipo. Portanto, para cada usuário que executará scripts externos, você deverá conceder as permissões de usuário para executar scripts do R em cada banco de dados em que o R será usado.   
  
  
```  
USE <database_name>  
GO  
GRANT EXECUTE ANY EXTERNAL SCRIPT  TO [UserName]  
```  

> [!TIP] Precisa de ajuda com a instalação? Não tem certeza de que executou todas as etapas?
>
> Use esses relatórios personalizados para verificar o status de instalação do R Services. Para obter mais informações, consulte [Monitorar o R Services usando relatórios personalizados](../../advanced-analytics/r-services/monitor-r-services-using-custom-reports-in-management-studio.md).    
  
##  <a name="a-namebkmkadditionala-optional-modifications"></a><a name="bkmk_Additional"></a> Modificações opcionais  
  
Esta seção descreve as alterações adicionais que você poderá fazer na configuração da instância, ou de seu cliente de ciência de dados, para dar suporte à execução de script do R.
  
### <a name="modify-the-number-of-worker-accounts-used-by-includersqllaunchpadtokenrsqllaunchpadmdmd"></a>Modificar o número de contas de trabalho usadas pelo [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]
  
Se você acreditar que fará uso considerável do R ou esperar que vários usuários executem scripts simultaneamente, aumente o número de contas de trabalho atribuídas ao serviço Launchpad. Para saber mais, confira [Modify the User Account Pool for SQL Server R Services](../../advanced-analytics/r-services/modify-the-user-account-pool-for-sql-server-r-services.md).  
  
  
### <a name="give-your-r-users-or-logins-read-write-or-ddl-permissions-as-needed-in-additional-databases"></a>Conceder aos usuários ou logons do R permissões de leitura, gravação ou DDL, conforme necessário, em bancos de dados adicionais  
  
Durante a execução de scripts do R, a conta de usuário poderá precisar ler dados de outros bancos de dados, criar novas tabelas para armazenar os resultados e gravar dados em tabelas. 
     
Para cada usuário que executará scripts do R, verifique se a conta de usuário tem a permissão **db_datareader**, **db_datawriter** ou **db_ddladmin** no banco de dados específico.   
       
Por exemplo, a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] a seguir concede ao logon SQL *MySQLLogin* os direitos para executar consultas T-SQL no banco de dados *RSamples*. Para executar essa instrução, o logon SQL já deve existir no contexto de segurança do servidor.  
  
```  
USE RSamples  
GO  
EXEC sp_addrolemember 'db_datareader', 'MySQLLogin'  
```  
  
Para obter mais informações sobre as permissões incluídas em cada função, consulte [Funções de nível de banco de dados](../../relational-databases/security/authentication-access/database-level-roles.md).  
  
  
### <a name="create-an-odbc-data-source-for-the-instance-on-your-data-science-client"></a>Criar uma fonte de dados ODBC para a instância no cliente de ciência de dados  
  
Se você criar uma solução do R em um computador cliente de ciência de dados e precisar se conectar ao computador [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como o contexto de computação, use um logon SQL ou a autenticação integrada do Windows.  
  
Se você usar um logon SQL, garanta que o logon tem as permissões apropriadas no banco de dados em que os dados serão lidos. Faça isso adicionando as permissões *Conectar a* e *SELECT* ou adicionando o logon à função **db_datareader**. Se precisar criar objetos, serão necessários direitos **DDL_admin**.  Para salvar dados em tabelas, adicione o logon à função **db_datawriter**.  
  
Se você usar a autenticação do Windows, será necessário configurar uma fonte de dados ODBC no cliente de ciência de dados que especifica o nome da instância e outras informações de conexão.  
  
Para obter mais informações, consulte [Usando o administrador de fonte de dados ODBC](http://windows.microsoft.com/windows/using-odbc-data-source-administrator).  
  
### <a name="optimize-the-server-for-r"></a>Otimizar o servidor para o R  

As configurações padrão da instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] destinam-se a otimizar o equilíbrio do servidor para uma variedade de serviços com suporte no mecanismo de banco de dados, que podem incluir processos ETL, relatórios, auditoria e aplicativos que usam os dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Portanto, nas configurações padrão, você poderá encontrar recursos restritos ou limitados para as operações do R, especialmente em operações com uso intensivo de memória.  
  
 Para garantir que as tarefas do R sejam priorizadas e tenham os recursos apropriados, recomendamos o uso do Resource Governor para configurar um pool de recursos externos específico à operação do R. Talvez você também deseje alterar a quantidade de memória alocada para o mecanismo de banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou aumentar o número de contas em execução no serviço [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)].  
  
-   Configurar um pool de recursos para o gerenciamento de recursos externos  
  
     [CREATE EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md)  
  
-   Alterar a quantidade de memória reservada para o mecanismo de banco de dados  
  
     [Opções Server Memory de configuração do servidor](../../database-engine/configure-windows/server-memory-server-configuration-options.md)  
  
-   Alterar o número de contas do R que podem ser iniciadas pelo [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]  
  
     [Modificar o pool de contas de usuário para o SQL Server R Services](../../advanced-analytics/r-services/modify-the-user-account-pool-for-sql-server-r-services.md)  
  
### <a name="get-the-r-source-code-optional"></a>Obter o código-fonte do R (opcional)  

O [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] inclui uma distribuição de pacotes base do R de software livre.  
  
Opcionalmente, clique em um desses links para iniciar imediatamente o download do código-fonte GPL/LGPL modificado. O código-fonte é disponibilizado em conformidade com a Licença Pública Geral GNU, mas não é necessário para instalar ou usar o [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)].  
  
-   Compatível com o RC2: Baixar arquivo morto [rre-gpl-src.8.0.2.tar.gz](http://go.microsoft.com/fwlink/?LinkId=786770) 
  
-   Compatível com o RC3: Baixar arquivo morto [rre-gpl-src.8.0.3.tar.gz](http://go.microsoft.com/fwlink/?LinkId=786771) 

-   Compatível com o RTM: Baixar arquivo morto [rre-gpl-src.8.0.3.tar.gz](http://go.microsoft.com/fwlink/?LinkID=786771)
  
## <a name="troubleshooting"></a>Solução de problemas  
 Está tendo problemas? Consulte esta lista de problemas comuns durante a instalação de versões de pré-lançamento do [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]  
  
 [Perguntas frequentes sobre atualização e instalação &#40;SQL Server R Services&#41;](../../advanced-analytics/r-services/upgrade-and-installation-faq-sql-server-r-services.md)  
  
## <a name="see-also"></a>Consulte também  
 [Configurar um cliente de ciência de dados](../../advanced-analytics/r-services/set-up-a-data-science-client.md)   
 [Criar um R Server autônomo](../../advanced-analytics/r-services/create-a-standalone-r-server.md)  
  
  