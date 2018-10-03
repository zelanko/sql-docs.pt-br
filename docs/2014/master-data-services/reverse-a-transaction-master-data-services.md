---
title: Reservar uma transação (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- master-data-services
ms.topic: conceptual
helpviewer_keywords:
- transactions [Master Data Services], reversing
ms.assetid: 6f7c3f07-0f64-4283-8c9c-93facd00a046
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 572a0fbe10594226a755a4f7ecb59c2e52ef6c82
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48140654"
---
# <a name="reverse-a-transaction-master-data-services"></a>Inverter uma transação (Master Data Services)
  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], os administradores podem inverter uma transação quando uma ação precisar ser desfeita. Exemplos de transações são alterações de valor de atributo, movimentos de hierarquia ou exclusões de membro.  
  
## <a name="prerequisites"></a>Prerequisites  
  
-   Você deve ter permissão para acessar a área funcional **Gerenciamento de Versões** .  
  
-   Você deve ser um administrador de modelo. Para obter mais informações, veja [Administrators &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
### <a name="to-reverse-a-transaction"></a>Para inverter uma transação  
  
1.  Na home page do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] , clique em **Gerenciamento de Versões**.  
  
2.  Na barra de menus, clique em **Transações**.  
  
3.  Na página **Transações** , na lista **Modelo** , selecione um modelo.  
  
4.  Na lista **Versão** , selecione uma versão.  
  
5.  Clique na linha da grade da transação que você deseja inverter.  
  
6.  Clique em **Inverter Transação**.  
  
7.  Na caixa de diálogo de confirmação, clique em **OK**. Outra transação é adicionada à grade para registrar a transação invertida.  
  
## <a name="see-also"></a>Consulte também  
 [Transações &#40;Master Data Services&#41;](../../2014/master-data-services/transactions-master-data-services.md)   
 [Reativar um membro ou coleção &#40;Master Data Services&#41;](../../2014/master-data-services/reactivate-a-member-or-collection-master-data-services.md)  
  
  
