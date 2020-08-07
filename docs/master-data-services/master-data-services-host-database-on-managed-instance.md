---
title: Hospedar um banco de dados em uma instância gerenciada
description: Saiba como criar e configurar um banco de dados Master Data Services (MDS) e hospedá-lo em um Instância Gerenciada SQL do Azure.
ms.custom: ''
ms.date: 07/01/2019
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 19519697-c219-44a8-9339-ee1b02545445
author: v-redu
ms.author: lle
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 616fa3791b0dbc154282f5273cd7fb4e1eb3c1f5
ms.sourcegitcommit: a4ee6957708089f7d0dda15668804e325b8a240c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2020
ms.locfileid: "87878943"
---
# <a name="host-an-mds-database-on-a-managed-instance"></a>Hospedar um banco de dados MDS em uma instância gerenciada

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  Este artigo aborda como configurar um banco de dados Master Data Services (MDS) em uma instância gerenciada.
  
## <a name="preparation"></a>Preparação

Para preparar, você precisa criar e configurar um Instância Gerenciada de SQL do Azure e configurar o computador do aplicativo Web.

### <a name="create-and-configure-the-database"></a>Criar e configurar o banco de dados

1. Crie uma instância gerenciada com uma rede virtual. Consulte [início rápido: criar um instância gerenciada SQL](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-get-started) para obter detalhes.

1. Configure uma conexão ponto a site. Consulte [Configurar uma conexão ponto a site com uma VNet usando a autenticação de certificado nativa do Azure: portal do Azure](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal) para obter instruções.

1. Configure Azure Active Directory autenticação com o SQL Instância Gerenciada. Consulte [configurar e gerenciar a autenticação de Azure Active Directory com o SQL](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication-configure) para obter detalhes.

### <a name="configure-web-application-machine"></a>Configurar computador do aplicativo Web

1. Instale um certificado de conexão ponto a site e uma VPN para garantir que o computador possa acessar a instância gerenciada. Consulte [Configurar uma conexão ponto a site com uma VNet usando a autenticação de certificado nativa do Azure: portal do Azure](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal) para obter instruções.

1. Instale as seguintes funções e recursos:
   - Funções:
     - Serviços de informações da Internet
     - Ferramentas de gerenciamento da Web
     - Console de Gerenciamento IIS
     - Serviços da World Wide Web
     - Desenvolvimento do aplicativo
     - .NET Extensibility 3.5
     - Extensibilidade do .NET 4.5
     - ASP.NET 3.5
     - ASP.NET 4.5
     - Extensões ISAPI
     - Filtros ISAPI
     - Recursos comuns de HTTP
     - Documento padrão
     - Navegação de diretório
     - Erros de HTTP
     - Conteúdo estático
     - Integridade e diagnóstico
     - Log de HTTP
     - Monitor de solicitação
     - Desempenho
     - Compactação de conteúdo estático
     - Segurança
     - Filtragem de solicitação
     - Autenticação do Windows
       > [!NOTE]
       > Não instalar a publicação WebDAV

   - Recursos:
     - .NET Framework 3.5 (inclui o .NET 2.0 e 3.0)
     - Serviços avançados do .NET Framework 4.5
     - ASP.NET 4.5
     - Serviços WCF
     - Ativação HTTP (obrigatório)
     - Compartilhamento de porta TCP
     - Serviço de Ativação de Processos do Windows
     - Modelo de processo
     - Ambiente .NET
     - APIs de configuração
     - Compactação de Conteúdo Dinâmico

## <a name="install-and-configure-an-mds-web-application"></a>Instalar e configurar um aplicativo Web do MDS

Em seguida, instale e configure o [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] .

### <a name="install-sql-server-2019"></a>Instalar o SQL Server 2019

Use o assistente de instalação SQL Server instalação do ou um prompt de comando para instalar o [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] .

1. Abra `Setup.exe` o e siga as etapas no assistente de instalação.

2. Selecione [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] na página **Seleção de Recursos** em **Recursos Compartilhados**.
Esta ação instala:
   - [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]
   - Assemblies
   - Um snap-in do Windows PowerShell
   - Pastas e arquivos para serviços e aplicativos Web.

   ![MDS-SQLServer2019-config-MI-SQLFeatureSelection](../master-data-services/media/mds-sqlserver2019-config-mi-sqlfeatureselection.png "MDS-SQLServer2019-config-MI_SQLFeatureSelection")  

### <a name="set-up-the-database-and-website"></a>Configurar o banco de dados e o site

1. Conecte a rede virtual do Azure para garantir que você possa se conectar à instância gerenciada.

   ![MDS-SQLServer2019-config-MI-P2SVPNConnect](../master-data-services/media/mds-sqlserver2019-config-mi-p2svpnconnect.png "MDS-SQLServer2019-config-MI_P2SVPNConnect")

1. Abra o [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] e selecione **configuração do banco de dados** no painel esquerdo.

