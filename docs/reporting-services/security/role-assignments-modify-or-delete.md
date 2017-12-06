---
title: "Modificar ou excluir uma atribuição de função (Gerenciador de Relatórios) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: security
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- removing role assignments
- roles [Reporting Services], assignments
- system roles [Reporting Services]
- modifying role assignments
- deleting role assignments
ms.assetid: 523bdd32-92cb-4b48-a3a9-d58b2385bde7
caps.latest.revision: "45"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 96d6e228e158ec7c00c212e2e29a11279afe42fa
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2017
---
# <a name="role-assignments---modify-or-delete"></a>Atribuições de função – Modificar ou excluir
  Uma atribuição de função mapeia uma conta de grupo ou usuário para uma definição de função predefinida que inclui as tarefas que podem ser executadas. Ela determina os tipos de operações que um usuário pode executar com relação a uma pasta, relatório, modelo ou outro tipo de conteúdo. Para criar, modificar ou excluir atribuições de função, use o Gerenciador de Relatórios. Após criar uma atribuição de função para um determinado usuário ou grupo, você pode modificá-la posteriormente selecionando uma função diferente. Para revogar permissões em um servidor de relatório, exclua uma atribuição de função desse servidor.  
  
 Dependendo de seu objetivo, abordagens alternativas podem ser mais apropriadas. Os exemplos incluem a personalização ou a criação de uma nova definição de função ou a modificação da associação de uma conta de grupo no Active Directory.  
  
 Por exemplo, suponha que você tenha um grupo de usuários que precisa gerenciar todo o conteúdo, mas não deve ter o conjunto completo de permissões associadas ao Gerenciador de Conteúdo. Nesse caso, você poderia criar uma nova definição de função chamada Gerenciador de Conteúdo do Departamento que inclui todas as tarefas do Gerenciador de Conteúdo, exceto **Definir políticas de segurança para itens**.  
  
 Similarmente, se você for um administrador de sistema ou rede e for mais fácil gerenciar as contas de grupo do Active Directory do que as atribuições de função do Gerenciador de Relatórios, reduza a sobrecarga do gerenciamento das atribuições de função criando uma única atribuição de função para uma conta de grupo e, em seguida, ajuste a associação do grupo quando os usuários não precisarem mais acessar os relatórios.  
  
 Se você considerar a modificação ou a exclusão de uma atribuição de função como a melhor abordagem, verifique as atribuições de função de sistema e de item. Cada tipo de atribuição de função é configurado em páginas diferentes do Gerenciador de Relatórios.  
  
### <a name="to-modify-or-delete-a-system-role-assignment"></a>Para modificar ou excluir uma atribuição de função de sistema  
  
1.  Inicie o [Gerenciador de Relatórios &#40;Modo Nativo do SSRS&#41;](http://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896).  
  
2.  Clique em **Configurações de Site**.  
  
3.  Clique em **Segurança**. Todas as atribuições de função do nível de sistema definidas atualmente para a implantação de servidor ou de expansão são listadas pelo nome de conta.  
  
4.  Localize a atribuição de função que deseja modificar ou excluir.  
  
5.  Para adicionar ou remover a função para um usuário ou grupo específico, clique em **Editar**.  
  
6.  Para excluir uma atribuição de função, marque a caixa de seleção próximo ao nome de usuário ou grupo e clique em **Excluir**.  
  
### <a name="to-modify-or-delete-an-item-role-assignment"></a>Para modificar ou excluir uma atribuição de função de item  
  
1.  Inicie o **Gerenciador de Relatórios** e localize o item para o qual você deseja editar ou excluir uma atribuição de função.  
  
2.  Focalize o item e clique na seta do menu suspenso.  
  
3.  No menu suspenso, clique em **Segurança**.  
  
4.  Localize a atribuição de função que deseja modificar ou excluir.  
  
5.  Para adicionar ou remover a função para um usuário ou grupo específico, clique em **Editar**.  
  
6.  Para excluir uma atribuição de função, marque a caixa de seleção próximo ao nome de usuário ou grupo e clique em **Excluir**.  
  
## <a name="see-also"></a>Consulte também  
 [Criar e gerenciar atribuições de função](../../reporting-services/security/create-and-manage-role-assignments.md)   
 [Atribuições de função](../../reporting-services/security/role-assignments.md)   
 [Página Configurações do Site &#40;Gerenciador de Relatórios&#41;](http://msdn.microsoft.com/library/4d67a01c-eae4-49ba-a6e8-8e983c0248f5)   
 [Atribuições de nova função do sistema: página Editar Atribuições de Função do Sistema &#40;Gerenciador de Relatórios&#41;](http://msdn.microsoft.com/library/62a22ab9-1eb4-4ce5-8dd7-06b5ed2d9a2a)  
  
  
