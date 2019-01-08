---
title: Notificações (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- notifications [Master Data Services]
- notifications [Master Data Services], about notifications
- e-mail [Master Data Services]
- e-mail [Master Data Services], about e-mail notifications
ms.assetid: d7ad32d5-9fe5-48fd-8c61-0b00c0aff082
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: ac5fbbd7a2ea3988fab52aaf921a74ba36519c0c
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53356908"
---
# <a name="notifications-master-data-services"></a>Notificações (Master Data Services)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] pode ser configurado para enviar uma notificação por email quando ocorre falha na validação de regra de negócio ou o status de uma versão de modelo mudar.  
  
## <a name="how-notifications-are-sent"></a>Como as notificações são enviadas  
 As notificações são configuradas no [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]. As notificações enviam mensagens de email por meio do Database Mail na instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../includes/ssde-md.md)] que hospeda o banco de dados do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] . Para obter mais informações sobre o Database Mail, consulte [Objetos de configuração do Database Mail](../relational-databases/database-mail/database-mail-configuration-objects.md) nos Manuais Online do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
## <a name="when-notifications-are-sent"></a>Quando as notificações são enviadas  
 Depois que as notificações são configuradas, notificações por email automatizadas podem ser enviadas nas instâncias a seguir.  
  
|Instância|Descrição|  
|--------------|-----------------|  
|Os dados falham na validação de regras de negócio.|Regras de negócio individuais devem ser configuradas para enviar email quando um valor de atributo é reprovado na validação da regra de negócio. Para obter mais informações, consulte [Configurar regras de negócio para enviar notificações &#40;Master Data Services&#41;](configure-business-rules-to-send-notifications-master-data-services.md).|  
|O status da versão do modelo é alterado|Cada vez que o status de uma versão de modelo muda, os usuários que são administradores de modelo recebem notificações automaticamente. Para obter mais informações, veja [Administradores &#40;Master Data Services&#41;](../../2014/master-data-services/administrators-master-data-services.md).|  
  
## <a name="system-settings"></a>Configurações do sistema  
 Existem configurações no [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] que afetam as notificações. Essas configurações podem ser ajustadas no [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] ou diretamente na tabela de Configurações do Sistema do banco de dados do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] . Para obter mais informações, veja [Configurações do sistema &#40;Master Data Services&#41;](../../2014/master-data-services/system-settings-master-data-services.md).  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Descrição da tarefa|Tópico|  
|----------------------|-----------|  
|Configurar o [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] para enviar notificações por email.|[Configurar notificações por email &#40;Master Data Services&#41;](../../2014/master-data-services/configure-email-notifications-master-data-services.md)|  
|Configurar o [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] para enviar notificações quando os valores dos atributos são alterados.|[Configurar regras de negócio para enviar notificações &#40;Master Data Services&#41;](configure-business-rules-to-send-notifications-master-data-services.md)|  
  
## <a name="related-content"></a>Conteúdo relacionado  
  
-   [Regras de negócio &#40;Master Data Services&#41;](../../2014/master-data-services/business-rules-master-data-services.md)  
  
-   [Versões &#40;Master Data Services&#41;](../../2014/master-data-services/versions-master-data-services.md)  
  
-   [Solucionando problemas de notificações por email (Master Data Services)](https://social.technet.microsoft.com/wiki/contents/articles/troubleshooting-email-notifications-master-data-services.aspx)  
  
  
