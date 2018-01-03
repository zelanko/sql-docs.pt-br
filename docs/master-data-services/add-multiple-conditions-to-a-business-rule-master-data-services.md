---
title: "Adicionar várias condições a uma regra de negócios (Master Data Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: non-specific
ms.reviewer: 
ms.suite: sql
ms.technology: master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: business rules [Master Data Services], multiple conditions
ms.assetid: 5f0f6958-6cf2-444b-bdcd-05b887637a0b
caps.latest.revision: "9"
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0ab40c3eda3f93bcee19f9d1de4faa0b6f0b6ecb
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="add-multiple-conditions-to-a-business-rule-master-data-services"></a>Adicionar várias condições a uma regra de negócio (Master Data Services)
  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], adicione várias condições **AND** ou **OR** a uma regra de negócio quando desejar uma regra mais complexa.  
  
> [!NOTE]  
>  Se você criar uma regra de negócio que usa o operador **OR** , considere a criação de uma regra separada para cada instrução condicional que possa ser avaliada independentemente. É possível excluir regras conforme necessário, para garantir mais flexibilidade e uma solução de problemas mais fácil.  
  
## <a name="prerequisites"></a>Prerequisites  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional **Administração do Sistema** .  
  
-   Você deve ser um administrador de modelo. Para obter mais informações, veja [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
-   Uma regra de negócios deve existir. Para obter mais informações, consulte [Criar e publicar uma regra de negócio &#40;Master Data Services&#41;](../master-data-services/create-and-publish-a-business-rule-master-data-services.md).  
  
### <a name="to-add-multiple-conditions-to-a-business-rule"></a>Para acrescentar várias condições a uma regra de negócio  
  
1.  No [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], clique em **Administração do Sistema**.  
  
2.  Na barra de menus, aponte para **Gerenciar** e clique em **Regras de Negócios**.  
  
3.  Na página **Regras de Negócio/** , na lista suspensa **Modelo** , selecione um modelo.  
  
4.  Na lista suspensa **Entidade** , escolha uma entidade.  
  
5.  Na lista suspensa **Tipos de Membro** , escolha um tipo de membro.  
  
6.  Clique na linha da regra de negócio que deseja editar.  
  
7.  Clique em **Editar**.  
  
8.  No bloco **If** , no lado esquerdo da lista suspensa do operador lógico, selecione **AND/OR/ NOT**.  
  
9. Clique em **Adicionar**. Um painel será exibido.  
  
10. Na lista suspensa **Atributo** , selecione um atributo.  
  
11. Na lista suspensa **Operador** , selecione uma condição.  
  
12. Preencha quaisquer campos obrigatórios.  
  
13. Clique em **Salvar**. Uma nova linha será adicionada à grade **Se** .  
  
14. Como opção, para adicionar mais condições, complete as etapas 8 a 13.  
  
    > [!TIP]  
    >  Para excluir uma condição, selecione a condição, clique com o botão direito do mouse nela e clique em **Excluir**.  
  
    > [!TIP]  
    >  Você pode selecionar várias condições e clicar com o botão direito para agrupá-las dentro de um operador lógico, ou para desagrupar condições dentro de um operador lógico específico.  
  
## <a name="see-also"></a>Consulte Também  
 [Regras de negócio &#40;Master Data Services&#41;](../master-data-services/business-rules-master-data-services.md)   
 [Alterar o nome de uma regra de negócios &#40;Master Data Services&#41;](../master-data-services/change-a-business-rule-name-master-data-services.md)   
 [Configurar regras de negócio para enviar notificações &#40;Master Data Services&#41;](../master-data-services/configure-business-rules-to-send-notifications-master-data-services.md)  
  
  
