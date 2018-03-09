---
title: Script e PowerShell com o Reporting Services | Microsoft Docs
ms.custom: 
ms.date: 09/14/2015
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: tools
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- scripts [Reporting Services]
- Reporting Services, scripting
- scripting [Reporting Services]
ms.assetid: 1ac2646d-ed5a-4436-b18f-2150c33f3d87
caps.latest.revision: 
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 0702fd257a20656ba61ebced29f17a971ee06f45
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/09/2018
---
# <a name="scripting-and-powershell-with-reporting-services"></a>Script e PowerShell com o Reporting Services
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] dá suporte a uma ampla variedade de cenários de desenvolvimento e gerenciamento por meio de script, incluindo o utilitário de linha de comando rs.exe, os cmdlets do PowerShell para servidores de relatório no modo SharePoint e aproveitando o modelo de objeto [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] do PowerShell para os modos nativo e SharePoint.  
  
-   Os administradores podem escrever o script em [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] para automatizar o modo como eles implantam e administram uma instalação de servidor de relatório. Os administradores também podem gerar e executar scripts [!INCLUDE[tsql](../../includes/tsql-md.md)] que criam, configuram e atualizam um banco de dados de servidor de relatório. Os administradores também podem usar o registro e os recursos de script de reprodução em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] para automatizar tarefas de manutenção de rotina.  
  
-   Os desenvolvedores podem criar aplicativos personalizados que incluem script. Você pode executar o script que faz chamadas ao serviço Web Servidor de Relatórios. Quase qualquer operação que pode ser escrita em código gerenciado também pode ser escrita em script.  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] dá suporte ao script [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] .NET como a linguagem de script que pode ser processada pelo utilitário RS.exe, um host de script que é executado no servidor de relatório.  
  
## <a name="reporting-services-sharepoint-mode-powershell-cmdlets-and-samples"></a>Exemplos e cmdlets do PowerShell do modo SharePoint do Reporting Services  
 ![Conteúdo relacionado ao PowerShell](../../analysis-services/instances/install-windows/media/rs-powershellicon.jpg "Conteúdo relacionado ao PowerShell")  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] O modo SharePoint inclui cmdlets [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para administração do servidor de relatório.  
  
-   [PowerShell cmdlets for Reporting Services SharePoint Mode](../../reporting-services/report-server-sharepoint/powershell-cmdlets-for-reporting-services-sharepoint-mode.md) Inclui os seguintes exemplos:  
  
    -   Criar um aplicativo de serviço e proxy  
  
    -   Revisar e atualizar uma extensão de entrega  
  
    -   Obter e definir propriedades do Banco de dados do aplicativo Reporting Services como, por exemplo, limite de banco de dados  
  
    -   Listar extensões de dados  
  
## <a name="reporting-services-object-model-and-powershell-samples"></a>Modelo de objeto do Reporting Services e exemplos do Powershell  
 ![Conteúdo relacionado ao PowerShell](../../analysis-services/instances/install-windows/media/rs-powershellicon.jpg "Conteúdo relacionado ao PowerShell")  
  
 O PowerShell chama o modelo de objeto principal e da maior parte válida do SharePoint e do modo nativo; por exemplo, o trabalho de migração, o trabalho de assinatura e mais exemplos relacionados para o trabalho de assinaturas no SQL15.  
  
-   [Usar o PowerShell para alterar e listar proprietários de assinatura do Reporting Services e executar uma assinatura](../../reporting-services/subscriptions/manage-subscription-owners-and-run-subscription-powershell.md).  
  
-   [Utilize o PowerShell para criar uma VM do Azure com um servidor de relatório no modo nativo](http://msdn.microsoft.com/library/azure/dn449661.aspx).  
  
-   Consulte a seção "Acessar as classes WMI usando o PowerShell" em [Access the Reporting Services WMI Provider](../../reporting-services/tools/access-the-reporting-services-wmi-provider.md).  
  

## <a name="rsexe-scripting-samples"></a>Exemplos de script RS.exe  
  
-   [Script rs.exe do Reporting Services de exemplo para copiar conteúdo entre Servidores de Relatório](../../reporting-services/tools/sample-reporting-services-rs-exe-script-to-copy-content-between-report-servers.md).  
  
-   Para obter exemplos adicionais de extensão, aplicativos e scripts, consulte [SQL Server Reporting Services Product Samples (Amostras do produto SQL Server Reporting Services)](http://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="see-also"></a>Consulte Também  
 [Utilitário RS.exe &#40;SSRS&#41;](../../reporting-services/tools/rs-exe-utility-ssrs.md)   
 [Implantação de script e tarefas administrativas](../../reporting-services/tools/script-deployment-and-administrative-tasks.md)   
 [Gerar scripts com o utilitário rs.exe e o serviço Web](../../reporting-services/tools/script-with-the-rs-exe-utility-and-the-web-service.md)  
  
  
