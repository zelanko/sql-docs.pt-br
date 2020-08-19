---
description: Confirmar ou Enviar um Conjunto de Alterações (Master Data Services)
title: Confirmar ou Enviar um Conjunto de Alterações
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: d323bbac-c8d4-4d2f-a7d2-a597e8b53e2d
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 47675ce7f7ac4704db9578564020c67fdc3b30b2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88430098"
---
# <a name="commit-or-submit-a-changeset-master-data-services"></a>Confirmar ou Enviar um Conjunto de Alterações (Master Data Services)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  Um conjunto de alterações é uma coleção das alterações pendentes nos dados mestre. Se as alterações da entidade não exigirem a aprovação do administrador, você poderá confirmar o conjunto de alterações. Se as alterações da entidade exigirem a aprovação do administrador, você poderá enviar o conjunto de alterações para a aprovação.  
  
## <a name="prerequisites"></a>Pré-requisitos  
  
-   Você deve ter permissão para acessar a área funcional do **Gerenciador** . Para obter mais informações, consulte [Permissões de área funcional &#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md)  
  
-   Se as alterações da entidade não exigirem a aprovação do administrador, você poderá confirmar o conjunto de alterações somente se for proprietário do conjunto de alterações e o status do conjunto de alterações for aberto.  
  
-   Se as alterações da entidade exigirem a aprovação do administrador, você poderá enviar o conjunto de alterações para a aprovação somente se possui-lo e se o status do conjunto estiver aberto ou for rejeitado.  
  
## <a name="to-commit-a-local-changeset"></a>Para confirmar um conjunto de alterações local  
 A opção de confirmação só estará disponível para conjuntos de alterações locais em entidades em que o Administrador de Entidade não tiver habilitado a necessidade de aprovação.  
  
1.  Na home page do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] , escolha o modelo e a versão e, em seguida, clique em **Explorer**.  
  
2.  Clique em uma entidade no menu **Entidades** .  
  
3.  No painel direito, selecione **Conjuntos de Alterações** e clique duas vezes no conjunto que você deseja confirmar.  
  
4.  Clique em **Confirmar**.  
  
## <a name="to-submit-a-changeset"></a>Para enviar um conjunto de alterações  
 A opção de envio só estará disponível em conjuntos de alterações em entidades em que o Administrador de Entidade tiver habilitado a necessidade de aprovação.  
  
1.  Na home page do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] , escolha o modelo e a versão e, em seguida, clique em **Explorer**.  
  
2.  Clique em uma entidade no menu **Entidades** .  
  
3.  No painel direito, selecione **Conjuntos de Alterações** e clique duas vezes no conjunto que você deseja enviar.  
  
4.  Clique em **Enviar**.  
  
## <a name="next-steps"></a>Próximas etapas  
 [Aprovar ou rejeitar um conjunto de alterações &#40;Master Data Services&#41;](../master-data-services/approve-or-reject-a-changeset-master-data-services.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Criar um conjunto de alterações &#40;Master Data Services&#41;](../master-data-services/create-a-changeset-master-data-services.md)   
 [Aplicar e atualizar um conjunto de alterações &#40;Master Data Services&#41;](../master-data-services/apply-and-update-a-changeset-master-data-services.md)   
 [Aprovar ou rejeitar um conjunto de alterações &#40;Master Data Services&#41;](../master-data-services/approve-or-reject-a-changeset-master-data-services.md)  
  
  
