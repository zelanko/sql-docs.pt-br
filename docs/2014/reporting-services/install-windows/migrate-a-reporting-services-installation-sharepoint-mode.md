---
title: Migrar uma instalação do Reporting Services (modo do SharePoint) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 61290949-690a-4e19-b078-57c99b6b30fa
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: cbfb8cf446cb95e5930ccb8178312e82db774ec3
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/28/2020
ms.locfileid: "78176956"
---
# <a name="migrate-a-reporting-services-installation-sharepoint-mode"></a>Migrar uma instalação do Reporting Services (modo do SharePoint)
  Este tópico é uma visão geral das etapas necessárias para migrar uma implantação do modo do SharePoint do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] de um ambiente do SharePoint para outro. As etapas específicas podem ser diferentes dependendo da versão da qual você está migrando. Para obter mais informações sobre Atualização e cenários de Migração para o modo do SharePoint, consulte [Upgrade and Migrate Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md). Se você quiser copiar os itens de relatório de um servidor para outro, consulte [Sample Reporting Services rs.exe Script to Migrate Content between Report Servers](../tools/sample-reporting-services-rs-exe-script-to-copy-content-between-report-servers.md).

 Para obter informações sobre como migrar uma implantação do modo nativo do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], veja [Migrar uma instalação do Reporting Services &#40;Modo Nativo&#41;](../../reporting-services/install-windows/migrate-a-reporting-services-installation-native-mode.md).

||
|-|
|**[!INCLUDE[applies](../../includes/applies-md.md)]** SharePoint 2010 e SharePoint 2013|

 Uma das razões comuns para concluir uma migração é quando você deseja atualizar a implantação do SharePoint 2010 para o SharePoint 2013. O SharePoint 2013 não oferece suporte à atualização no local do SharePoint 2010, e você deve concluir o procedimento de **atualização de anexação de banco de dados** ou apenas uma migração de conteúdo.

 Para obter mais informações sobre como atualizar o SharePoint 2013, consulte o seguinte:

-   [Visão geral do processo de atualização para o SharePoint 2013](https://go.microsoft.com/fwlink/p/?LinkId=256688).

-   [Atualize os bancos de dados do sharepoint 2010 para o sharepoint 2013](https://go.microsoft.com/fwlink/p/?LinkId=256690).

-   [Mova bancos de dados de conteúdo no SharePoint 2013](https://technet.microsoft.com/library/cc262792.aspx).

 

##  <a name="bkmk_prior_versions"></a>Migrar de versões do modo do Reporting Services SharePoint anteriores ao SQL Server 2012
 A arquitetura de modo do SharePoint do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] foi alterada no [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], inclusive o esquema de banco de dados de aplicativo de serviço. Se você quiser migrar para [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] o modo do SharePoint de uma versão [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]anterior ao, primeiro crie o novo ambiente do SharePoint instalando o SharePoint e [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] o modo do SharePoint. Para obter mais informações, consulte [Reporting Services instalação do modo sharepoint &#40;sharepoint 2010 e sharepoint 2013&#41;](../../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md).

 Quando o novo ambiente do SharePoint estiver em execução, você poderá escolher entre apenas uma migração de conteúdo ou uma migração completa no nível de banco de dados que inclui bancos de dados de conteúdo.

###  <a name="bkmk_content_only_migration"></a>Migração somente de conteúdo
 **Reporting Services migração somente de conteúdo:** Se você quiser copiar o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] conteúdo para um novo farm, precisará usar ferramentas como **RS. exe** para copiar o conteúdo para a nova instalação do SharePoint. Para obter mais informações sobre migrações somente de conteúdo, consulte o seguinte:

-   ** [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Scripts RSS:** Os scripts podem migrar conteúdo e recursos entre o modo nativo e os servidores de relatório no modo do SharePoint. Para obter mais informações, consulte [Sample Reporting Services rs.exe Script to Migrate Content between Report Servers](../tools/sample-reporting-services-rs-exe-script-to-copy-content-between-report-servers.md) e [Script RS.exe do Reporting Services que migra o conteúdo de um servidor de relatório para outro](https://azuresql.codeplex.com/releases/view/115207).

-   **Ferramenta de migração de Reporting Services:** A ferramenta pode copiar os itens de relatório de um servidor de modo nativo para um servidor de modo do SharePoint. Para obter mais informações, consulte [Ferramenta de migração do Reporting Services](https://www.microsoft.com/download/details.aspx?id=29560).

###  <a name="bkmk_full_migration"></a>Migração completa
 **Migração completa:** Se você estiver migrando bancos de dados de conteúdo do SharePoint [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] junto com os bancos de dados de catálogo para um novo farm, poderá seguir uma série de opções de backup e restauração resumidas neste tópico. Em alguns casos, você precisará usar uma ferramenta para a fase de restauração diferente da que você usou para a fase de backup. Por exemplo, você pode [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] usar Configuration Manager para fazer backup de chaves de criptografia de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] uma versão anterior do, mas precisa usar a administração central do SharePoint ou o PowerShell para [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] restaurar as chaves de criptografia para uma instalação do modo do SharePoint.

####  <a name="bkmk_databases"></a>Bancos de dados que você verá na migração concluída
 A tabela a seguir descreve os Bancos de dados do SQL Server relacionados ao [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que você terá depois que migrar com sucesso sua instalação do SharePoint do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] :

|Banco de dados|Nome de exemplo||
|--------------|------------------|-|
|Banco de dados de catálogo|ReportingService_ [GUID **do aplicativo de serviço\*] ()**|Usuário migra.|
|Banco de dados temporário|ReportingService_ [GUID do aplicativo de serviço] TempDB **(\*)**|Usuário migra.|
|Bancos de dados de alerta|ReportingService_[GUID do aplicativo de serviço]_Alerting|Criado quando um aplicativo de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] é criado.|

 **(\*)** Os nomes de exemplo mostrados na tabela seguem a Convenção de nomenclatura que o SSRS usa quando você cria um novo aplicativo de serviço do SSRS. Se você estiver migrando de um servidor diferente, seu catálogo e tempDBs terão os nomes da instalação original.

####  <a name="bkmk_backup_operations"></a>Operações de backup
 Esta seção descreve os tipos de informações que você precisa para migrar e as ferramentas ou processos que você usa para concluir o backup.

 ![Diagrama básico de Migração do SSRS SharePoint](../../../2014/sql-server/install/media/rs-sharepoint-migration.gif "Diagrama básico de Migração do SSRS SharePoint")

||Objetos|Método|Observações|
|-|-------------|------------|-----------|
|**1**|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]chaves de criptografia.|**Rskeymgmt. exe** ou [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager. Veja [Fazer backup e restaurar as chaves de criptografia do Reporting Services](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md).|As ferramentas observadas podem ser usadas para o backup, mas, para a operação de restauração, você usará as páginas de gerenciamento do aplicativo de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ou PowerShell.|
|**2**|Bancos de dados de conteúdo do SharePoint.||Faça backup do banco de dados e desanexe-o.<br /><br /> Confira a seção "Atualização da anexação do banco de dados" em [Determinar abordagem de atualização (SharePoint Server 2010) (https://technet.microsoft.com/library/cc263447.aspx)](https://technet.microsoft.com/library/cc263447.aspx).|
|**3**|Banco de dados do SQL Server que é o banco de dados de catálogo do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|Backup e restauração de banco de dados do SQL Server<br /><br /> ou<br /><br /> Anexar e desanexar banco de dados do SQL Server.||
|**4**|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]arquivos de configuração.|Cópia de arquivo simples.|Você só precisará copiar o rsreportserver.config se tiver feito personalizações ao arquivo. Exemplo do local padrão dos arquivos: C:\Program Files\Common Files\Microsoft Shared\Web Server Extensions\15\WebServices\Reporting<br /><br /> RSReportServer.config<br /><br /> Rssvrpolicy.config<br /><br /> Web.config para o aplicativo ASP.NET do Servidor de Relatório.<br /><br /> Machine.config para ASP.NET.|

####  <a name="bkmk_restore_operations"></a>Operações de restauração
 Esta seção descreve os tipos de informações que você precisa para migrar e as ferramentas ou processos que você usa para concluir a restauração. As ferramentas que você usa para restaurar podem ser diferentes das que você usou para o backup.

 Antes de concluir as etapas de restauração, você precisa instalar e configurar o novo Farm do SharePoint e modo do SharePoint do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Para obter mais informações sobre uma instalação básica [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] do modo do SharePoint, consulte [Reporting Services instalação do modo do sharepoint &#40;SharePoint 2010 e SharePoint 2013&#41;](../../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md).

||Objetos|Método|Observações|
|-|-------------|------------|-----------|
|**1**|Restaure bancos de dados de conteúdo do SharePoint para o novo farm.|Método "Atualização da anexação do banco de dados" do SharePoint.|Etapas básicas:<br /><br /> 1) Restaurar o banco de dados no novo servidor.<br /><br /> 2) Anexe o banco de dados de conteúdo a um aplicativo Web indicando a URL.<br /><br /> 3) O Get-SPWebapplication lista todos os aplicativos Web e as URLs.<br /><br /> Confira a seção "Atualização da anexação do banco de dados" em [Determinar abordagem de atualização (SharePoint Server 2010) (https://technet.microsoft.com/library/cc263447.aspx)](https://technet.microsoft.com/library/cc263447.aspx)e [Anexar bancos de dados e atualizar para o SharePoint Server 2010 (https://technet.microsoft.com/library/cc263299.aspx)](https://technet.microsoft.com/library/cc263299.aspx).|
|**2**|Restaure o banco de dados SQL que é o banco de dados de catálogo do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] (ReportServer).|Backup e restauração de bancos de dados SQL.<br /><br /> **or**<br /><br /> Anexar e desanexar bancos de dados SQL Server.|Na primeira vez que o banco de dados for usado, o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] atualizará o esquema de banco de dados conforme o necessário para que ele funcione com o ambiente do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .|
|**3**|Criar um novo aplicativo de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|Administração Central do SharePoint.|Quando você cria o novo aplicativo de serviço, configure-o para usar o banco de dados de servidor de relatório do qual você copiou.<br /><br /> Para obter mais informações sobre como usar a administração central do SharePoint, consulte a seção "etapa 3: criar um aplicativo de serviço Reporting Services" em [instalar Reporting Services modo do SharePoint para sharepoint 2013](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2013.md).<br /><br /> Para obter exemplos usando o PowerShell, confira a seção "Criar um aplicativo de serviço do Reporting Services usando o PowerShell" em [Serviço SharePoint do Reporting Services e aplicativos de serviço](../../../2014/reporting-services/reporting-services-sharepoint-service-and-service-applications.md).|
|**4**|Restaure os arquivos de configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|Cópia de arquivo simples.|Exemplo do local padrão dos arquivos: C:\Arquivos de Programas\Common Files\Microsoft Shared\Web Server Extensions\15\WebServices\Reporting.|
|**5**|Restaure as chaves de criptografia do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|Restaure o arquivo de backup de chave usando a página "SystemSettings" do aplicativo de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].<br /><br /> **or**<br /><br /> PowerShell.|Confira a seção "Gerenciamento de chaves" no tópico [Gerenciar um aplicativo de serviço SharePoint do Reporting Services](../../../2014/reporting-services/manage-a-reporting-services-sharepoint-service-application.md).|

#####  <a name="bkmk_additional_configuration"></a>Configuração adicional
 Dependendo de como seu ambiente do SharePoint anterior foi configurado, você poderá precisar concluir um ou mais das seguintes etapas:

1.  Configurar a autenticação NTLM para um aplicativo de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Para obter mais informações, veja [Configurar o email para um serviço de aplicativo do Reporting Services &#40;SharePoint 2010 e SharePoint 2013&#41;](../../reporting-services/install-windows/configure-e-mail-for-a-reporting-services-service-application.md)

##  <a name="bkmk_migrate_from_ctp"></a>Migrar de uma implantação SQL Server 2012
 Em um farm multisservidor, os usuários provavelmente terão os bancos de dados de Conteúdo e Catálogo em uma máquina diferente, nesse caso você realmente só precisará adicionar um novo servidor com o serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] instalado, para o farm do SharePoint e então remover o servidor antigo. Não há necessidade de copiar bancos de dados.

### <a name="backup-operations"></a>Operações de backup

1.  Backup das chaves de criptografia do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .

2.  Backup do aplicativo de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] na Administração Central do SharePoint (ou use o PowerShell). Isto também fará backup dos bancos de dados de aplicativo de serviço no SharePoint. Confira o tópico  [Aplicativos de serviço do SharePoint de backup e restauração do Reporting Services](../../../2014/reporting-services/backup-and-restore-reporting-services-sharepoint-service-applications.md)

3.  Se você tiver uma UEA (conta de execução autônoma conta) e a autenticação do Windows, faça uma nota das credenciais para que você possa usá-las para o processo de restauração.

4.  Para obter mais informações, consulte [Fazer backup de aplicativos de serviço no SharePoint 2013](https://technet.microsoft.com/library/ee428318.aspx).

### <a name="restore-operations"></a>Operações de restauração

1.  Restaurar o aplicativo de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] usando a Administração Central do SharePoint. Você também pode usar o PowerShell.

2.  Restaurar chaves de criptografia do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .

     Confira a seção "Gerenciamento de chaves" no tópico [Gerenciar um aplicativo de serviço SharePoint do Reporting Services](../../../2014/reporting-services/manage-a-reporting-services-sharepoint-service-application.md)

3.  Configure o UEA e as credenciais do Windows no aplicativo de serviço.

4.  Para obter mais informações, consulte [Restaurar aplicativos de serviço no SharePoint 2013](https://technet.microsoft.com/library/ee428305.aspx).

##  <a name="bkmk_additional_resources"></a> Recursos adicionais

-   [Introdução a upgrades para o SharePoint 2013 (https://technet.microsoft.com/library/ee833948.aspx)](https://technet.microsoft.com/library/ee833948.aspx).

-   [Visão geral do processo de upgrade para o SharePoint 2013 (https://technet.microsoft.com/library/cc262483.aspx)](https://technet.microsoft.com/library/cc262483.aspx).

## <a name="see-also"></a>Consulte Também
 [Atualizar e migrar Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md) [migrar uma instalação do Reporting Services &#40;modo nativo&#41;](../../reporting-services/install-windows/migrate-a-reporting-services-installation-native-mode.md)

