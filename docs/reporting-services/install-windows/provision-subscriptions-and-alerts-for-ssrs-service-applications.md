---
title: Provisionar assinaturas e alertas para aplicativos de serviço do SSRS | Microsoft Docs
ms.custom: ''
ms.date: 06/03/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint
ms.component: install-windows
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Reporting Services Shared Service
- SharePoint Mode [Reporting Services]
- SharePoint Mode
- Reporting Services Service Application
- SSRS service application
ms.assetid: d0de3f1f-4887-47fb-bacf-46aaad74c4be
caps.latest.revision: 20
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: a4de22aefed2d4602e5ca331355ae7588394672e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="provision-subscriptions-and-alerts-for-ssrs-service-applications"></a>Provisionar Assinaturas e Alertas para aplicativos de serviço SSRS
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] as assinaturas e os alertas de dados exigem o SQL Server Agent e a configuração de permissões para o SQL Server Agent. Se você visualizar mensagens de erro que indicam que um SQL Server Agent é necessário e tiver verificado que o SQL Server Agent está em execução; em seguida, atualize ou verifique as permissões. O escopo deste tópico é [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no modo do SharePoint e o tópico descreve três maneiras de atualizar as permissões do SQL Server Agent com assinaturas do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . As credenciais que você usa para as etapas neste tópico precisam ter permissões suficientes para conceder permissões execute a RSExecRole para objetos nos bancos de dados de aplicativos de serviço, msdb e mestre.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]** SharePoint 2016 &#124; SharePoint 2013|  
  
 ![Permissões do SQL Agent para BDs do Aplicativo de Serviço](../../reporting-services/install-windows/media/rs-provisionsqlagent.gif "Permissões do SQL Agent para BDs do Aplicativo de Serviço")  
  
||Description|  
|------|-----------------|  
|**1**|A instância do mecanismo de banco de dados do SQL Server que está hospedando os bancos de dados do aplicativo do serviço Reporting Services.|  
|**2**|A instância do SQL Server Agent para a instância do mecanismo de banco de dados SQL.|  
|**3**|Os bancos de dados do aplicativo do serviço Reporting Services. Os nomes são baseados nas informações usadas para criar o aplicativo de serviço. Veja a seguir nomes de bancos de dados de exemplo:<br /><br /> ReportingService_2fbae157295d49df86d0b85760c704b0<br /><br /> ReportingService_2fbae157295d49df86d0b85760c704b0_Alerting<br /><br /> ReportingService_2fbae157295d49df86d0b85760c704b0TempDB|  
|**4**|O banco de dados mestre e MSDB da instância do mecanismo de Banco de Dados do SQL Server.|  
  
 Use um dos três métodos a seguir para atualizar as permissões:  
  
1.  Na página **Provisionar Assinaturas e Alertas** , digite as credenciais e clique em **OK**.  
  
2.  Na página Provisionar Assinaturas e Alertas, clique no botão **Baixar Script** para baixar um script Transact-SQL que possa ser usado para configurar permissões.  
  
3.  Execute um cmdlet do PowerShell para criar um script transact SQL que pode ser usado para configurar permissões.  
  
### <a name="to-update-permissions-using-the-provision-page"></a>Para atualizar permissões usando a página de provisão  
  
1.  Na Administração Central do SharePoint, no grupo **Gerenciamento de Aplicativo** , clique em **Gerenciar Aplicativos de Serviço**  
  
2.  Encontre seu aplicativo de serviço na lista e clique no nome do aplicativo ou clique na coluna **Type** para selecionar o aplicativo de serviços e clique no botão **Gerenciar** na faixa de opções do SharePoint.  
  
3.  Na página **Gerenciar Aplicativo Reporting Services** , clique em **Provisionar Assinaturas e Alertas**.  
  
4.  Se o administrador do SharePoint tiver privilégios suficientes ao banco de dados Mestre e aos bancos de dados de aplicativo de serviço, digite as credenciais.  
  
5.  Clique no botão **OK** .  
  
