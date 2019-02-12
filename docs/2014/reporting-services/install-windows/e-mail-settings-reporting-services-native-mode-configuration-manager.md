---
title: Configurações de email – Configuration Manager (modo nativo do SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
f1_keywords:
- sql12.rsconfigtool.emailsettings.f1
helpviewer_keywords:
- SQL11.rsconfigtool.emailsettings.F1
ms.assetid: cdad1529-bfa6-41fb-9863-d9ff1b802577
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 1340e42824aabd3e4d32cc844f3061be90f97e52
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56031978"
---
# <a name="e-mail-settings---configuration-manager-ssrs-native-mode"></a>Configurações de Email - Gerenciador de Configurações (modo nativo do SSRS).
  Use esta página para especificar configurações do protocolo SMTP que habilitem a entrega de email do servidor de relatório a partir do servidor de relatório. Você pode usar a extensão de entrega de email do Servidor de Relatório para distribuir relatórios ou notificações de processamento de relatório por meio de assinaturas de email. A extensão de entrega de email do Servidor de relatório requer um servidor SMTP e um endereço de email a ser usado no campo De:.  
  
 Podem ser usados parâmetros de configuração adicionais para personalizar ainda mais as assinaturas de email, incluindo configurações que restrinjam a disponibilidade da extensão de renderização e dos hosts do servidor de email. Você não pode especificar essas configurações no Gerenciador de Configurações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Para configurar os parâmetros adicionais, você deve editar manualmente o arquivo RSReportServer.config. Para obter mais informações, consulte [configurar um servidor de relatório para entrega de email &#40;Configuration Manager do SSRS&#41; ](../../sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md) e [arquivos de configuração do Reporting Services](../report-server/reporting-services-configuration-files.md) na [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] manuais On-line.  
  
 Para abrir essa página, inicie o Gerenciador de configuração do Reporting Services e clique em **configurações de email** no painel de navegação. Para obter mais informações, consulte [Reporting Services Configuration Manager &#40;Modo Nativo&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md).  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
## <a name="options"></a>Opções  
 **Endereço do remetente**  
 Especifica o endereço de email a ser usado no campo De: de um email gerado. Você deve especificar uma conta de usuário que tenha permissão para enviar email do servidor SMTP.  
  
 **Método de entrega SMTP atual**  
 Especifica que o email do servidor de relatório é roteado por um servidor SMTP. Esse é o único método de entrega que você pode especificar no Gerenciador de Configurações do Reporting Services.  
  
 Um método de entrega alternativo é usar um diretório local de retirada de serviço SMTP. Você poderá usar esse método de entrega se um serviço de rede SMTP não estiver disponível. Para especificar um diretório local de retirada de serviço SMTP, você deve editar o arquivo RSReportServer.config. Se você edita o arquivo de configuração para usar um diretório local de retirada de serviço SMTP, o Gerenciador de Configurações do Reporting Services define a opção **Método de entrega** como *personalizado* para indicar que o método de entrega está especificado no arquivo de configuração.  
  
 No arquivo de configuração, o método de entrega é definido pelo parâmetro de configuração `SendUsing`. Para obter mais informações sobre como especificar o `SendUsing` , consulte [configurar um servidor de relatório para entrega de email &#40;Configuration Manager do SSRS&#41;](../../sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md).  
  
 **Servidor SMTP**  
 Especifique o servidor SMTP ou o gateway a ser usado. Você pode usar um servidor local ou um servidor SMTP em sua rede.  
  
## <a name="see-also"></a>Consulte também  
 [Configurar um servidor de relatório para entrega de email &#40;Configuration Manager do SSRS&#41;](../../sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md)   
 [Tópicos de Ajuda F1 do Configuration Manager do Reporting Services &#40;modo nativo do SSRS&#41;](../../sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)  
  
  
