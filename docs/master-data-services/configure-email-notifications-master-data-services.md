---
title: "Configurar notificações por email (Master Data Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: non-specific
ms.reviewer: 
ms.suite: sql
ms.technology: master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- e-mail [Master Data Services], configuring
- notifications [Master Data Services], configuring notifications
ms.assetid: 4241a6ab-7465-471b-9890-57c6b572037e
caps.latest.revision: "7"
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3ea4778f3e1ae329055ff9b3a378cab5d1fb803c
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="configure-email-notifications-master-data-services"></a>Configurar notificações por email (Master Data Services)
  Configure emails de notificação quando desejar que o [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] envie mensagens de email automaticamente.  
  
### <a name="to-configure-notifications"></a>Para configurar notificações  
  
1.  No [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)], na página **Banco de Dados** , selecione seu banco de dados do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .  
  
2.  Na seção **Configurações do Sistema** , clique em **Criar Perfil**.  
  
3.  Preencha todos os campos obrigatórios. Para obter mais informações, consulte [Caixa de diálogo Criar Perfil e Conta do Database Mail &#40;Gerenciador de Configuração do Master Data Services&#41;](../master-data-services/create-database-mail-profile-and-account-dialog-box.md).  
  
4.  Clique em **OK**.  
  
    > [!NOTE]  
    >  Depois de configurar notificações, você não poderá usar o [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] para fazer alterações. Você deve fazer alterações diretamente no banco de dados do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] . Para obter mais informações, consulte [Database Mail Configuration Objects](../relational-databases/database-mail/database-mail-configuration-objects.md).  
  
## <a name="next-steps"></a>Next Steps  
  
-   Existem configurações no [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] que afetam as notificações. Essas configurações podem ser ajustadas no [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] ou diretamente na tabela de Configurações do Sistema do banco de dados do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] . Para obter mais informações, veja [Configurações do sistema &#40;Master Data Services&#41;](../master-data-services/system-settings-master-data-services.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Notificações &#40;Master Data Services&#41;](../master-data-services/notifications-master-data-services.md)   
 [Solução de problemas de notificações por email (Master Data Services)](http://social.technet.microsoft.com/wiki/contents/articles/troubleshooting-email-notifications-master-data-services.aspx)   
 [Configurar regras de negócio para enviar notificações &#40;Master Data Services&#41;](../master-data-services/configure-business-rules-to-send-notifications-master-data-services.md)  
  
  
