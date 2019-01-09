---
title: Adicionar atributos a um grupo de controle de alterações (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- change tracking groups [Master Data Services]
- attributes [Master Data Services], change tracking groups
- change tracking groups [Master Data Services], adding attributes
ms.assetid: e153eb5f-70ca-4c6f-89d8-1f937ed3917d
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: e434f416ca936fdf1cc0361a70cf89f92f4814ed
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52805388"
---
# <a name="add-attributes-to-a-change-tracking-group-master-data-services"></a>Adicionar atributos a um grupo de controle de alterações (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], adicione atributos ao grupo de controle de alterações quando desejar controlar as alterações feitas nos valores dos atributos.  
  
> [!NOTE]  
>  Depois de adicionar um atributo a um grupo de controle de alterações, quando os valores do atributo forem alterados, o atributo será sinalizado como alterado no banco de dados [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] . Crie uma regra de negócio para executar uma ação com base na alteração.  
  
## <a name="prerequisites"></a>Prerequisites  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional **Administração do Sistema** .  
  
-   Você deve ser um administrador de modelo. Para obter mais informações, veja [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
-   Os atributos devem existir para que possam ser adicionados ao grupo de controle de alterações. Para obter mais informações, veja [Criar um atributo de texto &#40;Master Data Services&#41;](../master-data-services/create-a-text-attribute-master-data-services.md).  
  
### <a name="to-add-attributes-to-a-change-tracking-group"></a>Para adicionar atributos a um grupo de controle de alterações  
  
1.  No [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], clique em **Administração do Sistema**.  
  
2.  Na página **Gerenciar Modelo** , selecione um modelo na grade e clique em **Entidades**.  
  
3.  Na página **Gerenciar Entidade** , selecione a linha da entidade para a qual deseja criar um atributo.  
  
4.  Clique em **Atributos**.  
  
5.  Na página **Gerenciar atributos** , realize um dos procedimentos a seguir.  
  
    -   Se o atributo for para membros folha, selecione **Folha** na caixa de listagem **Tipos de Membro** .  
  
    -   Se o atributo for para membros consolidados, selecione **Consolidado** na caixa de listagem **Tipos de Membro** .  
  
    -   Se o atributo for para coleções, selecione **Coleção** na caixa de listagem **Tipos de Membro** .  
  
6.  Selecione a linha do atributo que deseja editar e clique em **Editar**.  
  
7.  Marque a caixa de seleção **Habilitar controle de alterações** .  
  
8.  Na caixa **Grupo de controle de alterações** , digite um número para o grupo.  
  
9. Clique em **Salvar atributo**.  
  
     Para o atributo editado, a coluna **Habilitar Grupo de Controle de Alterações** da grade é alterada para **Sim (Grupo: número do grupo inserido)**.  
  
10. Repita esse procedimento para todos os atributos que você deseja incluir no grupo. Use o mesmo número de grupo de controle de alterações para cada atributo no grupo.  
  
## <a name="next-steps"></a>Next Steps  
  
-   [Iniciar ações com base em alterações no valor do atributo &#40;Master Data Services&#41;](../master-data-services/initiate-actions-based-on-attribute-value-changes-master-data-services.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Criar um atributo de texto &#40;Master Data Services&#41;](../master-data-services/create-a-text-attribute-master-data-services.md)   
 [Criar um atributo baseado em domínio &#40;Master Data Services&#41;](../master-data-services/create-a-domain-based-attribute-master-data-services.md)  
  
  
