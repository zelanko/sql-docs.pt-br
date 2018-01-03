---
title: Conflitos de mesclagem (Master Data Services) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: non-specific
ms.reviewer: 
ms.suite: sql
ms.technology: master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 797219ad-5109-4666-94d3-dd1d59440a33
caps.latest.revision: "5"
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 61a4d43a179d344b89d9a71b67e0ae3ffa1b37b1
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="merge-conflicts-master-data-services"></a>Conflitos de mesclagem (Master Data Services)
  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], se os dados que você estiver tentando publicar tiverem sido alterados por outro usuário, a publicação falhará com um erro de conflito. Para resolver esse erro, você pode executar conflitos de mesclagem e republicar as alterações.  
  
## <a name="prerequisites"></a>Prerequisites  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional do **Gerenciador** .  
  
-   Você deve ter, no mínimo, a permissão Atualizar para o objeto de modelo folha para a entidade que você está atualizando.  
  
### <a name="to-merge-conflicts"></a>Para mesclar conflitos  
  
1.  Na página **Explorer** , atualize o atributo de membro.  
  
2.  Se o mesmo atributo de membro tiver sido alterado por outro usuário, o diálogo **Mesclar Conflitos** será exibido.  
  
3.  No diálogo **Mesclar Conflitos** , você pode:  
  
    -   Escolha **Mais recente** e clique em **Aplicar** para desfazer as alterações pendentes e recarregar a versão mais recente a partir do servidor.  
  
    -   Escolher **Original** e clicar em **Aplicar** para aplicar a versão original à planilha.  
  
    -   Escolher **Sua** e clicar em **Aplicar** para manter as alterações locais existentes.  
  
4.  Depois de clicar em **Aplicar**, você poderá fazer alterações adicionais e publicar novamente. Ou você pode clicar em **Cancelar** para cancelar a atualização e a recarga da versão mais recente do servidor.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros &#40;Master Data Services&#41;](../master-data-services/members-master-data-services.md)  
  
  
