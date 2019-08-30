---
title: Banco de dados do host em uma instância gerenciada | Microsoft Docs
description: Descreve como configurar um banco de dados do MDS em uma instância gerenciada.
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
manager: craigg
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 0081ea193452e4e92938051bc7b4a40bc8631eaa
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2019
ms.locfileid: "70155376"
---
# <a name="host-database-on-managed-instance"></a>Banco de dados host na instância gerenciada

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Este artigo aborda como configurar um banco de dados MDS na instância gerenciada.
  
## <a name="preparation"></a>Preparação

Precisamos concluir as etapas a seguir na preparação.
- Conclua a criação e configuração da instância gerenciada. Incluir rede virtual e VPN ponto a site.
- Conclua a configuração do computador do aplicativo Web.
  - Inclua a instalação de VPN ponto a site.
  - Instalar funções e recursos.

**Lado do banco de dados:**

1. Criar uma instância gerenciada do banco de dados SQL do Azure incluir rede virtual. [Início Rápido: Criar uma instância gerenciada do banco de dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-get-started)
2. Configure uma conexão ponto a site. [Configurar uma conexão ponto a site com uma VNet usando a autenticação de certificado nativa do Azure: portal do Azure](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal)
3. Configurar a autenticação de Azure Active Directory com a instância gerenciada do banco de dados SQL. [Configurar e gerenciar a autenticação de Azure Active Directory com o SQL](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication-configure)

**Lado do computador do aplicativo Web:**

1. Instale o certificado de conexão ponto a site e a VPN para garantir que o computador possa acessar a instância gerenciada do banco de dados SQL. [Configurar uma conexão ponto a site com uma VNet usando a autenticação de certificado nativa do Azure: portal do Azure](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal)
2. Instale a função e os recursos. O recurso a seguir é necessário.

- Papéis

      Internet Information Services
      Web Management Tools
      IIS Management Console
      World Wide Web Services
      Application Development
      .NET Extensibility 3.5
      .NET Extensibility 4.5
      ASP.NET 3.5
      ASP.NET 4.5
      ISAPI Extensions
      ISAPI Filters
      Common HTTP Features
      Default Document
      Directory Browsing
      HTTP Errors
      Static Content
      [Note: Do not install WebDAV Publishing]
      Health and Diagnostics
      HTTP Logging
      Request Monitor
      Performance
      Static Content Compression
      Security
      Request Filtering
      Windows Authentication

- Recursos:

      .NET Framework 3.5 (includes .NET 2.0 and 3.0)
      .NET Framework 4.5 Advanced Services
      ASP.NET 4.5
      WCF Services
      HTTP Activation [Note: This is required.]
      TCP Port Sharing
      Windows Process Activation Service
      Process Model
      .NET Environment
      Configuration APIs
      Dynamic Content Compression

## <a name="install-and-configure-includessmdsshort_mdincludesssmdsshort-mdmd-web-application"></a>Instalar e configurar [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] o aplicativo Web

Precisamos concluir as etapas a seguir para instalar e [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]configurar o.

1. Instale SQL Server recurso de [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] inclusão do 2019.
2. Crie um [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] banco de dados na instância de gerenciamento.
3. Criar e configurar o aplicativo Web [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]para o.
  
**Instalar o SQL Server 2019**

Use o assistente de instalação SQL Server instalação do ou um prompt de comando [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]para instalar o.

1. Clique duas vezes em Setup.exe e siga as etapas no assistente de instalação.

2. Selecione [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] na página seleção de recursos em recursos compartilhados.
A opção instala o [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)], assemblies, um snap-in do Windows PowerShell, pastas e arquivos de aplicativos Web e serviços Web.

    ![MDS-SQLServer2019-config-mi-SQLFeatureSelection](../master-data-services/media/mds-sqlserver2019-config-mi-sqlfeatureselection.png "MDS-SQLServer2019-config-MI_SQLFeatureSelection")  

**Configurando o banco de dados e o site**

1. Conecte a rede virtual do Azure para garantir que você possa se conectar à instância gerenciada.

    ![MDS-SQLServer2019-config-mi-P2SVPNConnect](../master-data-services/media/mds-sqlserver2019-config-mi-p2svpnconnect.png "MDS-SQLServer2019-config-MI_P2SVPNConnect")  

2. Inicie o [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]. E clique em **configuração do banco de dados** no painel esquerdo.

3. Clique em **criar banco de dados**e em avançar no Assistente para **criar banco de dados** .

