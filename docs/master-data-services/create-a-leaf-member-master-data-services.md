---
title: Criar um membro folha (Master Data Services) | Microsoft Docs
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: master-data-services
ms.reviewer: 
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- leaf members [Master Data Services], creating
- creating leaf members [Master Data Services]
- members [Master Data Services], creating leaf members
ms.assetid: 0499d3b3-d508-4d43-a740-19cf53ade9f1
caps.latest.revision: 14
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: fc46786e571f0a33de6226f83e96584a5765b0e9
ms.contentlocale: pt-br
ms.lasthandoff: 09/07/2017

---
# <a name="create-a-leaf-member-master-data-services"></a>Criar um membro folha (Master Data Services)
  Em [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], crie um membro folha quando quiser adicionar dados mestres ao sistema. Se você quiser adicionar dados em massa, use tabelas de preparo. Para obter mais informações, consulte [Importar dados de tabelas &#40;Master Data Services&#41;](../master-data-services/import-data-from-tables-master-data-services.md)  
  
 Você também pode usar o [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)] para importar os dados.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional do **Gerenciador** .  
  
-   Você deve ter um mínimo de permissão **Criar** ou **Atualizar** para o objeto de modelo folha para a entidade à qual está adicionando um membro. A permissão Criar permite que você crie um membro e edite apenas o atributo Code. A permissão Atualizar permite que você atualize outros atributos.  
  
     Para obter mais informações, consulte [Segurança &#40;Master Data Services&#41;](../master-data-services/security-master-data-services.md).  
  
### <a name="to-create-a-leaf-member"></a>Para criar um membro folha  
  
1.  Na página inicial do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] , na lista **Modelo** , selecione um modelo.  
  
2.  Se você for um usuário, selecione uma versão aberta da lista **Versão** . Se você for um administrador, selecione uma versão com status aberto ou bloqueado da lista **Versão** .  
  
3.  Clique em **Gerenciador**.  
  
4.  Na barra de menus, aponte para **Entidades** e clique no nome da entidade à qual você deseja adicionar um membro.  
  
5.  Clique em **Adicionar membro**.  
  
6.  No painel **Detalhes** , preencha os campos.  
  
     Se um atributo for baseado em domínio e um filtro tiver sido aplicado ao atributo, a lista de valores do atributo será limitada pelo atributo pai do filtro.  
  
     Para obter mais informações sobre atributos de filtro de pai e atributos baseados em domínio, consulte [Criar um atributo baseado em domínio &#40;Master Data Services&#41;](../master-data-services/create-a-domain-based-attribute-master-data-services.md)  
  
7.  Opcional. Na caixa **Anotações** , digite um comentário sobre por que o membro foi adicionado. Todos os usuários que têm acesso ao membro podem exibir a anotação.  
  
8.  Clique em **OK**.  
  
## <a name="see-also"></a>Consulte também  
 [Criar um membro consolidado &#40;Master Data Services&#41;](../master-data-services/create-a-consolidated-member-master-data-services.md)   
 [Membros &#40;Master Data Services&#41;](../master-data-services/members-master-data-services.md)  
  
  

