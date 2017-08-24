---
title: "Aplicar e atualizar um conjunto de alterações (Master Data Services) | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3a6a3cf2-1e77-43d3-a64a-855ae51258e7
caps.latest.revision: 10
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 8bd1f16bf28951aa128d1ab218ef12e8affbe1aa
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="apply-and-update-a-changeset-master-data-services"></a>Aplicar e atualizar um conjunto de alterações (Master Data Services)
  Um conjunto de alterações é uma coleção de alterações pendentes nos dados mestre. Você pode aplicar o conjunto de alterações localmente para exibir, adicionar, atualizar e excluir as alterações pendentes no conjunto de alterações.  
  
## <a name="prerequisites"></a>Pré-requisitos  
  
-   Você deve ter permissão para acessar a área funcional do **Gerenciador** . Para obter mais informações, consulte [Permissões de área funcional &#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md).  
  
-   Você deve ter pelo menos o acesso de atualização para a entidade ou um de seus atributos.  
  
-   Você pode exibir apenas o conjunto de alterações do qual é o proprietário ou o conjunto de alterações enviado para aprovação se você for o administrador da entidade.  
  
-   Você poderá modificar apenas o conjunto de alterações do qual é proprietário e quando o status do conjunto de alterações for aberto ou rejeitado.  
  
## <a name="to-apply-and-update-a-changeset"></a>Para aplicar e atualizar um conjunto de alterações  
  
1.  Na home page do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] , selecione um modelo e uma versão e clique em **Explorer**.  
  
2.  Clique em uma entidade no menu **Entidades** .  
  
3.  No painel direito, selecione **Conjuntos de Alterações** e clique duas vezes no conjunto que você deseja exibir e alterar.  
  
4.  Clique em **Aplicar**.  
  
     As alterações pendentes são aplicadas ao membro da entidade na grade. As alterações pendentes são realçadas.  
  
     A criação, a exclusão e a atualização de membros resultam em alterações no conjunto de alterações.  
  
5.  Para reverter as alterações pendentes, no painel **Conjuntos de Alterações** , clique com o botão direito do mouse na grade e clique em **Reverter**.  
  
## <a name="next-steps"></a>Próximas etapas  
 [Confirmar ou enviar um conjunto de alterações &#40;Master Data Services&#41;](../master-data-services/commit-or-submit-a-changeset-master-data-services.md)  
  
## <a name="see-also"></a>Consulte também  
 [Criar um conjunto de alterações &#40;Master Data Services&#41;](../master-data-services/create-a-changeset-master-data-services.md)   
 [Aprovar ou rejeitar um conjunto de alterações &#40;Master Data Services&#41;](../master-data-services/approve-or-reject-a-changeset-master-data-services.md)  
  
  