1. Selecione **criar banco de dados** para abrir o **Assistente para criar banco de dados**. Selecione **Avançar**.

1. Na página **servidor de banco de dados** , preencha o campo **instância de SQL Server** e escolha o **tipo de autenticação**. Selecione **testar conexão** para confirmar que você pode usar suas credenciais para se conectar ao banco de dados por meio do tipo de autenticação escolhido. Selecione **Avançar**.

   > [!NOTE]
   > - Uma instância de SQL Server é semelhante A `xxxxxxx.xxxxxxx.database.windows.net` .
   > - Para uma instância gerenciada, escolha entre os tipos de autenticação **"conta de SQL Server"** e **"usuário atual – Active Directory integrado"** .
   > - Se você selecionar **usuário atual – Active Directory integrado** como o tipo de autenticação, o campo **nome de usuário** será somente leitura e exibirá a conta de usuário do Windows conectada no momento. Se você estiver executando o SQL Server 2019 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] em uma VM (máquina virtual) do Azure, o campo **nome de usuário** exibirá o nome da VM e o nome de usuário para a conta de administrador local na VM.

   Sua autenticação deve conter a regra **"sysadmin"** para instâncias gerenciadas.

   ![MDS-SQLServer2019-config-MI-CreateDBConnect](../master-data-services/media/mds-sqlserver2019-config-mi-createdbconnect.png "MDS-SQLServer2019-config-MI_CreateDBConnect")  

1. Digite um nome no campo **Nome do banco de dados** . Opcionalmente, para selecionar um agrupamento do Windows, desmarque a caixa de seleção **SQL Server Agrupamento padrão** e selecione uma ou mais das opções disponíveis. Por exemplo, **diferencia maiúsculas de minúsculas**. Selecione **Avançar**.

   ![MDS-SQLServer2019-config-MI-CreatedDBName](../master-data-services/media/mds-sqlserver2019-config-mi-createddbname.png "MDS-SQLServer2019-config-MI_CreatedDBName")

1. No campo **nome de usuário** , especifique a conta do Windows do superusuário padrão para [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] . Um superusuário tem acesso a todas as áreas funcionais e pode adicionar, excluir e atualizar todos os modelos.

   ![MDS-SQLServer2019-config-MI-CreateDBUserName](../master-data-services/media/mds-sqlserver2019-config-mi-createdbusername.png "MDS-SQLServer2019-config-MI_createDBUserName")

1. Selecione **Avançar** para exibir um resumo das configurações do banco de [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] dados. Selecione **Avançar** novamente para criar o banco de dados. Você verá a página **progresso e conclusão** .

