---
title: "Como: implantar um Item de relatório personalizado | Microsoft Docs"
ms.custom: 
ms.date: 03/18/2017
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
- custom report items, deploying
ms.assetid: 80e97b0d-e355-4240-aebd-08cbc84089ed
caps.latest.revision: 26
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: ab5f90df0ff1d3c91a641811e54bf4394506c2a4
ms.contentlocale: pt-br
ms.lasthandoff: 06/13/2017

---
# <a name="how-to-deploy-a-custom-report-item"></a>Como implantar um item de relatório personalizado
  Para implantar um item de relatório personalizado no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], modifique os arquivos de configuração do servidor de relatório e copie os assemblies de componente em tempo de design e em tempo de execução nas pastas de aplicativo apropriadas para o Designer de Relatórios e o servidor de relatório.  
  
### <a name="to-deploy-a-custom-report-item"></a>Para implantar um item de relatório personalizado  
  
1.  Edite o arquivo Rsreportdesigner.config para configurar os componentes de item de relatório personalizado em tempo de execução e tempo de design para uso no designer. Observe que o **ReportItemName** a entrada deve corresponder a **CustomReportItemAttribute** atributo usado em seu **CustomReportItemDesigner** classe. Por exemplo:  
  
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
  
3.  Edite o arquivo rsssrvpolicy para adicionar um **CodeGroup** que concede as permissões apropriadas para o item de relatório personalizado. Por exemplo:  
  
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
 [Bibliotecas de classe de Item de relatório personalizado](../../reporting-services/custom-report-items/custom-report-item-class-libraries.md)  
  
  
