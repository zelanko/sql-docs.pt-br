---
title: Criar um Conjunto de Alterações
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: cfad6f1c-9125-4896-b5f5-a4b9f9593cc4
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 859eb2c829b7d6f35aa39cb2301a4a380c0d039e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "73729630"
---
# <a name="create-a-changeset-master-data-services"></a>Criar um Conjunto de Alterações (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Um conjunto de alterações é uma coleção das alterações pendentes nos dados mestre. Se a entidade requer aprovação para alterações, as alterações pendentes devem ser salvas em um conjunto de alterações e, em seguida, enviadas para aprovação do administrador.  
  
## <a name="prerequisites"></a>Prerequisites  
  
-   Você deve ter permissão para acessar a área funcional do Gerenciador. Para obter mais informações, consulte [permissões de área funcional &#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md)  
  
-   Você deve ter pelo menos o acesso de leitura para a entidade ou um de seus atributos.  
  
## <a name="to-create-a-local-changeset"></a>Para criar um conjunto de alterações local  
  
1.  Na [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Home Page, selecione o modelo e a versão e clique em **Gerenciador**.  
  
2.  Clique em uma entidade no menu **Entidades** .  
  
3.  No painel direito, escolha **Conjuntos de Alterações** e clique em **Criar**.  
  
4.  Insira um nome para o conjunto de alterações e clique em **Salvar**.  
  
     O nome do conjunto de alterações deve ser exclusivo dentro de um modelo.  
  
## <a name="to-create-a-changeset-for-approval"></a>Para criar um conjunto de alterações para aprovação  
  
1.  Na [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Home Page, selecione o modelo e a versão e clique em **Gerenciador**.  
  
2.  Clique em uma entidade no menu **Entidades** .  
  
3.  Faça alterações na entidade e clique em**OK**.  
  
4.  **A caixa de diálogo escolher um conjunto de alterações** é exibida.  
  
5.  Clique em **Novo**, insira um nome para o conjunto de alterações e clique em **Salvar**. O nome do conjunto de alterações deve ser exclusivo dentro de um modelo.  
  
6.  Para usar um conjunto de alterações existente, clique em **Existente** e escolha o conjunto de alterações na lista. Somente conjuntos de alterações que estão em um estado aberto ou rejeitado estão disponíveis.  
  
## <a name="next-steps"></a>Próximas etapas  
 [Aplicar e atualizar um conjunto de alterações &#40;Master Data Services&#41;](../master-data-services/apply-and-update-a-changeset-master-data-services.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Confirmar ou enviar um conjunto de alterações &#40;Master Data Services&#41;](../master-data-services/commit-or-submit-a-changeset-master-data-services.md)   
 [Aprovar ou rejeitar um conjunto de alterações &#40;Master Data Services&#41;](../master-data-services/approve-or-reject-a-changeset-master-data-services.md)  
  
  
