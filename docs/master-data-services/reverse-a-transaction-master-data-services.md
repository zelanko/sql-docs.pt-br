---
title: Inverter uma transação
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- transactions [Master Data Services], reversing
ms.assetid: 6f7c3f07-0f64-4283-8c9c-93facd00a046
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 870341b6ae6a3ffbda345aa7a0abc4a2fe253ac5
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "73728933"
---
# <a name="reverse-a-transaction-master-data-services"></a>Inverter uma transação (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], os administradores podem inverter uma transação quando uma ação precisar ser desfeita. Exemplos de transações são alterações de valor de atributo, movimentos de hierarquia ou exclusões de membro. Este tópico se aplica somente a transações de entidades com o tipo de log de transações “Atributo”. Vá para a página do gerenciador de entidade para exibir o histórico de transações das entidades com o tipo de log de transações “Membro”.  
  
## <a name="prerequisites"></a>Pré-requisitos  
  
-   Você deve ter permissão para acessar a área funcional **Gerenciamento de Versões** .  
  
-   Você deve ser um administrador de modelo. Para obter mais informações, consulte [administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
### <a name="to-reverse-a-transaction"></a>Para inverter uma transação  
  
1.  Na home page do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] , clique em **Gerenciamento de Versões**.  
  
2.  Na barra de menus, clique em **Transações**.  
  
3.  Na página **Transações** , na lista **Modelo** , selecione um modelo.  
  
4.  Na lista **Versão** , selecione uma versão.  
  
5.  Clique na linha da grade da transação que você deseja inverter.  
  
6.  Clique em **Inverter Transação**.  
  
7.  Na caixa de diálogo de confirmação, clique em **OK**. Outra transação é adicionada à grade para registrar a transação invertida.  
  
## <a name="see-also"></a>Consulte Também  
 [Transações &#40;Master Data Services&#41;](../master-data-services/transactions-master-data-services.md)   
 [Reativar um membro ou uma coleção &#40;Master Data Services&#41;](../master-data-services/reactivate-a-member-or-collection-master-data-services.md)  
 [Reverter Histórico de Revisões do Membro](../master-data-services/rollback-member-revision-history-master-data-services.md)
  
  
