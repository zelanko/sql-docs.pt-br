---
title: Combinações do SharePoint e do servidor e (SQL Server 2014) do suplemento Reporting Services com suporte | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- SharePoint mode
- add-in for sharepoint
ms.assetid: dc6a3372-db26-43f0-b7aa-f725acc635c2
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 158110c1273c64cb9fdf86d1b9f4bc4a40d780a8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63143964"
---
# <a name="supported-combinations-of-sharepoint-and-reporting-services-server-and-add-in-sql-server-2014"></a>Combinações do SharePoint e do servidor e suplemento do Reporting Services com suporte (SQL Server 2014)
  Servidores de relatório do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] podem ser instalados no modo do SharePoint e integrados com uma implantação do SharePoint. Nem todos os recursos são compatíveis em todas as combinações de servidor de relatório, suplemento Reporting Services para SharePoint e produtos do SharePoint. Este tópico resume as combinações com suporte. No [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], a integração é um resultado da combinação de:  
  
-   Uma versão de um servidor de relatório do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] configurado para o modo do SharePoint.  
  
-   Um produto SharePoint  
  
-   O suplemento [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para produtos SharePoint, que você instala nos servidores do SharePoint.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  SharePoint 2013 &#124; SharePoint 2010 &#124; SharePoint 2007|  
  
## <a name="supported-combinations-of-sharepoint-and-reporting-services-components"></a>Combinações de componentes do SharePoint e do Reporting Services com suporte  
 A tabela a seguir resume as combinações com suporte do servidor de relatório, o suplemento do Reporting Services para produtos SharePoint e produtos SharePoint. As combinações que não estão listadas na tabela a seguir não têm suporte  
  
### <a name="supported-combinations"></a>Combinações com suporte  
  
||Servidor de relatório|Suplemento|Versão do SharePoint|Tem suporte|  
|-|-------------------|-------------|------------------------|---------------|  
|1|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|SharePoint 2013|Sim|  
|2|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|SharePoint 2010|Sim|  
|3|[!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]|SharePoint 2013|Sim|  
|4|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|SharePoint 2010|Sim<br /><br /> Exceção: Não há suporte para a integração do Power view.|  
|5|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|SharePoint 2010|Sim|  
|6|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|SharePoint 2010|Sim|  
|7|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]|SharePoint 2010|Sim|  
|8|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|SharePoint 2010|Sim|  
|9|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP2|SharePoint 2007|Sim|  
|10|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP2|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] R2|SharePoint 2010|Sim|  
|11|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP2|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP2|SharePoint 2007|Sim|  
  
 Para obter mais informações sobre [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] recursos e modos de servidor de relatório, consulte [servidor de relatório do Reporting Services](../reporting-services-report-server.md).  
  
 **Observações adicionais:**  
  
-   O suporte do SharePoint 2013, inclusive integração do Power View, requer o servidor de relatório do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e a versão do suplemento do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] do SQL Server 2012 SP1 ou posterior.  
  
-   O Power View foi introduzido no [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]. Consequentemente, a integração do Power View com o SharePoint 2010 exige o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ou posterior do suplemento.  
  
-   O suplemento SQL Server 2008 R2 não é compatível com os servidores de relatório do SQL Server 2012 (ou posterior). O instalador de pré-requisito do SharePoint 2010 instala automaticamente o suplemento SQL Server 2008 R2. Ele deve ser desinstalado antes de instalar versões mais recentes do suplemento. A atualização no local do suplemento não tem suporte.  
  
-   **Atualização:** SharePoint 2010 com o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] suplemento instalado, não pode ser atualizado in-loco para o SharePoint 2013. O SharePoint 2013 exige o [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] ou posterior do suplemento [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e o servidor de relatório. Para obter mais informações, consulte [Atualizar e migrar o Reporting Services](upgrade-and-migrate-reporting-services.md).  
  
## <a name="see-also"></a>Consulte também  
 [Onde encontrar o suplemento Reporting Services para produtos do SharePoint](where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)   
 [Recursos com suporte nas edições do SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)   
 [Atualizar e migrar o Reporting Services](upgrade-and-migrate-reporting-services.md)  
  
  