1. Depois que o banco de dados for criado e configurado, selecione **concluir**.

   Para obter mais informações sobre as configurações no **Assistente para criar banco de dados**, consulte [Assistente para criar banco de dados &#40;[!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] Configuration Manager&#41;](../master-data-services/create-database-wizard-master-data-services-configuration-manager.md).

1. Na página **configuração do banco de dados** no [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] , **escolha Selecionar Banco de dados**.

1. Selecione **conectar**, escolha o [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] banco de dados e, em seguida, selecione **OK**.

   ![MDS-SQLServer2019-config-MI-connectDBName](../master-data-services/media/mds-sqlserver2019-config-mi-connectdbname.png "MDS-SQLServer2019-config-MI_connectDBName")

1. No [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] , selecione **configuração da Web** no painel esquerdo.

1. Na caixa de listagem **site** **da Web, escolha site padrão**e, em seguida, selecione **criar** para criar um aplicativo Web.

   ![MDS-SQLServer2019-config-MI-webconfiguration](../master-data-services/media/mds-sqlserver2019-config-mi-webconfiguration.png "MDS-SQLServer2019-config-MI_WebConfiguration")

   > [!NOTE]
   > Se você selecionar **site padrão**, precisará criar separadamente um aplicativo Web. Se você escolher **criar novo site** na caixa de listagem, o aplicativo será criado automaticamente.

1. Na seção **pool de aplicativos** , insira um nome de usuário diferente, insira a senha e, em seguida, selecione **OK**.

   ![MDS-SQLServer2019-config-MI-CreateWebApplication](../master-data-services/media/mds-sqlserver2019-config-mi-createwebapplication.png "MDS-SQLServer2019-config-MI_CreateWebApplication")

   > [!NOTE]
   > Verifique se o usuário pode acessar o banco de dados com a autenticação integrada Active Directory que você criou recentemente. Como alternativa, você pode alterar a conexão em `web.config` mais tarde.

   Para obter mais informações sobre a caixa de diálogo **criar aplicativo Web** , consulte a [caixa de diálogo criar aplicativo web &#40;[!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] Configuration Manager&#41;](../master-data-services/create-web-application-dialog-box-master-data-services-configuration-manager.md).

1. No painel **configuração da Web** na janela do **aplicativo Web** , selecione o aplicativo que você criou e escolha **selecionar** na seção **associar aplicativo com o banco de dados** .

1. Selecione **conectar** e escolha o [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] banco de dados que você deseja associar ao aplicativo Web. Selecione **OK**.

   Você concluiu a configuração do site. A página **configuração da Web** agora exibe o site selecionado, o aplicativo Web que você criou e o [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] banco de dados associado ao aplicativo.

   ![MDS-SQLServer2019-config-MI-WebConfigSelectDB](../master-data-services/media/mds-sqlserver2019-config-mi-webconfigselectdb.png "MDS-SQLServer2019-config-MI_WebConfigSelectDB")

1. Escolha **Aplicar**. Você verá a mensagem **configuração concluída** . Selecione **OK** na caixa de mensagem para iniciar o aplicativo Web. O endereço do site é `http://server name/web application/` .

## <a name="configure-authentication"></a>Configurar autenticação

Para conectar o banco de dados de instância gerenciada ao aplicativo Web, você precisa alterar o outro tipo de autenticação.

Localize o `web.config` arquivo em `C:\Program Files\Microsoft SQL Server\150\Master Data Services\WebApplication` . Modifique o connectionString para alterar o outro tipo de autenticação para se conectar ao banco de dados de instância gerenciada.

O tipo de autenticação padrão é `Active Directory Integrated` como mostrado na seguinte cadeia de conexão de exemplo:

   ```xml
   <add name="MDS1" connectionString="Data Source=*****.*****.database.windows.net;Initial Catalog=MasterDataServices;Integrated Security=False;Connect Timeout=60;Authentication=&quot;Active Directory Integrated&quot;" />
   ```

O MDS também dá suporte à autenticação de senha e SQL Server de Active Directory, conforme mostrado nas seguintes cadeias de conexão de exemplo:

- Autenticação de senha do Active Directory

   ```xml
   <add name="MDS1" connectionString="Data Source=*****.*****.database.windows.net;Initial Catalog=MasterDataServices;Integrated Security=False;Connect Timeout=60;Authentication=&quot;Active Directory Password&quot; ; UID=bob@contoso.onmicrosoft.com; PWD=MyPassWord!" />
   ```

- Os logons de autenticação do SQL Server

   ```xml
   <add name="MDS1" connectionString="Data Source=*****.*****.database.windows.net;Initial Catalog=MasterDataServices;Integrated Security=False;Connect Timeout=60;User ID=UserName;Password=MyPassword!;" />
   ```

## <a name="upgrade-ssmdsshort_md-and-sql-database-version"></a>Atualização [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] e versão do banco de dados SQL

### <a name="upgrade-ssmdsshort_md"></a>Melhora[!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]

Instale a **atualização cumulativa do SQL Server 2019**. [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]será atualizado automaticamente.

### <a name="upgrade-sql-server"></a>Atualizar o SQL Server

Você pode receber o erro: `The client version is incompatible with the database version` depois de instalar **SQL Server atualização cumulativa 2019**.
![MDS-SQLServer2019-config-MI-UpgradeDBPage](../master-data-services/media/mds-sqlserver2019-config-mi-upgradedbpage.png "MDS-SQLServer2019-config-MI_UpgradeDBPage")

Para corrigir esse problema, você precisa atualizar a versão do banco de dados:

1. Abra o [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] e selecione configuração do **banco de dados** no painel esquerdo.

1. Na página **configuração do banco de dados** no [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] , **escolha Selecionar Banco de dados**.

1. Escolha o [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] banco de dados que você associou ao aplicativo Web. Selecione **conectar**e, em seguida, selecione **OK**.

   ![MDS-SQLServer2019-config-MI-ConnectDBName](../master-data-services/media/mds-sqlserver2019-config-mi-connectdbname.png "MDS-SQLServer2019-config-MI_ConnectDBName")

1. Selecione **Atualizar banco de dados...** .

   ![MDS-SQLServer2019-config-MI-SelectUpgradeDB](../master-data-services/media/mds-sqlserver2019-config-mi-selectupgradedb.png "MDS-SQLServer2019-config-MI_SelectUpgradeDB")

1. No Assistente para atualizar banco de dados, selecione **Avançar** na página de **boas-vindas** e na página **revisão de atualização** .

   ![MDS-SQLServer2019-config-MI-UpgradeDBWizard](../master-data-services/media/mds-sqlserver2019-config-mi-upgradedbwizard.png "MDS-SQLServer2019-config-MI_UpgradeDBWizard")

1. Selecione **concluir** depois que todas as tarefas forem concluídas.

## <a name="see-also"></a>Confira também

- [Banco de dados do Master Data Services](../master-data-services/master-data-services-database.md)
- [Aplicativo Web Master Data Manager](../master-data-services/master-data-manager-web-application.md)
- [Página Configuração do Banco de Dados &#40;Gerenciador de Configuração do Master Data Services&#41;](../master-data-services/database-configuration-page-master-data-services-configuration-manager.md)
- [Novidades no MDS &#40;Master Data Services&#41;](../master-data-services/what-s-new-in-master-data-services-mds.md)
