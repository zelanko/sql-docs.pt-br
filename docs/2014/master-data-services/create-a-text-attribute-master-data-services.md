---
title: Criar um atributo de texto (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- attributes [Master Data Services], creating text attributes
- creating text attributes [Master Data Services]
ms.assetid: cd8b57de-364d-42a3-9273-c1c6b992bb40
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 5be296ceca85eb2032f2a409beefaed603c63f98
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "65483316"
---
# <a name="create-a-text-attribute-master-data-services"></a>Criar um atributo de texto (Master Data Services)
  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], crie um atributo de texto quando desejar que os usuários insiram uma cadeia de caracteres de texto como um valor de atributo.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional **Administração do sistema** .  
  
-   Você deve ser um administrador de modelo. Para obter mais informações, consulte [administradores &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
-   Uma entidade deve existir para que se possa criar o atributo para ela. Para obter mais informações, consulte [criar uma entidade &#40;Master Data Services&#41;](../../2014/master-data-services/create-an-entity-master-data-services.md).  
  
### <a name="to-create-a-text-attribute"></a>Para criar um atributo de texto  
  
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
  
8.  Na caixa **Nome** , digite um nome para o atributo. Para obter uma lista de palavras que não devem ser usadas como nomes de atributos, consulte [palavras reservadas &#40;Master Data Services&#41;](../../2014/master-data-services/reserved-words-master-data-services.md).  
  
9. Na caixa **Exibir largura em pixels** , digite a largura da coluna de atributo a ser exibida na grade do **Gerenciador** .  
  
10. Na lista **Tipo de dados** , selecione **Texto**.  
  
11. Na caixa **Tamanho** , digite o número máximo de caracteres permitidos.  
  
12. Opcionalmente, selecione **Habilitar controle de alterações** para controlar alterações de grupos de atributos. Para obter mais informações, consulte [Adicionar atributos a um grupo de controle de alterações &#40;Master Data Services&#41;](../../2014/master-data-services/add-attributes-to-a-change-tracking-group-master-data-services.md).  
  
13. Clique em **Salvar atributo**.  
  
14. Na página **Manutenção da Entidade** , clique em **Salvar entidade**.  
  
## <a name="see-also"></a>Consulte Também  
 [Atributos &#40;Master Data Services&#41;](../../2014/master-data-services/attributes-master-data-services.md)   
 [Alterar um nome de atributo &#40;Master Data Services&#41;](change-an-attribute-name-and-data-type-master-data-services.md)   
 [Criar um atributo baseado em domínio &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-domain-based-attribute-master-data-services.md)   
 [Criar um atributo de arquivo &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-file-attribute-master-data-services.md)  
  
  
