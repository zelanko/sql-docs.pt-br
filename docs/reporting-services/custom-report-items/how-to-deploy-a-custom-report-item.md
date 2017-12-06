---
title: "Como implantar um item de relatório personalizado | Microsoft Docs"
ms.custom: 
ms.date: 03/18/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: custom-report-items
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords: custom report items, deploying
ms.assetid: 80e97b0d-e355-4240-aebd-08cbc84089ed
caps.latest.revision: "26"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 39ecdd97ed53658b5daf1746997898a460647437
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2017
---
# <a name="how-to-deploy-a-custom-report-item"></a>Como implantar um item de relatório personalizado
  Para implantar um item de relatório personalizado no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], modifique os arquivos de configuração do servidor de relatório e copie os assemblies de componente em tempo de design e em tempo de execução nas pastas de aplicativo apropriadas para o Designer de Relatórios e o servidor de relatório.  
  
### <a name="to-deploy-a-custom-report-item"></a>Para implantar um item de relatório personalizado  
  
1.  Edite o arquivo Rsreportdesigner.config para configurar os componentes de item de relatório personalizado em tempo de execução e tempo de design para uso no designer. Observe que a entrada **ReportItemName** deve corresponder ao atributo **CustomReportItemAttribute** usado na classe **CustomReportItemDesigner**. Por exemplo:  
  
    ```  
    <ReportItems>  
       <ReportItem Name="Polygons" Type="PolygonsCRI.PolygonsCRI,PolygonsCRI"/>  
    </ReportItems>  
    <ReportItemDesigner>  
       <ReportItem Name="Polygons" Type="PolygonsCRI.PolygonsDesigner, PolygonsDesigner" />  
    </ReportItemDesigner>  
    <ReportItemConverter>  
       <Converter Source="Chart" Target="Polygons" Type="PolygonsCRI.PolygonsConverter, PolygonsDesigner" />  
    </ReportItemConverter>  
    ```  
  
2.  Edite o arquivo Rsreportserver.config para registrar o componente de item de relatório personalizado em tempo de execução. Por exemplo:  
  
    ```  
    <ReportItems>  
       <ReportItem Name="Polygons" Type="PolygonsCRI.PolygonsCRI,PolygonsCRI"/>  
    </ReportItems>  
    ```  
  
3.  Edite o arquivo Rsssrvpolicy.config para adicionar um **CodeGroup** que concede as permissões adequadas ao item de relatório personalizado. Por exemplo:  
  
    ```  
    <CodeGroup   
       class="UnionCodeGroup"   
       version="1"   
       PermissionSetName="FullTrust"  
       Description="This code group grants MyCustomReportItem.dll FullTrust permission. ">  
       <IMembershipCondition   
          class="UrlMembershipCondition"  
          version="1"  
       Url="C:\Program Files\Microsoft SQL Server\ MSRS10_50.SQLSERVER\Reporting Services\ReportServer\bin\MyCustomReportItem.dll" />  
    </CodeGroup>  
    ```  
  
4.  Copie a DLL de componente em tempo de execução de relatório personalizado para os diretórios %ProgramFiles%\Microsoft Visual Studio 9.0\Common7\IDE\PrivateAssemblies e \Arquivos de Programas\Microsoft SQL Server\MSRS10_50.SQLSERVER\Reporting Services\ReportServer\bin.  
  
5.  Copie a DLL de componente em tempo de design de item de relatório personalizado para o diretório %ProgramFiles%\Microsoft Visual Studio 9.0\Common7\IDE\PrivateAssemblies.  
  
## <a name="see-also"></a>Consulte também  
 [Arquivos de configuração do Reporting Services](../../reporting-services/report-server/reporting-services-configuration-files.md)   
 [Bibliotecas de classes de itens de relatório personalizados](../../reporting-services/custom-report-items/custom-report-item-class-libraries.md)  
  
  
