---
title: Utilitários de prompt de comando do servidor de relatório (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- rsconfig utility
- components [Reporting Services], command line utilities
- rs utility
- command prompt utilities [Reporting Services]
- rskeymgmt utility
ms.assetid: 68f2f9f4-f894-40ff-a71c-f9756bf4b68c
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 108eea6b0633f0dc17c29ad9d8fb8e5603e1facd
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56020248"
---
# <a name="report-server-command-prompt-utilities-ssrs"></a>Utilitários de prompt de comando do servidor de relatório (SSRS)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] inclui vários utilitários de linha de comando que podem ser usados para administrar um servidor de relatório. Esses utilitários são instalados automaticamente ao instalar um servidor de relatórios.  
  
|Nome|Arquivo de comandos|Modo de implantação com suporte|Descrição|  
|----------|------------------|-------------------------------|-----------------|  
|Utilitário RSS|rs.exe|Modo nativo e modo do SharePoint. A versão [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] introduziu suporte ao modo do SharePoint.|O [utilitário rs](rs-exe-utility-ssrs.md) é um host de script que pode ser usado para executar operações de script. Use essa ferramenta para executar scripts do [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] que copiam dados entre os bancos de dados do servidor de relatório, publicam relatórios, criam itens em um banco de dados do servidor de relatório e outras funções. Para saber mais sobre como usar scripts para administrar um servidor, consulte [Implantação de script e tarefas administrativas](script-deployment-and-administrative-tasks.md).|  
|Cmdlets do PowerShell||Apenas SharePoint|Para obter uma lista dos cmdlets do PowerShell, consulte [PowerShell cmdlets for Reporting Services SharePoint Mode](../powershell-cmdlets-for-reporting-services-sharepoint-mode.md).|  
|utilitário rsconfig|rsconfig.exe|Apenas nativo|O [utilitário rsconfig](rsconfig-utility-ssrs.md) é usado para configurar e gerenciar uma conexão de servidor de relatório com o banco de dados do servidor de relatório. Você também pode usá-lo para especificar uma conta de usuário a ser usada para processamento de relatório autônomo. Para obter mais informações, consulte [Servidor de relatório do Reporting Services &#40;Modo Nativo&#41;](../report-server/reporting-services-report-server-native-mode.md). Para saber mais sobre a configuração de conexão, consulte [Configurar uma conexão de banco de dados do servidor de relatório &#40;Gerenciador de Configurações do SSRS&#41;](../../sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md).|  
|Utilitário rskeymgmt|rskeymgmt.exe|Apenas nativo|O [utilitário rskeymgmt](rskeymgmt-utility-ssrs.md) é uma ferramenta de gerenciamento de chaves de criptografia. Você pode usá-lo para fazer backup, aplicar, recriar e excluir chaves simétricas. Você também pode usar essa ferramenta para anexar uma instância do servidor de relatório a um banco de dados do servidor de relatório compartilhado. Rskeymgmt pode ser usado em operações de recuperação de banco de dados. É possível reutilizar um banco de dados existente em uma nova instalação aplicando uma cópia de backup da chave simétrica. Se as chaves não puderem ser recuperadas, essa ferramenta fornecerá uma maneira de excluir o conteúdo criptografado que não é mais usado. Para saber mais sobre o gerenciamento de chaves e o armazenamento de dados confidenciais, consulte [Armazenar dados criptografados do servidor de relatório &#40;Gerenciador de Configurações do SSRS&#41;](../install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md) e [Configurar e gerenciar chaves de criptografia &#40;Gerenciador de Configurações do SSRS&#41;](../install-windows/ssrs-encryption-keys-manage-encryption-keys.md).|  
  
> [!NOTE]  
>  Se você preferir usar uma ferramenta que tenha uma interface gráfica de usuário, poderá usar o Gerenciador de Configurações do Reporting Services em vez de `rsconfig` e `rskeymgmt`.  
  
## <a name="see-also"></a>Consulte também  
 [Reporting Services Configuration Manager &#40;Modo Nativo&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)   
 [Ferramentas do Reporting Services](reporting-services-tools.md)   
 [Servidor de Relatório do Reporting Services &#40;modo nativo&#41;](../report-server/reporting-services-report-server-native-mode.md)  
  
  
