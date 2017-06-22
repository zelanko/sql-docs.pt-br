---
title: "Combinações do SharePoint e do servidor do Reporting Services com suporte | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 10/07/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SharePoint mode
- add-in for sharepoint
- rsSharePoint
ms.assetid: dc6a3372-db26-43f0-b7aa-f725acc635c2
caps.latest.revision: 39
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 2e66cac836de44e8d2a9f23d88a600daaa26c0d1
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="supported-combinations-of-sharepoint-and-reporting-services-server"></a>Combinações com suporte do SharePoint e do servidor do Reporting Services
[!INCLUDE[feedback_stackoverflow_msdn_connect_md](../../includes/feedback-stackoverflow-msdn-connect-md.md)]

  Um relatório de servidor [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] instalado no modo do SharePoint requer uma versão do SharePoint e o suplemento [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] (rsSharePoint.msi) para produtos do SharePoint, que você instala nos servidores do SharePoint.  Este tópico resume as combinações com suporte.  
  
## <a name="supported-combinations-of-sharepoint-and-reporting-services-components"></a>Combinações de componentes do SharePoint e do Reporting Services com suporte  
 A tabela a seguir resume as combinações com suporte do servidor de relatório, o suplemento do Reporting Services para produtos SharePoint e produtos SharePoint. As combinações que não estão listadas na tabela a seguir não têm suporte  
  
### <a name="supported-combinations"></a>Combinações com suporte  
  
||Servidor de relatório|Suplemento|Versão do SharePoint|  
|-|-------------------|-------------|------------------------|  
|1|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]|SharePoint 2016|  
|2|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]|SharePoint 2013|  
|3|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|SharePoint 2013|  
|4|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|SharePoint 2010|  
|5|SQL Server 2012 SP3|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e SQL Server 2012 SP3|SharePoint 2013|  
|6|SQL Server 2012 SP2|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e SQL Server 2012 SP2|SharePoint 2013|  
|7|[!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]|SharePoint 2013|  
|8|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]*|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|SharePoint 2010|  
|9|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|SharePoint 2010|  
|10|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|SharePoint 2010|  
|11|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]|SharePoint 2010|  
|12|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|SharePoint 2010|  
|13|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP2|SharePoint 2007|  
|14|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP2|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] R2|SharePoint 2010|  
|15|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP2|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP2|SharePoint 2007|  
  
 Exceção: a integração do Power View não tem suporte.  
  
 Para obter links para as páginas de download de suplementos, consulte [Onde encontrar o suplemento Reporting Services para produtos do SharePoint](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md).  
  
 **Observações adicionais:**  

- Certifique-se de atualizar todos os servidores do SharePoint no farm. Isso inclui os servidores front-end da Web e de aplicativos.

-   O suporte do SharePoint 2016, inclusive integração do Power View, requer o servidor de relatório do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e a versão do suplemento do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] do SQL Server 2016 ou posterior.  

-   O suporte do SharePoint 2013, inclusive integração do Power View, requer o servidor de relatório do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e a versão do suplemento do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] do SQL Server 2012 SP1 ou posterior.  
  
-   O Power View foi introduzido no [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]. Consequentemente, a integração do Power View com o SharePoint 2010 exige o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ou posterior do suplemento.  
  
-   O suplemento SQL Server 2008 R2 não é compatível com os servidores de relatório do SQL Server 2012 (ou posterior). O instalador de pré-requisito do SharePoint 2010 instala automaticamente o suplemento SQL Server 2008 R2. Ele deve ser desinstalado antes de instalar versões mais recentes do suplemento. A atualização no local do suplemento não tem suporte.  
  
-   **Atualização:** o SharePoint 2010 com o suplemento [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] instalado não pode ser atualizado no local para o SharePoint 2013. O SharePoint 2013 exige o [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] ou posterior do suplemento [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e o servidor de relatório. Para obter mais informações, consulte [Atualizar e migrar o Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md).  
  
## <a name="see-also"></a>Consulte também  
 [Onde encontrar o suplemento Reporting Services para produtos do SharePoint](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)   
 [Recursos com suporte nas edições do SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)   
 [Requisitos de hardware e software para a instalação do SQL Server 2016](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)  
  
  


