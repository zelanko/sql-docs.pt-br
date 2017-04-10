---
title: "Modificar ou excluir uma atribui&#231;&#227;o de fun&#231;&#227;o (Gerenciador de Relat&#243;rios) | Microsoft Docs"
ms.custom: ""
ms.date: "12/29/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "removendo atribuições de função"
  - "funções [Reporting Services], atribuições"
  - "função do sistema [Reporting Services]"
  - "modificando atribuições de função"
  - "excluindo atribuições de função"
ms.assetid: 523bdd32-92cb-4b48-a3a9-d58b2385bde7
caps.latest.revision: 45
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
---
# Modificar ou excluir uma atribui&#231;&#227;o de fun&#231;&#227;o (Gerenciador de Relat&#243;rios)
  Uma atribuição de função mapeia uma conta de grupo ou usuário para uma definição de função predefinida que inclui as tarefas que podem ser executadas. Ela determina os tipos de operações que um usuário pode executar com relação a uma pasta, relatório, modelo ou outro tipo de conteúdo. Para criar, modificar ou excluir atribuições de função, use o Gerenciador de Relatórios. Após criar uma atribuição de função para um determinado usuário ou grupo, você pode modificá-la posteriormente selecionando uma função diferente. Para revogar permissões em um servidor de relatório, exclua uma atribuição de função desse servidor.  
  
 Dependendo de seu objetivo, abordagens alternativas podem ser mais apropriadas. Os exemplos incluem a personalização ou a criação de uma nova definição de função ou a modificação da associação de uma conta de grupo no Active Directory.  
  
 Por exemplo, suponha que você tenha um grupo de usuários que precisa gerenciar todo o conteúdo, mas não deve ter o conjunto completo de permissões associadas ao Gerenciador de Conteúdo. Nesse caso, você poderia criar uma nova definição de função chamada Gerenciador de Conteúdo do Departamento que inclui todas as tarefas do Gerenciador de Conteúdo, exceto **Definir políticas de segurança para itens**.  
  
 Similarmente, se você for um administrador de sistema ou rede e for mais fácil gerenciar as contas de grupo do Active Directory do que as atribuições de função do Gerenciador de Relatórios, reduza a sobrecarga do gerenciamento das atribuições de função criando uma única atribuição de função para uma conta de grupo e, em seguida, ajuste a associação do grupo quando os usuários não precisarem mais acessar os relatórios.  
  
 Se você considerar a modificação ou a exclusão de uma atribuição de função como a melhor abordagem, verifique as atribuições de função de sistema e de item. Cada tipo de atribuição de função é configurado em páginas diferentes do Gerenciador de Relatórios.  
  
### Para modificar ou excluir uma atribuição de função de sistema  
  
1.  Inicie o [Gerenciador de Relatórios &#40;Modo Nativo do SSRS&#41;](../Topic/Report%20Manager%20%20\(SSRS%20Native%20Mode\).md).  
  
2.  Clique em **Configurações de Site**.  
  
3.  Clique em **Segurança**. Todas as atribuições de função do nível de sistema definidas atualmente para a implantação de servidor ou de expansão são listadas pelo nome de conta.  
  
4.  Localize a atribuição de função que deseja modificar ou excluir.  
  
5.  Para adicionar ou remover a função para um usuário ou grupo específico, clique em **Editar**.  
  
6.  Para excluir uma atribuição de função, marque a caixa de seleção próximo ao nome de usuário ou grupo e clique em **Excluir**.  
  
### Para modificar ou excluir uma atribuição de função de item  
  
1.  Inicie o **Gerenciador de Relatórios** e localize o item para o qual você deseja editar ou excluir uma atribuição de função.  
  
2.  Focalize o item e clique na seta do menu suspenso.  
  
3.  No menu suspenso, clique em **Segurança**.  
  
4.  Localize a atribuição de função que deseja modificar ou excluir.  
  
5.  Para adicionar ou remover a função para um usuário ou grupo específico, clique em **Editar**.  
  
6.  Para excluir uma atribuição de função, marque a caixa de seleção próximo ao nome de usuário ou grupo e clique em **Excluir**.  
  
## Consulte também  
 [Criar e gerenciar atribuições de função](../../reporting-services/security/create-and-manage-role-assignments.md)   
 [Atribuições de função](../../reporting-services/security/role-assignments.md)   
 [Página Configurações de Site &#40;Gerenciador de Relatórios&#41;](../Topic/Site%20Settings%20Page%20\(Report%20Manager\).md)   
 [Atribuições de nova função do sistema: página Editar atribuições de função do sistema &#40;Gerenciador de Relatórios&#41;](../Topic/New%20System%20Role%20Assignments:%20Edit%20System%20Role%20Assignments%20Page%20\(Report%20Manager\).md)  
  
  