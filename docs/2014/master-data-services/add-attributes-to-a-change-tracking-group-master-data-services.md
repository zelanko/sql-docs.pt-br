---
title: Adicionar atributos a um grupo de controle de alterações (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- change tracking groups [Master Data Services]
- attributes [Master Data Services], change tracking groups
- change tracking groups [Master Data Services], adding attributes
ms.assetid: e153eb5f-70ca-4c6f-89d8-1f937ed3917d
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 8e700942f9cebc08241cf4e159dceedc7d515a94
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "65480121"
---
# <a name="add-attributes-to-a-change-tracking-group-master-data-services"></a>Adicionar atributos a um grupo de controle de alterações (Master Data Services)
  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], adicione atributos ao grupo de controle de alterações quando desejar controlar as alterações feitas nos valores dos atributos.  
  
> [!NOTE]  
>  Depois de adicionar um atributo a um grupo de controle de alterações, quando os valores do atributo forem alterados, o atributo será sinalizado como alterado no banco de dados [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] . Crie uma regra de negócio para executar uma ação com base na alteração.  
  
## <a name="prerequisites"></a>Prerequisites  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional **Administração do sistema** .  
  
-   Você deve ser um administrador de modelo. Para obter mais informações, veja [Administradores &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
-   Os atributos devem existir para que possam ser adicionados ao grupo de controle de alterações. Para obter mais informações, veja [Criar um atributo de texto &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-text-attribute-master-data-services.md).  
  
### <a name="to-add-attributes-to-a-change-tracking-group"></a>Para adicionar atributos a um grupo de controle de alterações  
  
1.  No [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], clique em **Administração do Sistema**.  
  
2.  Na página **Gerenciador de modelos** , na barra de menus, aponte para **gerenciar** e clique em **entidades**.  
  
3.  Na página **Manutenção da Entidade** , na lista **Modelo** , selecione um modelo.  
  
4.  Selecione a linha correspondente à entidade para a qual você deseja controlar os valores de atributo.  
  
5.  Clique em **Editar entidade selecionada**.  
  
6.  Na página **Editar Entidade** :  
  
    -   Se o atributo for para membros folha, no painel **atributos de folha** , selecione o atributo e clique em **Editar atributo folha**.  
  
    -   Se o atributo for para membros consolidados, no painel **atributos consolidados** , selecione o atributo e clique em **Editar atributo consolidado**.  
  
    -   Se o atributo for para coleções, no painel **atributos da coleção** , selecione o atributo e clique em **Editar atributo de coleção**.  
  
7.  Marque a caixa de seleção **Habilitar controle de alterações** .  
  
8.  Na caixa **Grupo de controle de alterações** , digite um número para o grupo.  
  
9. Clique em **Salvar atributo**.  
  
10. Na página **Manutenção da Entidade** , clique em **Salvar entidade**.  
  
11. Repita esse procedimento para todos os atributos que você deseja incluir no grupo. Use o mesmo número de grupo de controle de alterações para cada atributo no grupo.  
  
## <a name="next-steps"></a>Próximas etapas  
  
-   [Iniciar ações com base nas alterações de valor de atributo &#40;Master Data Services&#41;](../../2014/master-data-services/initiate-actions-based-on-attribute-value-changes-master-data-services.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Criar um atributo de texto &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-text-attribute-master-data-services.md)   
 [Criar um atributo baseado em domínio &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-domain-based-attribute-master-data-services.md)  
  
  
