---
title: Como implantar um item de relatório personalizado | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- custom report items, deploying
ms.assetid: 80e97b0d-e355-4240-aebd-08cbc84089ed
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 2b41519ee6a6d31be33d92c8fbdf2ab503c93ec1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63265076"
---
# <a name="how-to-deploy-a-custom-report-item"></a>Como implantar um item de relatório personalizado
  Para implantar um item de relatório personalizado no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], modifique os arquivos de configuração do servidor de relatório e copie os assemblies de componente em tempo de design e em tempo de execução nas pastas de aplicativo apropriadas para o Designer de Relatórios e o servidor de relatório.  
  
### <a name="to-deploy-a-custom-report-item"></a>Para implantar um item de relatório personalizado  
  
1.  Edite o arquivo Rsreportdesigner.config para configurar os componentes de item de relatório personalizado em tempo de execução e tempo de design para uso no designer. Observe que a entrada `ReportItemName` deve corresponder ao atributo `CustomReportItemAttribute` usado em sua classe `CustomReportItemDesigner`. Por exemplo:  
  
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
  
3.  Edite o arquivo Rsssrvpolicy.config para adicionar um `CodeGroup` que concede as permissões adequadas ao item de relatório personalizado. Por exemplo:  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Arquivos de configuração do Reporting Services](../report-server/reporting-services-configuration-files.md)   
 [Bibliotecas de classes de itens de relatório personalizados](custom-report-item-class-libraries.md)  
  
  
