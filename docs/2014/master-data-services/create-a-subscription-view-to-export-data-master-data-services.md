---
title: Criar uma exibição de assinatura (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- subscription views [Master Data Services], creating
- creating subscription views [Master Data Services]
ms.assetid: a5e28961-af16-414a-9845-d2e06aac5214
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: c4a2f747192b1cddefeac256d4470a2b345305de
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65479943"
---
# <a name="create-a-subscription-view-master-data-services"></a>Criar uma exibição de assinatura (Master Data Services)
  Criar uma exibição de assinatura quando você deseja criar uma exibição de seus dados no [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] banco de dados para uso por sistemas de assinatura.  
  
## <a name="prerequisites"></a>Prerequisites  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional **Gerenciamento de Integração** .  
  
-   Você deve ser um administrador de modelo. Para obter mais informações, veja [Administradores &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
### <a name="to-create-a-subscription-view"></a>Para criar uma exibição de assinatura  
  
1.  No [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], clique em **Gerenciamento de Integração**.  
  
2.  Da barra de menus, clique em **Criar Exibições**.  
  
3.  Sobre o **exibições de assinatura** , clique em **adicionar exibição de assinatura**.  
  
4.  No **criar exibição de assinatura** painel, no **nome de exibição de assinatura** , digite um nome para o modo de exibição.  
  
5.  Na lista **Modelo** , selecione um modelo.  
  
6.  Selecione o **versão** ou **sinalizador de versão** opção e, em seguida, selecione da lista correspondente.  
  
    > [!TIP]  
    >  Crie uma exibição de assinatura com base em um sinalizador de versão. Quando você bloqueia uma versão, pode reatribuir o sinalizador a uma versão aberta sem atualizar a exibição de assinatura.  
  
7.  Selecione o **Entity** ou **hierarquia derivada** opção e, em seguida, selecione da lista correspondente.  
  
8.  Selecione um formato de exibição de assinatura na lista **Formato** .  
  
9. Se você escolheu **Níveis Explícitos** ou **Níveis Derivados** da lista **Formato** , digite o número de níveis na hierarquia para incluir na exibição.  
  
10. Clique em **Salvar**.  
  
## <a name="see-also"></a>Consulte também  
 [Exportação de dados &#40;Master Data Services&#41;](overview-exporting-data-master-data-services.md)   
 [Excluir uma exibição de assinatura &#40;Master Data Services&#41;](delete-a-subscription-view-master-data-services.md)   
 [Criar um sinalizador de versão &#40;Master Data Services&#41;](create-a-version-flag-master-data-services.md)  
  
  
