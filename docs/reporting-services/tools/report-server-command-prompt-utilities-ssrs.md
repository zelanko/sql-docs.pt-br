---
title: "Relatório de utilitários de Prompt de comando do servidor (SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- rsconfig utility
- components [Reporting Services], command line utilities
- rs utility
- command prompt utilities [Reporting Services]
- rskeymgmt utility
ms.assetid: 68f2f9f4-f894-40ff-a71c-f9756bf4b68c
caps.latest.revision: 48
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: eb04937fc5c68bf2efb82ece9914c56409b7f325
ms.contentlocale: pt-br
ms.lasthandoff: 08/09/2017

---
# <a name="report-server-command-prompt-utilities-ssrs"></a>Utilitários de prompt de comando do servidor de relatório (SSRS)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] inclui vários utilitários de linha de comando que você pode usar para administrar um servidor de relatório. Esses utilitários são instalados automaticamente ao instalar um servidor de relatórios.  
  
|Nome|Arquivo de comandos|Modo de implantação com suporte|Description|  
|----------|------------------|-------------------------------|-----------------|  
|Utilitário RSS|rs.exe|Modo nativo e modo do SharePoint. A versão [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] introduziu suporte ao modo do SharePoint.|O [utilitário rs](../../reporting-services/tools/rs-exe-utility-ssrs.md) é um host de script que pode ser usado para executar operações de script. Use essa ferramenta para executar [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] scripts que copiam dados entre bancos de dados de servidor de relatório, publicar relatórios, criam itens em um servidor de relatório, banco de dados e muito mais. Para saber mais sobre como usar scripts para administrar um servidor, consulte [Implantação de script e tarefas administrativas](../../reporting-services/tools/script-deployment-and-administrative-tasks.md).|  
|Cmdlets do PowerShell||Apenas SharePoint|Para obter uma lista dos cmdlets do PowerShell, consulte [PowerShell cmdlets for Reporting Services SharePoint Mode](../../reporting-services/report-server-sharepoint/powershell-cmdlets-for-reporting-services-sharepoint-mode.md).|  
|utilitário rsconfig|rsconfig.exe|Apenas nativo|O [utilitário rsconfig](../../reporting-services/tools/rsconfig-utility-ssrs.md) é usado para configurar e gerenciar uma conexão de servidor de relatório com o banco de dados do servidor de relatório. Você também pode usá-lo para especificar uma conta de usuário a ser usada para processamento de relatório autônomo. Para obter mais informações, consulte [Servidor de relatório do Reporting Services &#40;Modo Nativo&#41;](../../reporting-services/report-server/reporting-services-report-server-native-mode.md). Para saber mais sobre a configuração de conexão, consulte [Configurar uma conexão de banco de dados do servidor de relatório &#40;Gerenciador de configurações do SSRS&#41;](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md).|  
|Utilitário rskeymgmt|rskeymgmt.exe|Apenas nativo|O [utilitário rskeymgmt](../../reporting-services/tools/rskeymgmt-utility-ssrs.md) é uma ferramenta de gerenciamento de chaves de criptografia. Você pode usá-lo para fazer backup, aplicar, recriar e excluir chaves simétricas. Você também pode usar essa ferramenta para anexar uma instância do servidor de relatório a um banco de dados do servidor de relatório compartilhado. Rskeymgmt pode ser usado em operações de recuperação de banco de dados. É possível reutilizar um banco de dados existente em uma nova instalação aplicando uma cópia de backup da chave simétrica. Se as chaves não puderem ser recuperadas, essa ferramenta fornecerá uma maneira de excluir o conteúdo criptografado que não é mais usado. Para saber mais sobre gerenciamento de chaves e armazenamento de dados confidenciais, consulte [Armazenar dados do servidor de relatório criptografado do armazenamento &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md) e [Configurar e gerenciar chaves de criptografia &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md).|  
  
> [!NOTE]  
>  Se você preferir usar uma ferramenta que tenha uma interface gráfica do usuário, poderá usar o Gerenciador de Configurações do Reporting Services, em vez de **rsconfig** e **rskeymgmt**.  
  
## <a name="see-also"></a>Consulte também  
 [Reporting Services Configuration Manager &#40; Modo nativo &#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)   
 [Ferramentas do Reporting Services](../../reporting-services/tools/reporting-services-tools.md)   
 [Reporting Services Report Server &#40; Modo nativo &#41;](../../reporting-services/report-server/reporting-services-report-server-native-mode.md)  
  
  
