---
title: Criar uma hierarquia derivada (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- derived hierarchies, creating
- creating derived hierarchies [Master Data Services]
ms.assetid: fec653c4-11cc-46a2-8dd8-b605341ebb40
caps.latest.revision: 5
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 696b4bc98f4feb47ae7db6cae99d1ba9ae8a6628
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37217636"
---
# <a name="create-a-derived-hierarchy-master-data-services"></a>Criar uma hierarquia derivada (Master Data Services)
  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], crie uma hierarquia derivada quando desejar uma hierarquia baseada em nível que assegure que os membros existam no nível correto. As hierarquias derivadas são baseadas em relações de atributos baseados em domínio que existem em um modelo.  
  
> [!NOTE]  
>  Se não existir um valor de atributo baseado em domínio para um membro, o membro não será incluído na hierarquia derivada. Consulte [Exigir valores de atributos &#40;Master Data Services&#41;](require-attribute-values-master-data-services.md) para exigir um valor de atributo baseado em domínio para todos os membros.  
  
## <a name="prerequisites"></a>Prerequisites  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional **Administração do Sistema** .  
  
-   Você deve ser um administrador de modelo. Para obter mais informações, veja [Administrators &#40;Master Data Services&#41;](../../2014/master-data-services/administrators-master-data-services.md).  
  
### <a name="to-create-a-derived-hierarchy"></a>Para criar uma hierarquia derivada  
  
1.  No [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], clique em **Administração do Sistema**.  
  
2.  Sobre o **exibição de modelo** página, na barra de menus, aponte para **gerenciar** e clique em **hierarquias derivadas**.  
  
3.  Na página **Manutenção da Hierarquia Derivada** , na lista **Modelo** , selecione um modelo.  
  
4.  Clique em **adicionar hierarquia derivada**.  
  
5.  Na página **Adicionar Hierarquia Derivada** , na caixa **Nome da hierarquia derivada** , digite um nome para a hierarquia.  
  
    > [!TIP]  
    >  Use um nome que descreva os níveis na hierarquia, por exemplo, **Produto para Subcategoria para Categoria**.  
  
6.  Clique em **Salvar hierarquia derivada**.  
  
7.  No **Editar hierarquia derivada** página, o **entidades e hierarquias disponíveis** painel, clique em uma entidade ou hierarquia e arraste-o para o **níveis atuais** painel.  
  
8.  Continue a arrastar entidades ou hierarquias até que sua hierarquia esteja completa.  
  
9. Clique em **Voltar**.  
  
## <a name="see-also"></a>Consulte também  
 [Hierarquias derivadas &#40;Master Data Services&#41;](../../2014/master-data-services/derived-hierarchies-master-data-services.md)   
 [Hierarquias derivadas com limites explícitos &#40;Master Data Services&#41;](../../2014/master-data-services/derived-hierarchies-with-explicit-caps-master-data-services.md)   
 [Atributos baseados em domínio &#40;Master Data Services&#41;](../../2014/master-data-services/domain-based-attributes-master-data-services.md)  
  
  
