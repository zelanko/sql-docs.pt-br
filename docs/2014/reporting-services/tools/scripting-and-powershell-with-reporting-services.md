---
title: Script e PowerShell com o Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- scripts [Reporting Services]
- Reporting Services, scripting
- scripting [Reporting Services]
ms.assetid: 1ac2646d-ed5a-4436-b18f-2150c33f3d87
caps.latest.revision: 12
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 2b69a9713d015db66945a1c096f8896998459406
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37212536"
---
# <a name="scripting-and-powershell-with-reporting-services"></a>Script e PowerShell com o Reporting Services
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] dá suporte a uma ampla variedade de cenários de desenvolvimento e gerenciamento por meio de script, incluindo o utilitário de linha de comando rs.exe, os cmdlets do PowerShell para servidores de relatório de modo do SharePoint e aproveitando o [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] modelo de objeto do PowerShell para nativa e Modo do SharePoint.  
  
-   Os administradores podem escrever o script em [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] para automatizar o modo como eles implantam e administram uma instalação de servidor de relatório. Os administradores também podem gerar e executar scripts [!INCLUDE[tsql](../../includes/tsql-md.md)] que criam, configuram e atualizam um banco de dados de servidor de relatório. Os administradores também podem usar o registro e os recursos de script de reprodução em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] para automatizar tarefas de manutenção de rotina.  
  
-   Os desenvolvedores podem criar aplicativos personalizados que incluem script. Você pode executar o script que faz chamadas ao serviço Web Servidor de Relatórios. Quase qualquer operação que pode ser escrita em código gerenciado também pode ser escrita em script.  
  
-   [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] dá suporte a [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] script .NET como a linguagem de script que pode ser processada pelo utilitário RS.exe, um host de script é executado no servidor de relatório.  
  
## <a name="reporting-services-sharepoint-mode-powershell-cmdlets-and-samples"></a>Exemplos e cmdlets do PowerShell do modo SharePoint do Reporting Services  
 ![Conteúdo relacionado ao PowerShell](../media/rs-powershellicon.jpg "Conteúdo relacionado ao PowerShell")  
  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] O modo SharePoint inclui [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] cmdlets para a administração de servidor de relatórios.  
  
-   [PowerShell cmdlets for Reporting Services SharePoint Mode](../powershell-cmdlets-for-reporting-services-sharepoint-mode.md) Inclui os seguintes exemplos:  
  
    -   Criar um aplicativo de serviço e proxy  
  
    -   Revisar e atualizar uma extensão de entrega  
  
    -   Obter e definir propriedades do Banco de dados do aplicativo Reporting Services como, por exemplo, limite de banco de dados  
  
    -   Listar extensões de dados  
  
## <a name="reporting-services-object-model-and-powershell-samples"></a>Modelo de objeto do Reporting Services e exemplos do Powershell  
 ![Conteúdo relacionado ao PowerShell](../media/rs-powershellicon.jpg "Conteúdo relacionado ao PowerShell")  
  
 O PowerShell chama o modelo de objeto principal e da maior parte válida do SharePoint e do modo nativo; por exemplo, o trabalho de migração, o trabalho de assinatura e mais exemplos relacionados para o trabalho de assinaturas no SQL15.  
  
-   [Use o PowerShell para alterar e listar proprietários de assinaturas do Reporting Services e executar uma assinatura](../subscriptions/manage-subscription-owners-and-run-subscription-powershell.md).  
  
-   [Utilize o PowerShell para criar uma VM do Azure com um servidor de relatório no modo nativo](http://msdn.microsoft.com/library/azure/dn449661.aspx).  
  
-   Consulte a seção "Acessar as classes WMI usando o PowerShell" em [Access the Reporting Services WMI Provider](access-the-reporting-services-wmi-provider.md).  
  
-   [Como administrar SSRS usando o PowerShell](http://curah.microsoft.com/13107/how-to-administer-ssrs-using-powershell).scriptin  
  
## <a name="rsexe-scripting-samples"></a>Exemplos de script RS.exe  
  
-   [Sample Reporting Services rs.exe Script to Migrate Content between Report Servers](sample-reporting-services-rs-exe-script-to-copy-content-between-report-servers.md).  
  
-   Para obter exemplos adicionais de extensão, aplicativos e scripts, consulte [SQL Server Reporting Services Product Samples (Amostras do produto SQL Server Reporting Services)](http://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="see-also"></a>Consulte também  
 [Utilitário RS.exe &#40;SSRS&#41;](rs-exe-utility-ssrs.md)   
 [Implantação de script e tarefas administrativas](script-deployment-and-administrative-tasks.md)   
 [Gerar scripts com o utilitário rs.exe e o serviço Web](script-with-the-rs-exe-utility-and-the-web-service.md)  
  
  
