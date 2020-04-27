---
title: Criar e publicar uma regra de negócios (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- business rules [Master Data Services], creating
- creating business rules [Master Data Services]
ms.assetid: 6961d636-4d69-468e-81f7-8d0be6a4a039
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 2b52be0b8c76333b069c018415ff698f13f824ae
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "65479892"
---
# <a name="create-and-publish-a-business-rule-master-data-services"></a>Criar e publicar uma regra de negócio (Master Data Services)
  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], crie uma regra de negócio para garantir a exatidão de seus dados mestres. Depois de ser criada, uma regra deve ser publicada para poder ser aplicada aos dados.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional **Administração do sistema** .  
  
-   Você deve ser um administrador de modelo. Para obter mais informações, consulte [administradores &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
### <a name="to-create-and-publish-a-business-rule"></a>Para criar e publicar uma regra de negócio  
  
1.  No [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], clique em **Administração do Sistema**.  
  
2.  Na barra de menus, aponte para **Gerenciar** e clique em **Regras de Negócios**.  
  
3.  Na página **Manutenção de Regra de Negócio** , na lista **Modelo** , selecione um modelo.  
  
4.  Na lista **Entidade** , selecione uma entidade.  
  
5.  Na lista **Tipo de Membro** , selecione um tipo de membro ao qual a regra de negócio será aplicada.  
  
6.  Na lista **Atributo** , selecione um atributo ou deixe o valor padrão **Todos**.  
  
7.  Clique em **Adicionar regra de negócio**.  
  
8.  Clique em **Editar regra de negócio selecionada**.  
  
9. No painel **Componentes** , expanda o nó **Condições** .  
  
10. Clique em uma condição e arraste-a para o rótulo de **condições** do painel de **If** .  
  
    > [!TIP]  
    >  Você pode excluir itens de sua regra de negócio clicando com o botão direito do mouse e escolhendo **excluir**.  
  
11. No painel **atributos** , clique em um atributo e arraste-o para o rótulo de **atributo selecionar** do painel de **condição de edição** .  
  
12. No painel **Editar condição** , preencha todos os campos obrigatórios.  
  
13. No painel **Editar Condição** , clique em **Salvar item**.  
  
14. No painel **Componentes** , expanda o nó **Ações** .  
  
15. Clique em uma ação e arraste-a até o rótulo **Ação** do painel **THEN** .  
  
16. No painel **Atributos** , clique em um atributo e arraste-o até o rótulo **Selecionar atributo** do painel **Editar Ação** .  
  
17. No painel **Editar Ação** , preencha os campos necessários.  
  
18. No painel **Editar Ação** , clique em **Salvar item**.  
  
19. Opcionalmente, adicione várias condições à regra. Para obter mais informações, veja [Adicionar várias condições a uma regra de negócio &#40;Master Data Services&#41;](../../2014/master-data-services/add-multiple-conditions-to-a-business-rule-master-data-services.md).  
  
20. Clique em **Voltar**.  
  
21. Opcionalmente, na página **Manutenção de Regra de Negócio** , na linha que contém sua regra de negócio, clique duas vezes em uma célula da coluna **Nome**, **Descrição**ou **Notificação** para atualizar o valor.  
  
    > [!NOTE]  
    >  Notificações são enviadas somente para regras que incluem uma ação de validação.  
  
22. Clique em **Publicar regras de negócio**.  
  
23. Na caixa de diálogo de confirmação, clique em **OK**. O status da regra mudará para **Ativo**.  
  
## <a name="next-steps"></a>Próximas etapas  
  
-   Aplique regras de negócio a dados seguindo um destes procedimentos:  
  
    -   [Validar membros específicos em relação a regras de negócio &#40;Master Data Services&#41;](../../2014/master-data-services/validate-specific-members-against-business-rules-master-data-services.md)  
  
    -   [Validar uma versão em relação a regras de negócio &#40;Master Data Services&#41;](../../2014/master-data-services/validate-a-version-against-business-rules-master-data-services.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Configurar regras de negócio para enviar notificações &#40;Master Data Services&#41;](../../2014/master-data-services/configure-business-rules-to-send-notifications-master-data-services.md)   
 [Alterar o nome de uma regra de negócio &#40;Master Data Services&#41;](../../2014/master-data-services/change-a-business-rule-name-master-data-services.md)   
 [Adicionar várias condições a uma regra de negócios &#40;Master Data Services&#41;](../../2014/master-data-services/add-multiple-conditions-to-a-business-rule-master-data-services.md)  
  
  
