---
title: Criar uma entidade (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- entities [Master Data Services], creating
- creating entities [Master Data Services]
ms.assetid: d9a6a51e-7b53-4785-a118-3baeb7ca2d48
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 50cf10a9a745b3a111deb5db6be356d10d204d4a
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84971710"
---
# <a name="create-an-entity-master-data-services"></a>Criar uma entidade (Master Data Services)
  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], crie uma entidade para conter os membros e seus atributos.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional **Administração do sistema** .  
  
-   Você deve ser um administrador de modelo. Para obter mais informações, consulte [administradores &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
-   Deve existir um modelo. Para obter mais informações, consulte [Criar um modelo &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-model-master-data-services.md).  
  
### <a name="to-create-an-entity"></a>Para criar uma entidade  
  
1.  No [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], clique em **Administração do Sistema**.  
  
2.  Na página **Exibição de Modelos** , na barra de menus, aponte para **Gerenciar** e clique em **Entidades**.  
  
3.  Na página **Manutenção da Entidade** , na lista **Modelo** , selecione um modelo.  
  
4.  Clique em **Adicionar entidade**.  
  
5.  Na caixa **nome da entidade** , digite o nome da entidade.  
  
6.  Na caixa **nome para tabelas de preparo** , digite um nome para a tabela de preparo.  
  
    > [!TIP]  
    >  Use o nome do modelo como parte do nome da tabela de preparo, por exemplo, *Modelname_Entityname*. Isto facilita a localização das tabelas no banco de dados. Para obter mais informações sobre as tabelas de preparo, consulte [&#40;de importação de dados Master Data Services&#41;](overview-importing-data-from-tables-master-data-services.md).  
  
7.  Opcional. Marque a caixa de seleção **Criar valores de códigos automaticamente** . Para obter mais informações, consulte [criação automática de código &#40;Master Data Services&#41;](../../2014/master-data-services/automatic-code-creation-master-data-services.md).  
  
8.  Na lista **habilitar hierarquias explícitas e coleções** , selecione uma das seguintes opções:  
  
    -   **Não**. Selecione essa opção se não precisar habilitar a entidade para hierarquias explícitas e coleções. É possível alterar isso mais tarde se necessário.  
  
    -   **Sim**. Selecione essa opção quando desejar habilitar a entidade para hierarquias explícitas e coleções. Na caixa **nome da hierarquia explícita** , digite um nome. Opcionalmente, selecione **hierarquia obrigatória (todos os membros folha são incluídos** para tornar a hierarquia explícita uma hierarquia obrigatória.  
  
9. Clique em **Salvar entidade**.  
  
## <a name="next-steps"></a>Próximas etapas  
  
-   [Criar um atributo de texto &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-text-attribute-master-data-services.md)  
  
-   [Criar um atributo baseado em domínio &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-domain-based-attribute-master-data-services.md)  
  
-   [Criar um atributo de arquivo &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-file-attribute-master-data-services.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Entidades &#40;Master Data Services&#41;](../../2014/master-data-services/entities-master-data-services.md)   
 [Hierarquias explícitas &#40;Master Data Services&#41;](../../2014/master-data-services/explicit-hierarchies-master-data-services.md)   
 [Alterar um nome de entidade &#40;Master Data Services&#41;](edit-an-entity-master-data-services.md)   
 [Excluir uma entidade &#40;Master Data Services&#41;](../../2014/master-data-services/delete-an-entity-master-data-services.md)  
  
  