4. Na página **servidor de banco de dados** , preencha a **instância de SQL Server** e selecione o **tipo de autenticação** e clique em **testar conexão** para confirmar que você pode se conectar ao banco de dados usando as credenciais para o tipo de autenticação que você Selecione. Clique em Avançar.

   > [!NOTE]
   > - Instância de SQL Server para instância gerenciada, como "xxxxxxx.xxxxxxx.database.windows.net"
   > - Para a instância gerenciada, damos suporte ao tipo de autenticação **"conta de SQL Server"** e **"usuário atual – Active Directory integrado"** .
   > - Quando você seleciona **usuário atual – Active Directory integrado** como o tipo de autenticação, a caixa **nome de usuário** é somente leitura e exibe o nome da conta de usuário do Windows que está conectada ao computador. Se você estiver executando o SQL Server [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 2019 em uma VM (máquina virtual) do Azure, a caixa **nome de usuário** exibirá o nome da VM e o nome de usuário para a conta de administrador local na VM.

    Verifique se a autenticação contém a regra **"sysadmin"** para a instância gerenciada.
![MDS-SQLServer2019-config-mi-CreateDBConnect](../master-data-services/media/mds-sqlserver2019-config-mi-createdbconnect.png "MDS-SQLServer2019-config-MI_CreateDBConnect")  

5. Digite um nome no campo **Nome do banco de dados** . Opcionalmente, para selecionar uma ordenação do Windows, desmarque a caixa de seleção **Ordenação padrão do SQL Server** e clique em uma ou mais das opções disponíveis como **Diferenciar maiúsculas de minúsculas**. Clique em **Avançar**.

    ![MDS-SQLServer2019-config-mi-CreatedDBName](../master-data-services/media/mds-sqlserver2019-config-mi-createddbname.png "MDS-SQLServer2019-config-MI_CreatedDBName")  

6. No campo **nome de usuário** , especifique a conta do Windows do usuário que será o superusuário padrão do [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]. Um Superusuário tem acesso a todas as áreas funcionais e pode adicionar, excluir e atualizar todos os modelos.

    ![MDS-SQLServer2019-config-mi-CreateDBUserName](../master-data-services/media/mds-sqlserver2019-config-mi-createdbusername.png "MDS-SQLServer2019-config-MI_createDBUserName")

7. Clique em **Avançar** para exibir um resumo das configurações do banco de dados [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] e em **Avançar** novamente para criar o banco de dados. A página **Progresso e Conclusão** é exibida.

8. Quando o banco de dados estiver criado e configurado, clique em **Concluir**.

    Para obter mais informações sobre as configurações no **Assistente para criar banco de dados**, consulte [assistente&#41;para &#40; [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] criar banco de dados Configuration Manager](../master-data-services/create-database-wizard-master-data-services-configuration-manager.md).

9. Na página **configuração do banco** de dados [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]no, clique em **Selecionar Banco de dados**.

10. Clique em **conectar**, selecione [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] o banco de dados que você criou na etapa 8 e clique em **OK**.

    ![MDS-SQLServer2019-config-mi-connectDBName](../master-data-services/media/mds-sqlserver2019-config-mi-connectdbname.png "MDS-SQLServer2019-config-MI_connectDBName")

11. Em [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)], clique em **Configuração da Web** no painel esquerdo.

12. Na caixa de listagem **Site** , clique em **Site Padrão**e em **Criar** para criar um aplicativo Web.
![MDS-SQLServer2019-config-mi-Webconfiguration](../master-data-services/media/mds-sqlserver2019-config-mi-webconfiguration.png "MDS-SQLServer2019-config-MI_WebConfiguration")

   > [!NOTE] 
   > Quando você seleciona **Site Padrão**, é necessário criar um aplicativo Web. Se você selecionar **Criar novo site** na caixa de listagem, o aplicativo será criado automaticamente.

    

13. Na seção **pool de aplicativos** , insira um nome de usuário diferente, insira a senha e clique em OK.
![MDS-SQLServer2019-config-mi-CreateWebApplication](../master-data-services/media/mds-sqlserver2019-config-mi-createwebapplication.png "MDS-SQLServer2019-config-MI_CreateWebApplication")

   > [!NOTE]
   > Você precisa garantir que o usuário possa acessar o banco de dados com Active Directory autenticação integrada que você acabou de criar. Ou você precisa alterar a conexão em Web. config mais tarde.

    

14. Para obter mais informações sobre a caixa de diálogo **criar aplicativo Web** , consulte a [ &#40; [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] caixa de diálogo&#41;criar aplicativo Web Configuration Manager](../master-data-services/create-web-application-dialog-box-master-data-services-configuration-manager.md).

15. Na página **configuração da Web** na caixa **aplicativo Web** , clique no aplicativo que você criou e, em seguida, clique em **selecionar** na seção **associar aplicativo ao banco de dados** .

16. Clique em **Conectar**, selecione o banco de dados [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] que você deseja associar ao aplicativo Web e clique em **OK**.

    Você terminou de configurar o site. A página **configuração da Web** agora exibe o site selecionado, o aplicativo Web que você criou e [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] o banco de dados associado ao aplicativo.

    ![MDS-SQLServer2019-config-mi-WebConfigSelectDB](../master-data-services/media/mds-sqlserver2019-config-mi-webconfigselectdb.png "MDS-SQLServer2019-config-MI_WebConfigSelectDB")

17. Clique em **Aplicar**. A caixa de mensagem **Configuração Concluída** é exibida. Clique em **OK** na caixa de mensagem para iniciar o aplicativo Web. O endereço do site é http://server nome/aplicativo Web/.

## <a name="other-authentication-type-to-connect-managed-instance-database-on-web-application"></a>Outro tipo de autenticação para conectar o banco de dados de instância gerenciada no aplicativo Web

É possível obter o arquivo **Web. config** em C:\Program Files\Microsoft SQL Server\150\Master Data Services\WebApplication. Podemos modificar o connectionString para alterar outro tipo de autenticação para conectar o banco de dados de instância gerenciada.

O tipo de autenticação padrão é "**Active Directory integrado**", a seguir está a cadeia de conexão de exemplo.

```xml
<add name="MDS1" connectionString="Data Source=*****.*****.database.windows.net;Initial Catalog=MasterDataServices;Integrated Security=False;Connect Timeout=60;Authentication=&quot;Active Directory Integrated&quot;" />
```

Também há suporte para Active Directory autenticação de senha e autenticação de SQL Server, a seguir está a cadeia de conexão de exemplo.

Active Directory autenticação de senha

```xml
<add name="MDS1" connectionString="Data Source=*****.*****.database.windows.net;Initial Catalog=MasterDataServices;Integrated Security=False;Connect Timeout=60;Authentication=&quot;Active Directory Password&quot; ; UID=bob@contoso.onmicrosoft.com; PWD=MyPassWord!" />
```

Autenticação do SQL Server

```xml
<add name="MDS1" connectionString="Data Source=*****.*****.database.windows.net;Initial Catalog=MasterDataServices;Integrated Security=False;Connect Timeout=60;User ID=UserName;Password=MyPassword!;" />
```

## <a name="upgrade-includessmdsshort_mdincludesssmdsshort-mdmd-and-database-version"></a>Atualização [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] e versão do banco de dados

**Melhora[!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]**

Instale a **atualização cumulativa**do SQL Server 2019, [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] o será atualizado automaticamente.

**Atualizar versão do banco de dados**

Se você receber a mensagem "a versão do cliente é incompatível com a versão do banco de dados" depois de instalar SQL Server **atualização cumulativa**2019, será necessário atualizar a versão do banco de dados.

![MDS-SQLServer2019-config-mi-UpgradeDBPage](../master-data-services/media/mds-sqlserver2019-config-mi-upgradedbpage.png "MDS-SQLServer2019-config-MI_UpgradeDBPage")

1. Inicie o [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]. E clique em **configuração do banco de dados** no painel esquerdo.

2. Na página **configuração do banco** de dados [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]no, clique em **Selecionar Banco de dados**.

3. Clique em **conectar**, selecione [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] o banco de dados que você associou para o aplicativo Web e clique em **OK**.

    ![MDS-SQLServer2019-config-mi-ConnectDBName](../master-data-services/media/mds-sqlserver2019-config-mi-connectdbname.png "MDS-SQLServer2019-config-MI_ConnectDBName")

4. Clique em **Atualizar banco de dados...** Button

    ![MDS-SQLServer2019-config-mi-SelectUpgradeDB](../master-data-services/media/mds-sqlserver2019-config-mi-selectupgradedb.png "MDS-SQLServer2019-config-MI_SelectUpgradeDB")

5. No Assistente para atualizar banco de dados, clique no botão **Avançar** na página **Bem-vindo** e **revisão de atualização** .

    ![MDS-SQLServer2019-config-mi-UpgradeDBWizard](../master-data-services/media/mds-sqlserver2019-config-mi-upgradedbwizard.png "MDS-SQLServer2019-config-MI_UpgradeDBWizard")

6. Clique no botão **concluir** quando todas as tarefas forem concluídas.

## <a name="see-also"></a>Consulte também

 [Banco de dados Master Data Services](../master-data-services/master-data-services-database.md) [Master Data Manager aplicativo Web](../master-data-services/master-data-manager-web-application.md) [Página &#40;de configuração do&#41; banco de dados Gerenciador de configuração do Master Data Services](../master-data-services/database-configuration-page-master-data-services-configuration-manager.md) [O que há de novo &#40;no&#41; Master Data Services MDS](../master-data-services/what-s-new-in-master-data-services-mds.md)
