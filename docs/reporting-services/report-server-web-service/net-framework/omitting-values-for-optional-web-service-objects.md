---
title: "Omitindo valores de objetos de serviço Web opcional | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Web service [Reporting Services], omitted values
- XML Web service [Reporting Services], omitted values
- Report Server Web service, omitted values
- omitting values [Reporting Services]
ms.assetid: ceb68b8b-9214-4745-abc9-f47f33ecd6f7
caps.latest.revision: 36
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 727d9ccd8cd1e40d89cfe74291edae92988b407c
ms.openlocfilehash: 3532a470bd036e0128a8df21ca391210cf7209a2
ms.contentlocale: pt-br
ms.lasthandoff: 08/09/2017

---
# <a name="omitting-values-for-optional-web-service-objects"></a>Omitindo valores para objetos de serviço Web opcionais
  Propriedades de vários tipos complexos de serviço Web servidor de relatório têm uma propriedade associada conhecida como a propriedade especificada. O nome da propriedade consiste no nome de propriedade original com a palavra "Especificada" anexada a ele. A presença dessa propriedade indica que um valor da propriedade original às vezes pode ser omitido. Este é um resultado direto da conversão da WSDL (Web Service Description Language) em uma classe proxy [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]. Por exemplo, a propriedade de serviço Web <xref:ReportService2010.DataSourceDefinition.Enabled%2A> do tipo complexo <xref:ReportService2010.DataSourceDefinition> tem uma propriedade associada nomeada <xref:ReportService2010.DataSourceDefinition.EnabledSpecified%2A>. Se você estiver criando um aplicativo e não quiser definir um valor para o <xref:ReportService2010.DataSourceDefinition.Enabled%2A> propriedade, você não precisa fornecer um valor para <xref:ReportService2010.DataSourceDefinition.Enabled%2A>; o valor padrão de **true** é usado. No entanto, você ainda precisa definir <xref:ReportService2010.DataSourceDefinition.EnabledSpecified%2A> para **false**. Se você fornecer um valor para o <xref:ReportService2010.DataSourceDefinition.Enabled%2A> propriedade, você precisa definir <xref:ReportService2010.DataSourceDefinition.EnabledSpecified%2A> igual a **true**. Esse é o caso de propriedades graváveis. Para propriedades somente leitura, você não precisa tomar uma ação.  
  
> [!IMPORTANT]  
>  A falha em especificar uma propriedade usando a técnica supracitada pode resultar em comportamento de serviço Web imprevisível.  
  
 Os tipos de dados que costumam exigem que você trate a propriedade especificada adicional são **booliano**, **DateTime**, e **enumeração**.  
  
 Para obter um exemplo, consulte o método <xref:ReportService2010.ReportingService2010.CreateDataSource%2A>.  
  
## <a name="see-also"></a>Consulte também  
 [Criando aplicativos que usam o serviço Web e o .NET Framework](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [Referência técnica &#40; SSRS &#41;](../../../reporting-services/technical-reference-ssrs.md)  
  
  

