---
title: Migrar uma instalação do Reporting Services (modo do SharePoint) | Microsoft Docs
ms.date: 08/17/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.topic: conceptual
ms.assetid: 61290949-690a-4e19-b078-57c99b6b30fa
author: markingmyname
ms.author: maghan
ms.openlocfilehash: cf12709e232d4b9d84f311784f78d469b7f00e7b
ms.sourcegitcommit: 3daacc4198918d33179f595ba7cd4ccb2a13b3c0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/25/2018
ms.locfileid: "50021310"
---
# <a name="migrate-a-reporting-services-installation-sharepoint-mode"></a>Migrar uma instalação do Reporting Services (modo do SharePoint)

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)]

  Este tópico é uma visão geral das etapas necessárias para migrar uma implantação do modo do SharePoint do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] de um ambiente do SharePoint para outro. As etapas específicas podem ser diferentes dependendo da versão da qual você está migrando. Para obter mais informações sobre Atualização e cenários de Migração para o modo do SharePoint, consulte [Upgrade and Migrate Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md). Se você quiser copiar os itens de relatório de um servidor para outro, veja [Script rs.exe do Reporting Services de exemplo para copiar conteúdo entre Servidores de Relatório](../../reporting-services/tools/sample-reporting-services-rs-exe-script-to-copy-content-between-report-servers.md).  
  
 Para obter informações sobre como migrar uma implantação do modo nativo do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , veja [Migrar uma instalação do Reporting Services &#40;modo nativo&#41;](../../reporting-services/install-windows/migrate-a-reporting-services-installation-native-mode.md).  
  
 Uma das razões comuns para concluir uma migração é quando você deseja atualizar a implantação do SharePoint 2010 para o SharePoint 2013/2016. O SharePoint 2013/2016 não dá suporte à atualização in-loco do SharePoint 2010, e é necessário concluir o procedimento de **atualização de anexação de banco de dados** ou de migração apenas de conteúdo.  
  
 Para obter mais informações sobre como atualizar o SharePoint 2013/2016, consulte o seguinte:  

-   [Visão geral do processo de atualização para o SharePoint 2016](https://technet.microsoft.com/library/cc262483\(v=office.16\)).

-   [Visão geral do processo de atualização para o SharePoint 2013](https://go.microsoft.com/fwlink/p/?LinkId=256688).
  
-   [Limpar preparações antes de uma atualização do SharePoint 2013](https://go.microsoft.com/fwlink/p/?LinkId=256689).  
  
-   [Atualizar bancos de dados do SharePoint 2013 para o SharePoint 2016](https://technet.microsoft.com/library/cc303436\(v=office.16\)).

-   [Atualizar bancos de dados do SharePoint 2010 para o SharePoint 2013](https://go.microsoft.com/fwlink/p/?LinkId=256690).
  
-   [Mova os bancos de dados de conteúdo no SharePoint 2016](https://technet.microsoft.com/library/cc262792\(v=office.16\).aspx).

-   [Mova os bancos de dados de conteúdo no SharePoint 2013](https://technet.microsoft.com/library/cc262792.aspx).
  
##  <a name="bkmk_prior_versions"></a> Migrar de versões do modo SharePoint do Reporting Services anteriores ao SQL Server 2012  
 A arquitetura de modo do SharePoint do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] foi alterada no [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], inclusive o esquema de banco de dados de aplicativo de serviço. Se desejar migrar para o modo do SharePoint do [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] de uma versão anterior do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], primeiro crie o novo ambiente do SharePoint instalando o SharePoint e o modo do SharePoint do SQL Server 2016 Reporting Services. Para obter mais informações, veja [Instalar o Reporting Services no modo do SharePoint](../../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md).  
  
 Quando o novo ambiente do SharePoint estiver em execução, você poderá escolher entre apenas uma migração de conteúdo ou uma migração completa no nível de banco de dados que inclui bancos de dados de conteúdo.  
  
###  <a name="bkmk_content_only_migration"></a> Migração de conteúdo apenas  
 **Migração apenas de conteúdo do Reporting Services:** Se você quiser copiar o conteúdo do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para um novo farm, precisará usar ferramentas como **rs.exe** para copiar o conteúdo para a nova instalação do SharePoint. Para obter mais informações sobre migrações somente de conteúdo, consulte o seguinte:  
  
-   **[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] :** Os scripts podem migrar conteúdo e recursos entre servidores de relatório de modo nativo e SharePoint. Para obter mais informações, veja [Script rs.exe do Reporting Services de exemplo para copiar conteúdo entre Servidores de Relatório](../../reporting-services/tools/sample-reporting-services-rs-exe-script-to-copy-content-between-report-servers.md) e [Script RS.exe do Reporting Services que migra o conteúdo de um servidor de relatório para outro](http://azuresql.codeplex.com/releases/view/115207).  
  
-   **Ferramenta de migração do Reporting Services:** A ferramenta de migração pode copiar seus itens de relatório de um servidor de modo nativo para um servidor de modo do SharePoint. Para saber mais, veja [Ferramenta de migração do Reporting Services](http://www.microsoft.com/download/details.aspx?id=29560) (http://www.microsoft.com/download/details.aspx?id=29560).  
  
###  <a name="bkmk_full_migration"></a> Migração completa  
 **Migração completa:** Se você estiver migrando bancos de dados de conteúdo do SharePoint junto com os bancos de dados de catálogo do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para um novo farm, você poderá seguir uma série de opções de backup e restauração resumidas neste tópico. Em alguns casos, você precisará usar uma ferramenta para a fase de restauração diferente da que você usou para a fase de backup. Por exemplo, você pode usar o Gerenciador de Configurações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para fazer backup de chaves de criptografia de uma versão anterior do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], mas precisa usar a Administração central do SharePoint ou o PowerShell para restaurar as chaves de criptografia para uma instalação do modo do SharePoint do SQL Server 2016 Reporting Services.  
  
####  <a name="bkmk_databases"></a> Bancos de dados que você verá na migração concluída  
 A tabela a seguir descreve os Bancos de dados do SQL Server relacionados ao [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que você terá depois que migrar com sucesso sua instalação do SharePoint do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] :  
  
|banco de dados|Nome de exemplo||  
|--------------|------------------|-|  
|Banco de dados de catálogo|ReportingService_[service application GUID] **(\*)**|Usuário migra.|  
|Banco de dados temporário|ReportingService_[service application GUID]TempDB **(\*)**|Usuário migra.|  
|Bancos de dados de alerta|ReportingService_[GUID do aplicativo de serviço]_Alerting|Criado quando um aplicativo de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] é criado.|  
  
 **(\*)** Os nomes de exemplo mostrados na tabela seguem a convenção de nomenclatura que o SSRS usa quando você cria um novo aplicativo de serviço SSRS. Se você estiver migrando de um servidor diferente, seu catálogo e tempDBs terão os nomes da instalação original.  
  
####  <a name="bkmk_backup_operations"></a> Operações de backup  
 Esta seção descreve os tipos de informações que você precisa para migrar e as ferramentas ou processos que você usa para concluir o backup.  
  
 ![Diagrama básico de migração do SharePoint do SSRS](../../reporting-services/install-windows/media/rs-sharepoint-migration.gif "Diagrama básico de migração do SharePoint do SSRS")  
  
||Objetos|Método|Observações|  
|-|-------------|------------|-----------|  
|**1**|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|**Rskeymgmt.exe** ou [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager. Veja [Fazer backup e restaurar as chaves de criptografia do Reporting Services](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md).|As ferramentas observadas podem ser usadas para o backup, mas, para a operação de restauração, você usará as páginas de gerenciamento do aplicativo de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ou PowerShell.|  
|**2**|Bancos de dados de conteúdo do SharePoint.||Faça backup do banco de dados e desanexe-o.<br /><br /> Confira a seção "Upgrade da anexação do banco de dados" em [Determinar abordagem de upgrade (SharePoint Server 2010) (https://technet.microsoft.com/library/cc263447.aspx)](https://technet.microsoft.com/library/cc263447.aspx).|  
|**3**|Banco de dados do SQL Server que é o banco de dados de catálogo do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|Backup e restauração de banco de dados do SQL Server<br /><br /> ou em<br /><br /> Anexar e desanexar banco de dados do SQL Server.||  
|**4**|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|Cópia de arquivo simples.|Você só precisará copiar o rsreportserver.config se tiver feito personalizações ao arquivo. Exemplo do local padrão dos arquivos: C:\Arquivos de Programas\Common Files\Microsoft Shared\Web Server Extensions\15\WebServices\Reporting\\*:<br /><br /> <br /><br /> RSReportServer.config<br /><br /> Rssvrpolicy.config<br /><br /> Web.config para o aplicativo ASP.NET do Servidor de Relatório.<br /><br /> Machine.config para ASP.NET.|  
  
####  <a name="bkmk_restore_operations"></a> Operações de restauração  
 Esta seção descreve os tipos de informações que você precisa para migrar e as ferramentas ou processos que você usa para concluir a restauração. As ferramentas que você usa para restaurar podem ser diferentes das que você usou para o backup.  
  
 Antes de concluir as etapas de restauração, você precisa instalar e configurar o novo Farm do SharePoint e modo do SharePoint do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Para saber mais sobre a instalação do modo do SharePoint do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , confira [Instalar o Reporting Services no modo do SharePoint](../../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md).  
  
||Objetos|Método|Observações|  
|-|-------------|------------|-----------|  
|**1**|Restaure bancos de dados de conteúdo do SharePoint para o novo farm.|Método "Atualização da anexação do banco de dados" do SharePoint.|Etapas básicas:<br /><br /> 1) Restaurar o banco de dados no novo servidor.<br /><br /> 2) Anexe o banco de dados de conteúdo a um aplicativo Web indicando a URL.<br /><br /> 3) O Get-SPWebapplication lista todos os aplicativos Web e as URLs.<br /><br /> <br /><br /> Confira a seção "Upgrade da anexação do banco de dados" em [Determinar abordagem de upgrade (SharePoint Server 2010) (https://technet.microsoft.com/library/cc263447.aspx)](https://technet.microsoft.com/library/cc263447.aspx)e [Anexar bancos de dados e fazer upgrade para o SharePoint Server 2010 (https://technet.microsoft.com/library/cc263299.aspx)](https://technet.microsoft.com/library/cc263299.aspx).|  
|**2**|Restaure o banco de dados SQL que é o banco de dados de catálogo do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] (ReportServer).|Backup e restauração de bancos de dados SQL.<br /><br /> **ou**<br /><br /> Anexar e desanexar bancos de dados SQL Server.|Na primeira vez que o banco de dados for usado, o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] atualizará o esquema de banco de dados, conforme necessário, para que ele funcione com o ambiente do SQL Server 2016.|  
|**3**|Criar um novo aplicativo de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|Criar um novo aplicativo de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|Quando você cria o novo aplicativo de serviço, configure-o para usar o banco de dados de servidor de relatório do qual você copiou.<br /><br /> Para obter mais informações sobre como usar a Administração Central do SharePoint, veja a “Etapa 3: Criar um aplicativo de serviço do Reporting Services” em [Instalar o Primeiro Servidor de Relatório no Modo do SharePoint](../../reporting-services/install-windows/install-the-first-report-server-in-sharepoint-mode.md).<br /><br /> Para obter exemplos usando o PowerShell, consulte a seção "Criar um aplicativo de serviço do Reporting Services usando o PowerShell" em [Reporting Services SharePoint Service and Service Applications](../../reporting-services/report-server-sharepoint/reporting-services-sharepoint-service-and-service-applications.md).|  
|**4**|Restaure os arquivos de configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|Cópia de arquivo simples.|Exemplo do local padrão dos arquivos: C:\Arquivos de Programas\Common Files\Microsoft Shared\Web Server Extensions\15\WebServices\Reporting.|  
|||||  
|**5**|Restaurar as chaves de criptografia do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|Restaure o arquivo de backup de chave usando a página "SystemSettings" do aplicativo de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .<br /><br /> **ou**<br /><br /> PowerShell.|Confira a seção “Gerenciamento de chaves” no tópico [Gerenciar um aplicativo de serviço SharePoint do Reporting Services](../../reporting-services/report-server-sharepoint/manage-a-reporting-services-sharepoint-service-application.md).|   
  
##  <a name="bkmk_migrate_from_ctp"></a> Migrar de um SQL Server 2012 ou implantação do SQL Server 2014  
 Em um farm multisservidor, os usuários provavelmente terão os bancos de dados de Conteúdo e Catálogo em uma máquina diferente, nesse caso você realmente só precisará adicionar um novo servidor com o serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] instalado, para o farm do SharePoint e então remover o servidor antigo. Não há necessidade de copiar bancos de dados.  
  
### <a name="backup-operations"></a>Operações de backup  
  
1.  Backup das chaves de criptografia do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
2.  Backup do aplicativo de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] na Administração Central do SharePoint (ou use o PowerShell). Isto também fará backup dos bancos de dados de aplicativo de serviço no SharePoint. Confira o tópico  [Aplicativos de serviço do SharePoint de backup e restauração do Reporting Services](../../reporting-services/report-server-sharepoint/backup-and-restore-reporting-services-sharepoint-service-applications.md)  
  
3.  Se você tiver uma UEA (conta de execução autônoma conta) e a autenticação do Windows, faça uma nota das credenciais para que você possa usá-las para o processo de restauração.  
  
4.  Para obter mais informações, consulte [Fazer backup de aplicativos de serviço no SharePoint 2013](https://technet.microsoft.com/library/ee428318.aspx).  
  
### <a name="restore-operations"></a>Operações de restauração  
  
1.  Restaurar o aplicativo de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] usando a Administração Central do SharePoint. Você também pode usar o PowerShell.  
  
2.  Restaurar chaves de criptografia do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
     Confira a seção “Gerenciamento de chaves” no tópico [Gerenciar um aplicativo de serviço SharePoint do Reporting Services](../../reporting-services/report-server-sharepoint/manage-a-reporting-services-sharepoint-service-application.md)  
  
3.  Configure o UEA e as credenciais do Windows no aplicativo de serviço.  
  
4.  Para obter mais informações, consulte [Restaurar aplicativos de serviço no SharePoint 2013](https://technet.microsoft.com/library/ee428305.aspx).  
  
##  <a name="bkmk_additional_resources"></a> Recursos adicionais  
  
-   [Introdução a upgrades para o SharePoint 2013 (https://technet.microsoft.com/library/ee833948.aspx)](https://technet.microsoft.com/library/ee833948.aspx).  
  
-   [Visão geral do processo de upgrade para o SharePoint 2013 (https://technet.microsoft.com/library/cc262483.aspx)](https://technet.microsoft.com/library/cc262483.aspx).  

## <a name="next-steps"></a>Próximas etapas

[Atualizar e migrar o Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)   
[Migrar uma instalação do Reporting Services](../../reporting-services/install-windows/migrate-a-reporting-services-installation-native-mode.md)  

Ainda tem dúvidas? [Experimente perguntar no fórum do Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
