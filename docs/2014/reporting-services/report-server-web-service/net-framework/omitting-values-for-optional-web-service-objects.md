---
title: Omitindo valores para objetos opcionais de serviço Web | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- Web service [Reporting Services], omitted values
- XML Web service [Reporting Services], omitted values
- Report Server Web service, omitted values
- omitting values [Reporting Services]
ms.assetid: ceb68b8b-9214-4745-abc9-f47f33ecd6f7
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 3858f73e1b332acfa1a1bbc640007f6f0884abff
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63260706"
---
# <a name="omitting-values-for-optional-web-service-objects"></a>Omitindo valores para objetos de serviço Web opcionais
  Propriedades de vários tipos complexos de serviço Web Servidor de Relatórios têm uma propriedade complementar conhecida como propriedade Specified. O nome da propriedade consiste no nome de propriedade original com a palavra "Especificada" anexada a ele. A presença dessa propriedade indica que um valor da propriedade original às vezes pode ser omitido. Este é um resultado direto da conversão da WSDL (Web Service Description Language) em uma classe proxy [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]. Por exemplo, a propriedade de serviço Web <xref:ReportService2010.DataSourceDefinition.Enabled%2A> do tipo complexo <xref:ReportService2010.DataSourceDefinition> tem uma propriedade associada nomeada <xref:ReportService2010.DataSourceDefinition.EnabledSpecified%2A>. Se você estiver criando um aplicativo e não quiser definir um valor para a propriedade <xref:ReportService2010.DataSourceDefinition.Enabled%2A>, não precisará fornecer um valor para <xref:ReportService2010.DataSourceDefinition.Enabled%2A>; o valor padrão de `true` é usado. Porém, você ainda precisa definir <xref:ReportService2010.DataSourceDefinition.EnabledSpecified%2A> como `false`. Se você fornecer um valor para a propriedade <xref:ReportService2010.DataSourceDefinition.Enabled%2A>, precisará definir <xref:ReportService2010.DataSourceDefinition.EnabledSpecified%2A> igual a `true`. Esse é o caso de propriedades graváveis. Para propriedades somente leitura, você não precisa tomar uma ação.  
  
> [!IMPORTANT]  
>  A falha em especificar uma propriedade usando a técnica supracitada pode resultar em comportamento de serviço Web imprevisível.  
  
 Os tipos de dados que geralmente exigem que você manipule a propriedade adicional especificada `Boolean`são `DateTime`, e `Enumeration`.  
  
 Para obter um exemplo, consulte o método <xref:ReportService2010.ReportingService2010.CreateDataSource%2A>.  
  
## <a name="see-also"></a>Consulte Também  
 [Criando aplicativos usando o serviço Web e o .NET Framework](building-applications-using-the-web-service-and-the-net-framework.md)   
 [Referência técnica &#40;SSRS&#41;](../../technical-reference-ssrs.md)  
  
  
