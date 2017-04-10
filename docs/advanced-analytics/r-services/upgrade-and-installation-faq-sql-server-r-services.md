---
title: "Perguntas frequentes sobre atualiza&#231;&#227;o e instala&#231;&#227;o (SQL Server R Services) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/13/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 001e66b9-6c3f-41b3-81b7-46541e15f9ea
caps.latest.revision: 58
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 47
---
# Perguntas frequentes sobre atualiza&#231;&#227;o e instala&#231;&#227;o (SQL Server R Services)
  Este tópico fornece respostas a perguntas comuns sobre instalação, bem como a perguntas sobre atualizações de versões prévias do [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)].  
  
 Se você estiver instalando o [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] pela primeira vez, siga os procedimentos para configurar o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e os componentes do R, conforme descrito aqui: [Configurar o SQL Server R Services &#40;no Banco de Dados&#41;](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md).  

   
## <a name="important-changes-from-pre-releae-versions"></a>Alterações importantes desde as versões de pré-lançamento  
 Se você instalou qualquer versão de pré-lançamento do SQL Server 2016 ou está usando instruções de instalação publicadas antes da liberação pública do SQL Server 2016, é importante saber que o processo de instalação é completamente diferente entre as versões de pré-lançamento e RTM. Essas alterações incluem as opções disponíveis no assistente de instalação do SQL Server e as etapas pós-instalação. 
   
> [!WARNING] Não há mais suporte para uma nova instalação de nenhuma versão de pré-lançamento do [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]. Recomendamos a atualização assim que possível.  
+ Se você tiver instalado o [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] no CTP3, CTP3.1, CTP3.2, RC0 ou RC1, será necessário executar novamente o script de instalação pós-configuração para desinstalar as versões anteriores dos componentes do R e do R Services. 
+ O script de instalação pós-configuração é fornecido apenas para ajudar os clientes a desinstalar as versões de pré-lançamento.  Não o execute durante a instalação de uma versão mais nova.

## <a name="how-to-uninstall-previous-versions-of-r-services"></a>Como desinstalar as versões anteriores do R Services

É importante que você desinstale as versões anteriores do [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] e os componentes do R relacionados na ordem correta.

### <a name="1-run-script-to-deregister-windows-user-group-and-components-before-uninstalling-previous-components"></a>1. Executar o script para cancelar o registro do grupo de usuários do Windows e dos componentes antes de desinstalar os componentes anteriores
Se tiver instalado uma versão de pré-lançamento do [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], primeiro você deverá executar o script `RegisteREext.exe` com o argumento `/uninstall`.

Ao fazer isso, você cancela o registro de componentes antigos e remove o grupo de usuários do Windows associado ao Launchpad. Se você não fizer isso, não será possível criar o grupo de usuários do Windows necessário para as novas instâncias que serão instaladas.
  
Por exemplo, se você tiver instalado o R Services na instância padrão, execute este comando no diretório em que o script está instalado:  
  
~~~~
    RegisterRExt.exe /UNINSTALL  
~~~~ 
  
Se você tiver instalado o R Services em uma instância nomeada, especifique o nome da instância após *INSTANCE:*  
  
~~~~ 
RegisterRExt.exe /UNINSTALL /INSTANCE:<instancename>   
~~~~  

Talvez seja necessário executar o script mais de uma vez para remover todos os componentes.

> [!NOTE]
> A localização padrão desse script varia de acordo com a versão de pré-lançamento instalada. Se você tentar executar a versão incorreta do script, poderá receber um erro. 
> 
>  + Se você tiver o CTP 3.1, 3.2 ou 3.3, antes de desinstalar os componentes, será necessário baixar uma versão atualizada do script de configuração pós-instalação no [Centro de Download da Microsoft](http://go.microsoft.com/fwlink/?LinkId=723194). O script atualizado dá suporte ao cancelamento do registro de componentes mais antigos. Clique no link e selecione **Salvar como** para salvar o script em uma pasta local. Renomeie o script existente e, em seguida, copie o novo script na pasta onde o script será executado. 
>  + Para o RC0, o arquivo de script correto foi instalado e está localizado nesta pasta: `C:\Program Files\Microsoft\MRO-for-RRE\8.0\R-3.2.2\library\RevoScaleR\rxLibs\x64`  
>  + Para versões de lançamento (13.0.1601.5 ou posterior), nenhum script é necessário para instalar ou configurar componentes. O script deve ser usado somente para remoção de componentes mais antigos. 


### <a name="2-uninstall-any-older-versions-of-the-revolution-enterprise-tools-including-components-installed-with-ctp-releases"></a>2. Desinstale as versões mais antigas das ferramentas do Revolution Enterprise, incluindo os componentes instalados com as versões CTP.

A ordem de desinstalação dos componentes do R é crítica. Sempre desinstale o [!INCLUDE[rsql_rre-noversion](../../includes/rsql-rre-noversion-md.md)] primeiro. Em seguida, desinstale o [!INCLUDE[rsql_rro-noversion](../../includes/rsql-rro-noversion-md.md)].  

 Se você desinstalar por engano o R Open primeiro e receber um erro ao tentar desinstalar o Revolution R Enterprise, uma solução é reinstalar o Microsoft R Open ou o Revolution R Open e desinstalar os dois componentes na ordem correta.  

### <a name="3-uninstall-any-other-version-of-microsoft-r-open"></a>3. Desinstale as outras versões do Microsoft R Open.

Por fim, desinstale todas as outras versões do Microsoft R Open.
 
### <a name="4-upgrade-sql-server"></a>4. Atualizar o SQL Server  
  
Após a desinstalação de todos os componentes de pré-lançamento, reinicie o computador. Esse é um requisito de instalação do SQL Server e você só poderá continuar com uma instalação atualizada depois que a reinicialização for concluída.     

Depois de fazer isso, execute a instalação do SQL Server e siga estas instruções para instalar o [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]: [Configurar o SQL Server R Services](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md).  
  
Nenhum componente adicional é necessário; os pacotes de R e os pacotes de conectividade são instalados pela instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 


## <a name="upgrading-r-components"></a>Atualização dos componentes do R

Quando hotfixes ou melhorias para o SQL Server 2016 forem liberados, os componentes do R serão atualizados, caso sua instância já inclua o recurso R Services. 

No entanto, ao atualizar ou aplicar patch a servidores que não estão conectados à Internet, é necessário baixar uma versão atualizada dos componentes do R manualmente antes de iniciar a atualização. Para obter mais informações, consulte [Instalando componentes do R sem acesso à Internet](../../advanced-analytics/r-services/installing-r-components-without-internet-access.md).

## <a name="problems-uninstalling-older-versions-of-r"></a>Problemas com a desinstalação de versões anteriores do R  
Em alguns casos, as versões mais antigas do Revolution R Open ou do Revolution R Enterprise não foram completamente removidas pelo processo de desinstalação.  
  
 Se você tiver problemas ao remover uma versão mais antiga, edite também o Registro para remover as chaves relacionadas.  
  
 Abra o Registro do Windows e localize esta chave: `HKLM\Software\Microsoft\Windows\CurrentVersion\Uninstall`.  
  
 Exclua as seguintes entradas, se houver, e se a chave contiver apenas um único valor `sEstimatedSize2`:  
  
-   E0B2C29E-B8FC-490B-A043-2CAE75634972        (para o 8.0.2)  
  
-   46695879-954E-4072-9D32-1CC84D4158F4        (para o 8.0.1)  
  
-   2DF16DF8-A2DB-4EC6-808B-CB5A302DA91B        (para o 8.0.0)  
  
-   5A2A1571-B8CD-4AAF-9303-8DF463DABE5A        (para o 7.5.0)  


## <a name="new-license-agreement-for-r-components-required-for-unattended-installs"></a>Novo contrato de licença para componentes do R necessários para instalações autônomas  
 Se você usar a linha de comando para atualizar uma instância do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] que já tem o [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] instalado, será necessário modificar a linha de comando para usar o novo parâmetro de contrato de licença, */IACCEPTROPENLICENSEAGREEMENT*. 
 
 O uso mal-sucedido do argumento correto pode causar uma falha na configuração do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="after-running-setup-includersqlproductnametokenrsqlproductnamemdmd-is-still-not-enabled"></a>Depois de executar a instalação, o [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] não ainda estará habilitado  
 O recurso que dá suporte à execução de scripts externos é desabilitado por padrão, mesmo se instalado. Isso ocorre por design, para reduzir a área de superfície.  
  
 Para habilitar scripts do R, um administrador poderá executar a seguinte instrução no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]:  
  
