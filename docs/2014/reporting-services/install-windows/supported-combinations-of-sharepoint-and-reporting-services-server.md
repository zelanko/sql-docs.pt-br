---
title: Combinações com suporte do SharePoint e Reporting Services Server e suplemento (SQL Server 2014) | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- SharePoint mode
- add-in for sharepoint
ms.assetid: dc6a3372-db26-43f0-b7aa-f725acc635c2
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 05f0997cb73a156e54b22ad280fa5d6eb0ec7d73
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66108646"
---
# <a name="supported-combinations-of-sharepoint-and-reporting-services-server-and-add-in-sql-server-2014"></a>Combinações do SharePoint e do servidor e suplemento do Reporting Services com suporte (SQL Server 2014)
  Servidores de relatório do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] podem ser instalados no modo do SharePoint e integrados com uma implantação do SharePoint. Nem todos os recursos são compatíveis em todas as combinações de servidor de relatório, suplemento Reporting Services para SharePoint e produtos do SharePoint. Este tópico resume as combinações com suporte. No [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], a integração é um resultado da combinação de:  
  
-   Uma versão de um servidor de relatório do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] configurado para o modo do SharePoint.  
  
-   Um produto SharePoint  
  
-   O suplemento [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para produtos SharePoint, que você instala nos servidores do SharePoint.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]** SharePoint 2013 &#124; SharePoint 2010 &#124; SharePoint 2007|  
  
## <a name="supported-combinations-of-sharepoint-and-reporting-services-components"></a>Combinações de componentes do SharePoint e do Reporting Services com suporte  
 A tabela a seguir resume as combinações com suporte do servidor de relatório, o suplemento do Reporting Services para produtos SharePoint e produtos SharePoint. As combinações que não estão listadas na tabela a seguir não têm suporte  
  
### <a name="supported-combinations"></a>Combinações com suporte  
  
||Servidor de relatório|Suplemento|Versão do SharePoint|Suportado|  
|-|-------------------|-------------|------------------------|---------------|  
|1|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|SharePoint 2013|Sim|  
|2|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|SharePoint 2010|Sim|  
|3|[!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]|SharePoint 2013|Sim|  
|4|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|SharePoint 2010|Sim<br /><br /> Exceção: a integração do Power View não tem suporte.|  
|5|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|SharePoint 2010|Sim|  
|6|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|SharePoint 2010|Sim|  
|7|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]|SharePoint 2010|Sim|  
|8|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|SharePoint 2010|Sim|  
|9|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP2|SharePoint 2007|Sim|  
|10|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP2|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] R2|SharePoint 2010|Sim|  
|11|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP2|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP2|SharePoint 2007|Sim|  
  
 Para obter mais informações [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] sobre os recursos e modos de servidor de relatório, consulte [Reporting Services servidor de relatório](../reporting-services-report-server.md).  
  
 **Observações adicionais:**  
  
-   O suporte do SharePoint 2013, inclusive integração do Power View, requer o servidor de relatório do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e a versão do suplemento do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] do SQL Server 2012 SP1 ou posterior.  
  
-   O Power View foi introduzido no [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]. Consequentemente, a integração do Power View com o SharePoint 2010 exige o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ou posterior do suplemento.  
  
-   O suplemento SQL Server 2008 R2 não é compatível com os servidores de relatório do SQL Server 2012 (ou posterior). O instalador de pré-requisito do SharePoint 2010 instala automaticamente o suplemento SQL Server 2008 R2. Ele deve ser desinstalado antes de instalar versões mais recentes do suplemento. A atualização no local do suplemento não tem suporte.  
  
-   **Atualização:** o SharePoint 2010 com o suplemento [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] instalado não pode ser atualizado no local para o SharePoint 2013. O SharePoint 2013 exige o [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] ou posterior do suplemento [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e o servidor de relatório. Para obter mais informações, consulte [Atualizar e migrar o Reporting Services](upgrade-and-migrate-reporting-services.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Onde encontrar o suplemento de Reporting Services para produtos do SharePoint](where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)   
 [Recursos com suporte nas edições do SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)   
 [Atualizar e migrar o Reporting Services](upgrade-and-migrate-reporting-services.md)  
  
  
