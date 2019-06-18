---
title: Operações de backup e restauração para o Reporting Services | Microsoft Docs
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
ms.assetid: 157bc376-ab72-4c99-8bde-7b12db70843a
ms.date: 05/08/2019
ms.openlocfilehash: 9598804150f150cb9bf6050eb39048892219cc26
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65580521"
---
# <a name="backup-and-restore-operations-for-reporting-services"></a>Operações de backup e restauração para o Reporting Services

  Este artigo fornece uma visão geral de todos os arquivos de dados usados em uma instalação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e descreve quando e como você deve fazer backup dos arquivos. O desenvolvimento de um plano de backup e restauração para os arquivos do banco de dados do servidor de relatório é a parte mais importante de uma estratégia de recuperação. No entanto, uma estratégia de recuperação mais abrangente incluiria backups de chaves de criptografia, assemblies ou extensões personalizados, arquivos de configuração e arquivos de origem para relatórios.  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] | Modo do SharePoint do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  

> [!NOTE]
> A integração do Reporting Services ao SharePoint não está mais disponível após o SQL Server 2016.
  
 As operações de backup e restauração são usadas com frequência para mover todo ou parte de uma instalação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] :  
  
-   Se estiver movendo apenas os bancos de dados do servidor de relatório, poderá usar o backup e restauração ou anexar e desanexar para realocar os bancos de dados em uma instância diferente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, consulte [Movendo os bancos de dados do servidor de relatório para outro computador &#40;modo nativo do SSRS&#41;](../../reporting-services/report-server/moving-the-report-server-databases-to-another-computer-ssrs-native-mode.md).  
  
-   Mover uma instalação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para um computador novo é chamado de migração. Quando você migra uma instalação, o Programa de Instalação é executado para instalar uma nova instância do servidor de relatório e, em seguida, os dados da instância são copiados para o novo computador. Para obter mais informações sobre como migrar uma instalação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], consulte os seguintes artigos:  
  
    - [Atualizar e migrar o Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)  
    - [Migrar uma instalação do Reporting Services &#40;modo nativo&#41;](../../reporting-services/install-windows/migrate-a-reporting-services-installation-native-mode.md)  

    ::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
  
    - [Migrar uma instalação do Reporting Services &#40;modo do SharePoint&#41;](../../reporting-services/install-windows/migrate-a-reporting-services-installation-sharepoint-mode.md)  

    ::: moniker-end
  
## <a name="backing-up-the-report-server-databases"></a>Fazendo backup dos bancos de dados do servidor de relatório  
 Uma vez que um servidor de relatório é um servidor sem monitoração de estado, os dados de todos os aplicativos são armazenados nos bancos de dados **reportserver** e **reportservertempdb** que são executados em uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] . É possível fazer backup dos bancos de dados **reportserver** e **reportservertempdb** usando um dos métodos com suporte para fazer backup dos bancos de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Veja algumas recomendações específicas para bancos de dados de servidor de relatório:  
  
-   Use o modelo de recuperação completo para fazer backup do banco de dados **reportserver**.  
  
-   Use o modelo de recuperação simples para fazer backup do banco de dados **reportservertempdb**.  
  
-   Você pode usar agendas de backup diferentes para cada banco de dados. O único motivo para fazer backup do **reportservertempdb** é evitar ter que recriá-lo se houver uma falha de hardware. No caso de uma falha de hardware, não é necessário recuperar os dados no **reportservertempdb**, mas você precisará da estrutura da tabela. Se você perder o **reportservertempdb**, o único modo de reverter isso é recriar o banco de dados de servidor de relatório. Se você recriar o **reportservertempdb**, é importante que você tenha o mesmo nome que o banco de dados do servidor de relatório primário.  
  
 Para obter mais informações sobre backup e recuperação dos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bancos de dados relacionais [Fazer backup e restaurar bancos de dados do SQL Server](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md).  

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"  

> [!IMPORTANT]  
>  Se o servidor de relatório estiver no modo do SharePoint, haverá bancos de dados adicionais com os quais se preocupar, incluindo bancos de dados de configuração do SharePoint e o banco de dados de alertas do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. No modo do SharePoint, três bancos de dados são criados para cada aplicativo de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Os bancos de dados **reportserver**, **reportservertempdb**e **dataalerting** . Para obter mais informações, consulte [Fazer backup e restaurar aplicativos de serviço SharePoint do Reporting Services](../../reporting-services/report-server-sharepoint/backup-and-restore-reporting-services-sharepoint-service-applications.md)  

::: moniker-end
  
## <a name="backing-up-the-encryption-keys"></a>Fazendo backup das chaves de criptografia  
 Você deve fazer backup das chaves de criptografia ao configurar uma instalação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] pela primeira vez. Você também deve fazer backup das chaves sempre que alterar a identidade das contas de serviço ou renomear o computador. Para saber mais, confira [Back Up and Restore Reporting Services Encryption Keys](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md). 

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"

Para servidores de relatório do modo do SharePoint, confira a seção "Gerenciamento de chaves" de [Manage a Reporting Services SharePoint Service Application](../../reporting-services/report-server-sharepoint/manage-a-reporting-services-sharepoint-service-application.md)(Gerenciar um aplicativo de serviço SharePoint do Reporting Services).  

::: moniker-end
  
## <a name="backing-up-the-configuration-files"></a>Fazendo backup dos arquivos de configuração  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] usa arquivos de configuração para armazenar as configurações do aplicativo. Você deve fazer backup dos arquivos quando configurar o servidor pela primeira vez e depois de implantar quaisquer extensões personalizadas. Os arquivos dos quais deve ser feito backup incluem:  
  
-   RSReportServer.config  
  
-   Rssvrpolicy.config  
  
-   Rsmgrpolicy.config  
  
-   Reportingservicesservice.exe.config  
  
-   Web.config para o aplicativo [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] do Servidor de Relatório
  
-   Machine.config para [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)]  
  
## <a name="backing-up-data-files"></a>Fazendo backup de arquivos de dados  
 Faça backup dos arquivos criados e mantidos no Designer de Relatórios. Eles incluem arquivos de definição de relatórios (.rdl), arquivos de fontes de dados compartilhadas (.rds), arquivos de exibição de dados (.dv), arquivos de fonte de dados (.ds), arquivos de projeto do servidor de relatório (.rptproj) e arquivos de solução de relatórios (.sln).  
  
 Lembre-se de fazer backup de quaisquer arquivos de script (.rss) criados para as tarefas de administração ou de implantação.  
  
 Verifique se você tem uma cópia de backup de todas as extensões e assemblies personalizados que você está usando.  

## <a name="next-steps"></a>Próximas etapas

[Banco de dados do servidor de relatório](../../reporting-services/report-server/report-server-database-ssrs-native-mode.md)   
[Arquivos de configuração do Reporting Services](../../reporting-services/report-server/reporting-services-configuration-files.md)   
[Utilitário rskeymgmt](../../reporting-services/tools/rskeymgmt-utility-ssrs.md)   
[Copiar bancos de dados com backup e restauração](../../relational-databases/databases/copy-databases-with-backup-and-restore.md)   
[Administrar um banco de dados do servidor de relatório](../../reporting-services/report-server/administer-a-report-server-database-ssrs-native-mode.md)   
[Configurar e gerenciar chaves de criptografia](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md)  

Ainda tem dúvidas? [Experimente perguntar no fórum do Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