1.  Na instância do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] em que você deseja usar o R, execute esta instrução.  
  
    ```  
    sp_configure 'external scripts enabled',1 
    reconfigure with override  
    ```  
  
2.  Reinicie a instância.  
  
3.  Depois de reiniciar a instância, abra o **SQL Server Configuration Manager** ou o painel **Serviços** e verifique se o serviço [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] está em execução.  

> [!TIP] Para instalar uma instância do R Services que é pré-configurada, use a imagem de máquina virtual do Azure que inclui o Enterprises Edition com R Services habilitado. Para obter mais informações, consulte [Instalando o SQL Server R Services em uma Máquina Virtual do Azure](../../advanced-analytics/r-services/installing-sql-server-r-services-on-an-azure-virtual-machine.md).
 

## <a name="setup-of-includersqlproductnametokenrsqlproductnamemdmd-not-available-in-a-failover-cluster"></a>A instalação do [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] não está disponível em um cluster de failover  
 Atualmente, não é possível instalar o [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] em um cluster de failover.  
    
 No entanto, é possível instalar o [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] em um computador autônomo que usa o AlwaysOn e que faz parte de um grupo de disponibilidade. Para obter mais informações sobre como usar o R Services em um grupo de disponibilidade AlwaysOn, consulte [Grupos de Disponibilidade AlwaysOn: interoperabilidade](../../database-engine/availability-groups/windows/always-on-availability-groups-interoperability-sql-server.md).  

