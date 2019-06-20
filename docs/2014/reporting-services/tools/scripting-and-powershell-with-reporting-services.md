---
title: Script e PowerShell com o Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- scripts [Reporting Services]
- Reporting Services, scripting
- scripting [Reporting Services]
ms.assetid: 1ac2646d-ed5a-4436-b18f-2150c33f3d87
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 1cbb7d07835b63509ecd854788ce21e382141728
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66099636"
---
# <a name="scripting-and-powershell-with-reporting-services"></a>Script e PowerShell com o Reporting Services
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] dá suporte a uma ampla variedade de cenários de desenvolvimento e gerenciamento por meio de script, incluindo o utilitário de linha de comando rs.exe, os cmdlets do PowerShell para servidores de relatório no modo SharePoint e aproveitando o modelo de objeto [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] do PowerShell para os modos nativo e SharePoint.  
  
-   Os administradores podem escrever o script em [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] para automatizar o modo como eles implantam e administram uma instalação de servidor de relatório. Os administradores também podem gerar e executar scripts [!INCLUDE[tsql](../../includes/tsql-md.md)] que criam, configuram e atualizam um banco de dados de servidor de relatório. Os administradores também podem usar o registro e os recursos de script de reprodução em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] para automatizar tarefas de manutenção de rotina.  
  
-   Os desenvolvedores podem criar aplicativos personalizados que incluem script. Você pode executar o script que faz chamadas ao serviço Web Servidor de Relatórios. Quase qualquer operação que pode ser escrita em código gerenciado também pode ser escrita em script.  
  
-   [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] dá suporte ao script [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] .NET como a linguagem de script que pode ser processada pelo utilitário RS.exe, um host de script que é executado no servidor de relatório.  
  
## <a name="reporting-services-sharepoint-mode-powershell-cmdlets-and-samples"></a>Exemplos e cmdlets do PowerShell do modo SharePoint do Reporting Services  
 ![Conteúdo relacionado ao PowerShell](../media/rs-powershellicon.jpg "Conteúdo relacionado ao PowerShell")  
  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] O modo SharePoint inclui cmdlets [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] para administração do servidor de relatório.  
  
-   [PowerShell cmdlets for Reporting Services SharePoint Mode](../powershell-cmdlets-for-reporting-services-sharepoint-mode.md) Inclui os seguintes exemplos:  
  
    -   Criar um aplicativo de serviço e proxy  
  
    -   Revisar e atualizar uma extensão de entrega  
  
    -   Obter e definir propriedades do Banco de dados do aplicativo Reporting Services como, por exemplo, limite de banco de dados  
  
    -   Listar extensões de dados  
  
## <a name="reporting-services-object-model-and-powershell-samples"></a>Modelo de objeto do Reporting Services e exemplos do Powershell  
 ![Conteúdo relacionado ao PowerShell](../media/rs-powershellicon.jpg "Conteúdo relacionado ao PowerShell")  
  
 O PowerShell chama o modelo de objeto principal e da maior parte válida do SharePoint e do modo nativo; por exemplo, o trabalho de migração, o trabalho de assinatura e mais exemplos relacionados para o trabalho de assinaturas no SQL15.  
  
-   [Usar o PowerShell para alterar e listar proprietários de assinatura do Reporting Services e executar uma assinatura](../subscriptions/manage-subscription-owners-and-run-subscription-powershell.md).  
  
-   [Utilize o PowerShell para criar uma VM do Azure com um servidor de relatório no modo nativo](https://msdn.microsoft.com/library/azure/dn449661.aspx).  
  
-   Veja a seção "Acessar as classes WMI usando o PowerShell" em [Acessar o Provedor WMI do Reporting Services](access-the-reporting-services-wmi-provider.md).  
  
-   [Como administrar SSRS usando o PowerShell](https://www.sqlshack.com/how-to-administer-sql-server-reporting-services-ssrs-subscriptions-using-powershell/).scriptin  
  
## <a name="rsexe-scripting-samples"></a>Exemplos de script RS.exe  
  
-   [Exemplo do Reporting Services rs.exe Script para migrar conteúdo entre servidores de relatório](sample-reporting-services-rs-exe-script-to-copy-content-between-report-servers.md).  
  
-   Para obter exemplos adicionais de extensão, aplicativos e scripts, consulte [SQL Server Reporting Services Product Samples (Amostras do produto SQL Server Reporting Services)](https://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="see-also"></a>Consulte também  
 [Utilitário RS.exe &#40;SSRS&#41;](rs-exe-utility-ssrs.md)   
 [Implantação de script e tarefas administrativas](script-deployment-and-administrative-tasks.md)   
 [Gerar scripts com o utilitário rs.exe e o serviço Web](script-with-the-rs-exe-utility-and-the-web-service.md)  
  
  
