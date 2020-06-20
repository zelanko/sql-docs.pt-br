---
title: Criar uma hierarquia derivada (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- derived hierarchies, creating
- creating derived hierarchies [Master Data Services]
ms.assetid: fec653c4-11cc-46a2-8dd8-b605341ebb40
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 7c831ab360f2cbe4b32834ae2a280b961d2bac1e
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84971866"
---
# <a name="create-a-derived-hierarchy-master-data-services"></a>Criar uma hierarquia derivada (Master Data Services)
  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], crie uma hierarquia derivada quando desejar uma hierarquia baseada em nível que assegure que os membros existam no nível correto. As hierarquias derivadas são baseadas em relações de atributos baseados em domínio que existem em um modelo.  
  
> [!NOTE]  
>  Se não existir um valor de atributo baseado em domínio para um membro, o membro não será incluído na hierarquia derivada. Consulte [Exigir valores de atributos &#40;Master Data Services&#41;](require-attribute-values-master-data-services.md) para exigir um valor de atributo baseado em domínio para todos os membros.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional **Administração do sistema** .  
  
-   Você deve ser um administrador de modelo. Para obter mais informações, consulte [administradores &#40;Master Data Services&#41;](../../2014/master-data-services/administrators-master-data-services.md).  
  
### <a name="to-create-a-derived-hierarchy"></a>Para criar uma hierarquia derivada  
  
1.  No [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], clique em **Administração do Sistema**.  
  
2.  Na página **exibição de modelo** , na barra de menus, aponte para **gerenciar** e clique em **hierarquias derivadas**.  
  
3.  Na página **Manutenção da Hierarquia Derivada** , na lista **Modelo** , selecione um modelo.  
  
4.  Clique em **Adicionar hierarquia derivada**.  
  
5.  Na página **Adicionar Hierarquia Derivada** , na caixa **Nome da hierarquia derivada** , digite um nome para a hierarquia.  
  
    > [!TIP]  
    >  Use um nome que descreva os níveis na hierarquia, por exemplo, **Produto para Subcategoria para Categoria**.  
  
6.  Clique em **Salvar hierarquia derivada**.  
  
7.  Na página **Editar hierarquia derivada** , no painel **entidades e hierarquias disponíveis** , clique em uma entidade ou hierarquia e arraste-a para o painel **níveis atuais** .  
  
8.  Continue a arrastar entidades ou hierarquias até que sua hierarquia esteja completa.  
  
9. Clique em **Voltar**.  
  
## <a name="see-also"></a>Consulte Também  
 [Hierarquias derivadas &#40;Master Data Services&#41;](../../2014/master-data-services/derived-hierarchies-master-data-services.md)   
 [Hierarquias derivadas com limites explícitos &#40;Master Data Services&#41;](../../2014/master-data-services/derived-hierarchies-with-explicit-caps-master-data-services.md)   
 [Atributos baseados em domínio &#40;Master Data Services&#41;](../../2014/master-data-services/domain-based-attributes-master-data-services.md)  
  
  
