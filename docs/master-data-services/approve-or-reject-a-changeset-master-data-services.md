---
title: "Aprovar ou rejeitar um conjunto de altera&#231;&#245;es (Master Data Services) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 45bd01f9-ae15-4fc5-a2ba-eee565a26ef8
caps.latest.revision: 8
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 8
---
# Aprovar ou rejeitar um conjunto de altera&#231;&#245;es (Master Data Services)
  Um conjunto de alterações é uma coleção de alterações pendentes nos dados mestre. Se as alterações de entidade exigirem aprovação do administrador e se um conjunto de alterações for enviado para aprovação, você poderá examinar e então aprovar ou rejeitar o conjunto de alterações.  
  
## Pré-requisitos  
  
-   Você deve ter permissão para acessar a área funcional do **Gerenciador** . Para obter mais informações, consulte [Permissões de área funcional &#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md).  
  
-   Você deve ter permissões de administrador para a entidade.  
  
-   As alterações de entidade devem exigir aprovação do administrador.  
  
-   Se o status do conjunto de alterações estiver pendente, você poderá examinar e aprovar ou rejeitar o conjunto de alterações.  
  
-   Os usuários não podem aprovar suas próprias alterações. Se você for o administrador da entidade, deverá atribuir um administrador secundário para aprovar seu próprio conjunto de alterações.  
  
## Para aprovar ou rejeitar um conjunto de alterações  
  
1.  Na home page do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] , selecione o modelo e a versão e depois clique em **Explorer**.  
  
2.  Clique em uma entidade no menu **Entidades** .  
  
3.  No painel direito, selecione **Conjuntos de Alterações** e clique duas vezes no conjunto de alterações que você deseja aprovar ou rejeitar.  
  
4.  Clique em **Aplicar** para aplicar o conjunto de alterações e examinar as alterações pendentes.  
  
5.  Clique em **Rejeitar** para rejeitar o conjunto de alterações e enviá-lo ao proprietário.  
  
6.  Clique em **Aprovar** para aprovar o conjunto de alterações. O conjunto de alterações é confirmado automaticamente.  
  
## Consulte também  
 [Criar um conjunto de alterações &#40;Master Data Services&#41;](../master-data-services/create-a-changeset-master-data-services.md)   
 [Aplicar e atualizar um conjunto de alterações &#40;Master Data Services&#41;](../master-data-services/apply-and-update-a-changeset-master-data-services.md)   
 [Confirmar ou enviar um conjunto de alterações &#40;Master Data Services&#41;](../master-data-services/commit-or-submit-a-changeset-master-data-services.md)  
  
  