---
title: Propriedades do Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.topic: reference
helpviewer_keywords:
- report servers [Reporting Services], properties
- properties [Reporting Services], about properties
- reports [Reporting Services], properties
- Report Server Web service, properties
- report properties [Reporting Services]
- XML Web service [Reporting Services], properties
- Web service [Reporting Services], properties
- properties [Reporting Services]
ms.assetid: 8c855194-4c20-4ecc-a328-5137d54b560c
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 176c823af74d2b9842477d02c4e560984673dc21
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48061666"
---
# <a name="reporting-services-properties"></a>Propriedades do Reporting Services
  O servidor de relatório define um conjunto de propriedades do sistema globais para ele e um conjunto de propriedades de item associadas a um item individual armazenado no banco de dados do servidor de relatório. As propriedades definidas pelo servidor de relatório não podem ser excluídas e, em alguns casos, são somente leitura. Um aplicativo pode estender as propriedades do sistema e as propriedades do item acrescentando propriedades definidas pelo usuário adicionais a elas.  
  
 Os métodos de serviço Web a seguir recuperam e definem propriedades do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].  
  
|Método|Ação|  
|------------|------------|  
|<xref:ReportService2010.ReportingService2010.GetProperties%2A>|Retorna os valores de uma ou mais propriedades de um item do banco de dados do servidor de relatório.|  
|<xref:ReportService2010.ReportingService2010.GetSystemProperties%2A>|Retorna uma ou mais propriedades do sistema.|  
|<xref:ReportService2010.ReportingService2010.SetProperties%2A>|Define uma ou mais propriedades de um item no banco de dados do servidor de relatório.|  
|<xref:ReportService2010.ReportingService2010.SetSystemProperties%2A>|Define uma ou mais propriedades do sistema.|  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Description|  
|-----------|-----------------|  
|[Propriedades do item do servidor de relatório](reporting-services-properties-report-server-item-properties.md)|Descreve as propriedades específicas do item no [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].|  
|[Propriedades do sistema do Servidor de Relatório](reporting-services-properties-report-server-system-properties.md)|Descreve as propriedades específicas do sistema no [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].|  
  
## <a name="see-also"></a>Consulte também  
 [Criando aplicativos usando o serviço Web e o .NET Framework](building-applications-using-the-web-service-and-the-net-framework.md)   
 [Serviço Web do Servidor de Relatório](../report-server-web-service.md)   
 [Referência técnica &#40;SSRS&#41;](../../technical-reference-ssrs.md)  
  
  
