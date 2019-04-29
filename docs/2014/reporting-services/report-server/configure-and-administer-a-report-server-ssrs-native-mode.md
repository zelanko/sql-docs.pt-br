---
title: Configurar e administrar um servidor de relatório (modo nativo do SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Reporting Services, components
- deploying [Reporting Services], component options
- report servers [Reporting Services], component options
- configuration options [Reporting Services]
- administering Reporting Services
- components [Reporting Services], configuring
- configuring servers [Reporting Services]
ms.assetid: cfec012b-56f1-4346-9814-247acf22351c
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 8c49924100d5d052210f23bbf162d46b801cf11a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63010799"
---
# <a name="configure-and-administer-a-report-server-ssrs-native-mode"></a>Configurar e administrar um servidor de relatório (modo nativo do SSRS)
  Este tópico resume as abordagens que podem ser usadas para configurar o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Também inclui uma lista de tópicos que explicam como configurar componentes, recursos ou recursos específicos de servidor. Para configurar o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], você pode:  
  
-   Usar o Gerenciador de Configuração do Reporting Services. Muitos dos tópicos nesta seção contêm informações sobre como configurar recursos específicos com essa ferramenta.  
  
-   Usar o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] para personalizar propriedades de servidor, habilitar Meus Relatórios, habilitar logs de rastreamento e definir padrões em todo o site. Para obter mais informações sobre configurações de site, consulte [Servidor de relatório do Reporting Services &#40;Modo Nativo&#41;](reporting-services-report-server-native-mode.md) para o Management Studio. Observe que é possível criar e executar um script que defina propriedades de servidor programaticamente. Para obter mais informações, consulte [Implantação de script e tarefas administrativas](../tools/script-deployment-and-administrative-tasks.md) e [Propriedades de sistema do Servidor de Relatório](../report-server-web-service/net-framework/reporting-services-properties-report-server-system-properties.md).  
  
-   Use o Gerenciador de Relatórios para conceder permissões de acesso ao servidor de relatório. Permissões são concedidas por atribuições de função definidas para cada usuário ou conta de grupo. Para obter mais informações, consulte [Funções e permissões &#40;Reporting Services&#41;](../security/roles-and-permissions-reporting-services.md).  
  
-   Como alternativa, modifique arquivos de configuração para alterar configurações do aplicativo. Para obter mais informações sobre cada arquivo e diretrizes para modificá-los, consulte [Arquivos de configuração do Reporting Services](reporting-services-configuration-files.md).  
  
## <a name="in-this-section"></a>Nesta seção  
 [Configurar as URLs do servidor de relatório &#40;SSRS Configuration Manager&#41;](../install-windows/configure-report-server-urls-ssrs-configuration-manager.md)  
 Descreve como definir as URLs usadas para acessar o servidor de relatório e o Gerenciador de Relatórios.  
  
 [Configurar a conta de serviço do servidor de relatório &#40;SSRS Configuration Manager&#41;](../install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)  
 Fornece recomendações e etapas sobre como modificar a conta de serviço e a senha.  
  
 [Criar um banco de dados do servidor de relatório &#40;SSRS Configuration Manager&#41;](../../sql-server/install/create-a-report-server-database-ssrs-configuration-manager.md)  
 Descreve como criar um banco de dados de servidor de relatório, exigido por armazenar metadados e objetos de servidor.  
  
 [Configurar uma conexão de banco de dados do servidor de relatório &#40;SSRS Configuration Manager&#41;](../../sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)  
 Descreve como modificar a cadeia de conexão usada pelo servidor de relatório para conexão com o banco de dados do servidor de relatório.  
  
 [Configurar um servidor de relatório para entrega de email &#40;Configuration Manager do SSRS&#41;](../../sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md)  
 Descreve como configurar um servidor de relatório para dar suporte à distribuição de relatório por email.  
  
 [Configurar a conta de execução autônoma &#40;Gerenciador de configurações do SSRS&#41;](../install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)  
 Descreve como configurar uma conta do usuário para processar relatórios no modo autônomo.  
  
## <a name="see-also"></a>Consulte também  
 [Configurar o acesso ao Construtor de Relatórios](configure-report-builder-access.md)   
 [Arquivos de configuração do Reporting Services](reporting-services-configuration-files.md)   
 [Reporting Services Configuration Manager &#40;Modo Nativo&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)   
 [Segurança e proteção do Reporting Services](../security/reporting-services-security-and-protection.md)   
 [Servidor de Relatório do Reporting Services &#40;modo nativo&#41;](reporting-services-report-server-native-mode.md)  
  
  
