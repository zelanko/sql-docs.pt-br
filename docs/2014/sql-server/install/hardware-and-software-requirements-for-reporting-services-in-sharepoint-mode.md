---
title: Requisitos de hardware e software para Reporting Services no modo do SharePoint | Microsoft Docs
ms.custom: ''
ms.date: 01/09/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: ed91877d-4f74-4266-a932-b824b4810c99
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 56ddfce4fc1812e99870c22eeb0e15be64c5decb
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "75245630"
---
# <a name="hardware-and-software-requirements-for-reporting-services-in-sharepoint-mode"></a>Requisitos de hardware e software para o Reporting Services no modo do SharePoint

  Este tópico descreve os pré-requisitos, os requisitos de hardware e as considerações [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] de instalação para execução no modo do SharePoint. Como o modo SharePoint do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] requer um servidor do SharePoint, a maioria dos requisitos são baseados no ambiente do SharePoint. Para servidores de relatório no modo nativo, o seu hardware deve atender aos requisitos mínimos de hardware e software para executar o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Para obter mais informações, consulte [Hardware and Software Requirements for Installing SQL Server 2014](hardware-and-software-requirements-for-installing-sql-server.md).  
  
-   [Pré-requisitos](#bkmk_prereq)  
  
-   [Requisitos de banco de dados do servidor de relatório](#bkmk_report_server_database)  
  
-   [Requisitos de Power View](#bkmk_powerview)  
  
-   [Mais informações](#bkmk_more_information)  
  
##  <a name="bkmk_prereq"></a> Pré-requisitos  
  
-   Para instalações locais, a conta registrada durante a instalação do SharePoint e do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] precisa ser membro do grupo de administradores no sistema operacional local. A conta de instalação não precisa ser membro do grupo de administradores de farm do SharePoint.  
  
     Para obter mais informações, consulte [Permissões de conta e configurações de segurança no SharePoint 2013](https://technet.microsoft.com/library/cc678863.aspx).  
  
-   O [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que é executado no modo do SharePoint exige o SharePoint Server. Para obter mais informações sobre os requisitos e as configurações do SharePoint, consulte o seguinte:  
  
    -   [Requisitos de hardware e software (SharePoint 2013)](https://go.microsoft.com/fwlink/p/?LinkId=256365) (https://go.microsoft.com/fwlink/p/?LinkId=256365)  
  
    -   [Gerenciamento de capacidade e dimensionamento para o SharePoint Server 2013](https://technet.microsoft.com/library/cc261700.aspx)  
  
    -   [Requisitos de software para o business intelligence (SharePoint 2013)](https://go.microsoft.com/fwlink/p/?LinkId=256367)  
  
    -   [Requisitos de hardware e software (SharePoint Server 2010)](https://technet.microsoft.com/library/cc262485\(v=office.14\))  
  
    -   [Gerenciamento de capacidade e dimensionamento para o SharePoint Server 2010](https://technet.microsoft.com/library/cc261700.aspx\(v=office.14\))  
  
-   Se você quiser atualizar uma instalação existente do SharePoint do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] com o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], consulte [Upgrade and Migrate Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md).  
  
-   Verifique se o serviço **Administração do SharePoint 2013** foi iniciado no Windows Server Manager.  
  
###  <a name="bkmk_report_server_database"></a>Requisitos de banco de dados do servidor de relatório  
  
-   Os produtos e as tecnologias do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e do SharePoint usam bancos de dados relacionais do SQL Server para armazenar dados de aplicativo.  
  
-   O [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] requer uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] de uma edição compatível do SQL Server. Para obter mais informações sobre requisitos de hardware e software, consulte [Hardware and Software Requirements for Installing SQL Server 2014](hardware-and-software-requirements-for-installing-sql-server.md).  
  
-   Os produtos do SharePoint poderão usar uma instância de banco de dados existente. Se uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] não estiver instalada, a Instalação dos Produtos do SharePoint instalará o SQL Server Express Edition para os bancos de dados de aplicativo do SharePoint.  
  
-   A instância do servidor de relatório não pode usar o SQL Server Express Edition para seu banco de dados. No entanto, a instância do SQL Server Express Edition instalada pelo produto ou tecnologia do SharePoint pode existir lado a lado com outras edições do Mecanismo de Banco de Dados.  
  
##  <a name="bkmk_powerview"></a>[!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] Requisitos do

 Analise a [documentação do Power View](https://office.microsoft.com/excel-help/power-view-explore-visualize-and-present-your-data-HA102835634.aspx) mais atualizada em Office.Microsoft.com. O [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] é um recurso do Microsoft Excel 2013 e faz parte do suplemento [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Reporting Services para Microsoft SharePoint Server 2010 e 2013 Enterprise Editions.  
  
##  <a name="bkmk_more_information"></a> Mais informações

 Para obter informações sobre as alterações do SharePoint, consulte [alterações do sharepoint 2010 para o sharepoint 2013](https://technet.microsoft.com/library/ff607742\(office.15\).aspx) (https://technet.microsoft.com/library/ff607742(office.15).aspx).  
  
 [Notas de versão do SQL Server 2014](https://go.microsoft.com/fwlink/?LinkID=296445).  
  
