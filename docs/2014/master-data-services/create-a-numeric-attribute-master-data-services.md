---
title: Criar um atributo numérico (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- master-data-services
ms.topic: conceptual
helpviewer_keywords:
- attributes [Master Data Services], creating number attributes
- creating number attributes [Master Data Services]
ms.assetid: c0dbb6d8-ba78-485a-a40d-6d5cb7e75d0a
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: a3aee9b1bbe939c3790d2849c829a706425aa1b4
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48072626"
---
# <a name="create-a-numeric-attribute-master-data-services"></a>Criar um atributo numérico (Master Data Services)
  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], crie um atributo numérico quando desejar que os usuários insiram um número como valor de atributo.  
  
> [!NOTE]  
>  Os atributos numéricos têm limitações. Para obter mais informações, consulte [Attributes &#40;Master Data Services&#41;](attributes-master-data-services.md).  
  
## <a name="prerequisites"></a>Prerequisites  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional **Administração do Sistema** .  
  
-   Você deve ser um administrador de modelo. Para obter mais informações, veja [Administrators &#40;Master Data Services&#41;](../../2014/master-data-services/administrators-master-data-services.md).  
  
-   Uma entidade deve existir para que se possa criar o atributo para ela. Para obter mais informações, consulte [Criar uma entidade &#40;Master Data Services&#41;](../../2014/master-data-services/create-an-entity-master-data-services.md).  
  
### <a name="to-create-a-numeric-attribute"></a>Para criar um atributo numérico  
  
1.  No [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], clique em **Administração do Sistema**.  
  
2.  Na página **Exibição de Modelos** , na barra de menus, aponte para **Gerenciar** e clique em **Entidades**.  
  
3.  Na página **Manutenção da Entidade** , na lista **Modelo** , selecione um modelo.  
  
4.  Selecione a linha correspondente à entidade para a qual você deseja criar um atributo.  
  
5.  Clique em **Editar entidade selecionada**.  
  
6.  Na página **Editar Entidade** :  
  
    -   Se o atributo for para membros folha, no painel **Atributos de membro folha** , clique em **Adicionar atributo folha**.  
  
    -   Se o atributo for para membros consolidados, no painel **Atributo de membro consolidado** , clique em **Adicionar atributo consolidado**.  
  
    -   Se o atributo for para coleções, no painel **Atributos da coleção** , clique em **Adicionar atributo de coleção**.  
  
7.  Na página **Adicionar Atributo** , selecione a opção **Forma livre** .  
  
8.  Na caixa **Nome** , digite um nome para o atributo. Para obter uma lista de palavras que não devem ser usadas como nomes de atributo, consulte [Palavras reservadas &#40;Master Data Services&#41;](../../2014/master-data-services/reserved-words-master-data-services.md).  
  
9. Na caixa **Exibir largura em pixels** , digite a largura da coluna de atributo a ser exibida na grade do **Gerenciador** .  
  
10. Na lista **Tipo de dados** , selecione **Número**.  
  
11. Na caixa **Decimais** , digite a quantidade de números que podem ser inseridos depois de um decimal.  
  
12. Dos **máscara de entrada** , selecione um formato para números negativos.  
  
13. Opcionalmente, selecione **Habilitar controle de alterações** para controlar alterações de grupos de atributos. Consulte [Add Attributes to a Change Tracking Group &#40;Master Data Services&#41;](../../2014/master-data-services/add-attributes-to-a-change-tracking-group-master-data-services.md) para obter mais informações.  
  
14. Clique em **Salvar atributo**.  
  
15. Na página **Manutenção da Entidade** , clique em **Salvar entidade**.  
  
## <a name="see-also"></a>Consulte também  
 [Atributos &#40;Master Data Services&#41;](attributes-master-data-services.md)   
 [Alterar um nome de atributo &#40;Master Data Services&#41;](change-an-attribute-name-and-data-type-master-data-services.md)   
 [Criar um atributo baseado em domínio &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-domain-based-attribute-master-data-services.md)   
 [Criar um atributo de arquivo &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-file-attribute-master-data-services.md)  
  
  
