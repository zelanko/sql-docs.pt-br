---
title: Criar um atributo baseado em domínio (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- domain-based attributes [Master Data Services], creating
- creating domain-based attributes [Master Data Services]
- attributes [Master Data Services], creating domain-based attributes
ms.assetid: 11c31c9f-e6cc-47b7-b76a-d691f84c93c6
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: f0760ef2d2a29540b126235d6328af1fbfad39ce
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "65483425"
---
# <a name="create-a-domain-based-attribute-master-data-services"></a>Criar um atributo baseado em domínio (Master Data Services)
  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], crie um atributo baseado em domínio para popular os valores de um atributo com membros de uma entidade.  
  
## <a name="prerequisites"></a>Prerequisites  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional **Administração do sistema** .  
  
-   Você deve ser um administrador de modelo. Para obter mais informações, veja [Administradores &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
-   Uma entidade deve existir para ser usada como a origem dos valores de atributo. Por exemplo, para criar um atributo baseado em domínio com base na entidade Color, você deve primeiro criar a entidade Color. Para obter mais informações, consulte [criar uma entidade &#40;Master Data Services&#41;](../../2014/master-data-services/create-an-entity-master-data-services.md).  
  
-   Uma entidade deve existir para que se possa criar o atributo para ela. Para obter mais informações, consulte [criar uma entidade &#40;Master Data Services&#41;](../../2014/master-data-services/create-an-entity-master-data-services.md).  
  
### <a name="to-create-a-domain-based-attribute"></a>Para criar um atributo baseado em domínio  
  
1.  No [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], clique em **Administração do Sistema**.  
  
2.  Na página **Exibição de Modelos** , na barra de menus, aponte para **Gerenciar** e clique em **Entidades**.  
  
3.  Na página **Manutenção da Entidade** , na lista **Modelo** , selecione um modelo.  
  
4.  Selecione a linha correspondente à entidade para a qual você deseja criar um atributo.  
  
5.  Clique em **Editar entidade selecionada**.  
  
6.  Na página **Editar Entidade** :  
  
    -   Se o atributo for para membros folha, no painel **Atributos de membro folha** , clique em **Adicionar atributo folha**.  
  
    -   Se o atributo for para membros consolidados, no painel **Atributo de membro consolidado** , clique em **Adicionar atributo consolidado**.  
  
    -   Se o atributo for para coleções, no painel **Atributos da coleção** , clique em **Adicionar atributo de coleção**.  
  
7.  Na página **Adicionar atributo** , selecione a opção **baseado em domínio** .  
  
8.  Na caixa **Nome** , digite um nome para o atributo. Ele não precisa ser o mesmo nome da entidade que você usa para a origem dos valores de atributo.  
  
9. Na caixa **Exibir largura em pixels** , digite a largura da coluna de atributo a ser exibida na grade do **Gerenciador** .  
  
10. Na lista **entidade** , escolha a entidade a ser usada para popular os valores de atributo.  
  
11. Opcional. Selecione **Enable change tracking** para acompanhar as alterações feitas em grupos de atributos. Para obter mais informações, consulte [Adicionar atributos a um grupo de controle de alterações &#40;Master Data Services&#41;](../../2014/master-data-services/add-attributes-to-a-change-tracking-group-master-data-services.md).  
  
12. Clique em **Salvar atributo**.  
  
13. Na página **Manutenção da Entidade** , clique em **Salvar entidade**.  
  
## <a name="see-also"></a>Consulte Também  
 [Atributos baseados em domínio &#40;Master Data Services&#41;](../../2014/master-data-services/domain-based-attributes-master-data-services.md)   
 [Criar uma hierarquia derivada &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-derived-hierarchy-master-data-services.md)   
 [Alterar um nome de atributo &#40;Master Data Services&#41;](change-an-attribute-name-and-data-type-master-data-services.md)   
 [Excluir um atributo &#40;Master Data Services&#41;](../../2014/master-data-services/delete-an-attribute-master-data-services.md)  
  
  