Outra opção é configurar uma réplica em outra instância do SQL Server com a finalidade de executar os scripts do R. A réplica poderá ser criada com o uso da replicação ou do envio de logs.
 
## <a name="launchpad-service-cannot-be-started"></a>O serviço Launchpad não pode ser iniciado  

Há vários problemas que podem impedir a inicialização do Launchpad.
+ **Notação 8dot3 não habilitada**.  Para instalar o R Services (no Banco de Dados), a unidade em que o recurso está instalado deve dar suporte à criação de nomes de arquivos curtos usando a notação **8dot3**.  Um nome de arquivo 8.3 também é chamado um nome de arquivo curto e é usado para compatibilidade com versões anteriores do Microsoft Windows antes ou como um nome de arquivo alternativo ao nome de arquivo longo. 

  Se o volume em que você está instalando o [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] não der suporte a nomes de arquivos curtos, os processos que iniciam o R por meio do SQL Server não poderão localizar o executável correto e o [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] não será iniciado.  
  
   Como alternativa, você deverá habilitar a notação 8dot3 no volume em que o SQL Server e o R Services estão instalados. Em seguida, será necessário fornecer o nome curto para o diretório de trabalho no arquivo de configuração do R Services. 

    1. Para habilitar a notação 8dot3, execute o utilitário **fsutil** com o argumento *8dot3name*, conforme descrito aqui: [fsutil 8dot3name](https://technet.microsoft.com/library/ff621566(v=ws.11).aspx).
    2. Depois de habilitar a notação 8dot3, abra o arquivo RLauncher.config. Em uma instalação padrão, o arquivo RLauncher.config está localizado em C:\Arquivos de Programas\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn
    3. Anote a propriedade de WORKING_DIRECTORY.
    4. Use o utilitário fsutil com o argumento *file* para especificar um caminho de arquivo curto para a pasta especificada em WORKING_DIRECTORY.
    5. Edite o arquivo de configuração para usar o nome curto de WORKING_DIRECTORY.   
     
Como alternativa, especifique outro diretório para WORKING_DIRECTORY que tem um caminho compatível com a notação 8dot3.     
   
   > [!NOTE] Essa restrição será removida em uma versão posterior. 
 
+ **A conta que executa o Launchpad foi alterada ou as permissões necessárias foram removidas.** Por padrão, o [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] usa a seguinte conta na inicialização, que é configurada pela instalação do [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] para ter todas as permissões necessárias: NT Service\MSSQLLaunchpad

  Portanto, se você atribuir outra conta ao Launchpad ou a conta correta for removida por uma política no computador do SQL Server, a conta poderá não ter as permissões necessárias e você poderá receber este erro: *ERROR_LOGON_TYPE_NOT_GRANTED 1385 (0x569) Falha de logon: o usuário não recebeu o tipo de logon solicitado neste computador.*

  Para conceder as permissões necessárias à nova conta de serviço, use o aplicativo **Política de Segurança Local** e atualize as permissões na conta para incluir estas permissões:
  + Ajustar cotas de memória para um processo (SeIncreaseQuotaPrivilege)
  + Ignorar verificação completa (SeChangeNotifyPrivilege)
  + Fazer logon como um serviço (SeServiceLogonRight)
  + Substituir um token de nível de processo (SeAssignPrimaryTokenPrivilege)

  Para obter mais informações sobre as permissões para executar serviços SQL Server, consulte [Configurar contas de serviço e permissões do Windows](https://msdn.microsoft.com/library/ms143504.aspx#Windows).
  
## <a name="side-by-side-installation-not-supported"></a>Sem suporte para a instalação lado a lado  
 Não crie uma instalação lado a lado usando outra versão do R, ou outras versões do Revolution Analytics.  

## <a name="offline-installation-of-r-components-for-localized-version-of-sql-server"></a>Instalação offline de componentes do R para a versão localizada do SQL Server 
Se você estiver instalando o R Services em um computador que não tem acesso à Internet, você deverá realizar duas etapas adicionais: baixar o instalador do componente do R em uma pasta local antes de executar a instalação do SQL Server e editar o arquivo do instalador para garantir que o idioma correto é instalado. 

O identificador de idioma usado para os componentes do R deve ser o mesmo que o idioma da instalação do SQL Server que está sendo instalado; caso contrário, o botão **Avançar** estará desabilitado e não será possível concluir a instalação.

Para obter mais informações, consulte [Instalando componentes do R sem acesso à Internet](../../advanced-analytics/r-services/installing-r-components-without-internet-access.md). 
  
## <a name="unable-to-launch-runtime-for-r-script"></a>Não é possível iniciar o tempo de execução para o script do R
O [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] cria um grupo de usuários do Windows que é usado pelo [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] para executar os trabalhos do R. Esse grupo de usuários deve ter a capacidade de fazer logon na instância que executa o R Services para executar o R em nome de usuários remotos que estejam usando a autenticação integrada do Windows.
  
 Em um ambiente no qual o grupo do Windows para usuários do R (**SQLRUsers**) não tem essa permissão, os seguintes erros poderão ser exibidos:  
  
-   Quando tentar executar scripts R:  
  
     *Não é possível iniciar o tempo de execução para o script do “R”. Verifique a configuração do tempo de execução do script do R.*  
  
     *Erro de script externo. Não é possível iniciar o tempo de execução.*  
  
-   Erros gerados pelo serviço do [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] :  
  
     *Falha ao inicializar o inicializador RLauncher.dll*  
  
     *Nenhuma dll do inicializador foi registrada!*  
  
-   Os logs de segurança indicam que a conta NT SERVICE\MSSQLLAUNCHPAD está desabilitada para logon.  
  
Para obter informações sobre como atribuir as permissões necessárias a esse grupo de usuários, consulte [Configurar o SQL Server R Services](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md). 

> [!NOTE]
> 
> Essa limitação não se aplicará se você usar logons SQL para executar scripts do R em uma estação de trabalho remota. 

  
## <a name="remote-execution-via-odbc"></a>Execução remota por meio de ODBC   
 Se você usar uma estação de trabalho de ciência de dados e se conectar ao computador [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para executar comandos do R usando as funções **RevoScaleR**, poderá receber um erro ao usar chamadas ODBC que gravam dados no servidor. 
 
 O motivo é o mesmo descrito na seção anterior: durante a instalação, o R Services cria um grupo de contas de trabalho usadas para executar tarefas do R. No entanto, se essas contas não puderem se conectar ao servidor, não será possível executar as chamadas ODBC em seu nome. 
 
 Observe que essa limitação não se aplicará se você usar logons SQL para executar scripts do R em uma estação de trabalho remota, pois as credenciais de logon SQL são passadas explicitamente do cliente R para a instância do SQL Server e, em seguida, para o ODBC.
  
Para habilitar a autenticação implícita, você deverá conceder permissões a esse grupo de contas de trabalho da seguinte maneira:  
    
1. Abra o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] como administrador na instância em que você executará o código R. 

2. Execute o script a seguir. Lembre-se de editar o nome do grupo de usuários, caso tenha alterado o padrão, além do nome do computador e da instância.
    ```sql
    USE [master]
    GO
    
    CREATE LOGIN [computername\SQLRUserGroup] FROM WINDOWS WITH DEFAULT_DATABASE=[master], DEFAULT_LANGUAGE=[language]
    GO  
    ```

Para obter mais informações e as etapas para fazer isso usando a interface do usuário do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], consulte [Configurar o SQL Server R Services](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md).

    
## <a name="errors-during-setup-because-r-components-cannot-be-installed"></a>Erros durante a instalação devido a não ser possível instalar os componentes do R  
 Quando você instala o R Services (no Banco de Dados) usando a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ao clicar em **Aceitar** na página que contém os termos de licença do Microsoft R Open, a instalação deverá localizar os componentes e iniciar a instalação quando outros componentes forem instalados. Entretanto, nesses casos, poderá ocorrer uma falha na instalação dos componentes:  
  
-   Você está realizando uma instalação offline e os componentes não podem ser baixados.  
  
     [Instalando os componentes do R sem acesso à Internet](../../advanced-analytics/r-services/installing-r-components-without-internet-access.md)  
  
-   Você está usando a opção para verificar se há atualizações e o serviço de atualização retorna um erro informando não ser possível localizar a versão correta do componente.  
  
  Esse é um problema conhecido que foi corrigido no RC3.  
  
 
  
## <a name="upgrade-of-r-server-standalone-to-rc3-requires-uninstallation-using-the-rc2-setup-utility"></a>A atualização do R Server (Autônomo) para o RC3 exige a desinstalação com o utilitário de configuração do RC2
 O Microsoft R Server (Autônomo) foi disponibilizado primeiro no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] RC2. Para atualizar para a versão RC3 do Microsoft R Server, primeiro você deverá desinstalá-lo usando a instalação do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] RC2 e, em seguida, reinstalá-lo usando a instalação do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] RC3.  
  
1.  Desinstale o R Server (Autônomo) para [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] RC2 usando a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
2.  Atualize o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] para o RC3 e selecione a opção para instalar o R Services (no Banco de Dados). Isso atualiza a instância do [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] para o RC3; nenhuma configuração adicional é necessária.  
  
3.  Execute a instalação do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] para o RC3 mais uma vez e instale o Microsoft R Server (Autônomo).  

Essa solução alternativa não é necessária ao atualizar para a versão RTM do Microsoft R Server.

## <a name="see-also"></a>Consulte também  
 [Introdução ao SQL Server R Services](../../advanced-analytics/r-services/getting-started-with-sql-server-r-services.md)   
 [Introdução ao Microsoft R Server &#40;autônomo&#41;](../../advanced-analytics/r-services/getting-started-with-microsoft-r-server-standalone.md)  
  
  