##  <a name="bkmk_download"></a> Para baixar o script Transact-SQL  
  
1.  Na Administração Central do SharePoint, no grupo **Gerenciamento de Aplicativo** , clique em **Gerenciar Aplicativos de Serviço**  
  
2.  Encontre seu aplicativo de serviço na lista e clique no nome do aplicativo ou clique na coluna **Type** para selecionar o aplicativo de serviços e clique no botão **Gerenciar** na faixa de opções do SharePoint.  
  
3.  Na página **Gerenciar Aplicativo Reporting Services** , clique em **Provisionar Assinaturas e Alertas**.  
  
4.  Na área **Exibir Status** , verifique se o SQL Server Agent está em execução.  
  
5.  Clique em **Baixar Script** para baixar um script Transact-SQL que você pode executar no SQL Server Management Studio para conceder permissões. O nome do arquivo de script que é criado conterá o nome de seu aplicativo de serviço do Reporting Services, por exemplo **[nome do aplicativo de serviço]-GrantRights.sql**.  
  
### <a name="to-generate-the-transact-sql-statement-with-powershell"></a>Para gerar a instrução Transact-SQL com o PowerShell  
  
1.  Você também pode usar um cmdlet do Windows PowerShell no Shell de Gerenciamento do SharePoint 2013 ou 2016 para criar o script Transact-SQL.  
  
2.  No menu **Iniciar** , clique em **Todos os Programas**.  
  
3.  Expanda **Produtos do Microsoft SharePoint 2016** e clique em **Shell de Gerenciamento do Microsoft SharePoint 2016**.
  
4.  Atualize o seguinte cmdlet do PowerShell substituindo o nome do banco de dados do servidor de relatório, a conta do pool de aplicativos e o caminho da instrução.  
  
     **Sintaxe do cmdlet:** `Get-SPRSDatabaseRightsScript –DatabaseName <ReportingServices database name> -UserName <app pool account> -IsWindowsUser | Out-File <path of statement>`  
  
     **Cmdlet de exemplo:** `Get-SPRSDatabaseRightsScript –DatabaseName ReportingService_46fd00359f894b828907b254e3f6257c –UserName “NT AUTHORITY\NETWORK SERVICE” –IsWindowsUser | Out-File c:\SQLServerAgentrights.sql`  
  
## <a name="using-the-transact-sql-script"></a>Usando o script Transact-SQL  
 Os seguintes procedimentos podem ser usados com o download de scripts da página de provisões ou scripts criados usando o PowerShell.  
  
#### <a name="to-load-the-transact-sql-script-in-sql-server-management-studio"></a>Para carregar o script Transact-SQL no SQL Server Management Studio  
  
1.  Para abrir o SQL Server Management Studio, no menu **Iniciar** , clique em [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)] e em **SQL Server Management Studio**.  
  
2.  Na caixa de diálogo **Conectar ao Servidor** , defina as seguintes opções:  
  
    -   Na lista **Tipo de servidor** , selecione **Mecanismo de Banco de Dados**  
  
    -   Na caixa **Nome do Servidor**, digite o nome da instância do SQL Server no qual você deseja configurar o SQL Server Agent.  
  
    -   Selecione um modo de autenticação.  
  
    -   Se estiver conectando usando a Autenticação do SQL Server, forneça um logon e uma senha.  
  
3.  Clique em **Conectar**.  
  
#### <a name="to-run-the-transact-sql-statement"></a>Para executar a instrução Transact-SQL  
  
1.  Na barra de ferramentas do SQL Server Management Studio, clique em **Nova Consulta**.  
  
2.  No menu **Arquivo** , clique em **Abrir**e em **Arquivo**.  
  
3.  Navegue até a pasta em que você salvou a instrução Transact-SQL gerada no Shell de Gerenciamento do SharePoint 2013 ou 2016.  
  
4.  Clique no arquivo e em **Abrir**.  
  
     A instrução é adicionada à janela de consulta.  
  
5.  Clique em **Executar**.  
  
  
