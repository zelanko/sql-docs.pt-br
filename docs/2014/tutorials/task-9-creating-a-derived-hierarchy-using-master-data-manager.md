---
title: 'Tarefa 9: Criando uma hierarquia derivada usando o Master Data Manager | Microsoft Docs'
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3bd2ec05-933f-4947-b1fe-c9226961eb7d
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 35584d33afac7a2a8f74abd013288a974cade512
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36130453"
---
# <a name="task-9-creating-a-derived-hierarchy-using-master-data-manager"></a>Tarefa 9: Criando uma hierarquia derivada usando o Master Data Manager
  Nesta tarefa, você criará uma hierarquia derivada usando o Master Data Manager. Essa hierarquia é derivada de relações de atributo baseado em domínio entre o **Supplier** e **estado** entidades.  
  
1.  Alterne para a página principal do **Master Data Manager** clicando **SQL Server 2012 Master Data Services** na parte superior da página.  
  
2.  Clique em **Administração do Sistema** na seção **Tarefas Administrativas** .  
  
3.  Passe o mouse sobre **gerenciar** na barra de menus, clique em **hierarquias derivadas**.  
  
     ![Menu gerenciar - hierarquias derivadas selecionada](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-01.jpg "Menu gerenciar - hierarquias derivadas selecionada")  
  
4.  Clique em **adicionar a hierarquia derivada (+)** na barra de ferramentas.  
  
     ![Botão Adicionar hierarquia derivada](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-02.jpg "botão Adicionar hierarquia derivada")  
  
5.  Tipo **SuppliersInState** para o **nome da hierarquia derivada**.  
  
6.  Clique em **salvar** na barra de ferramentas.  
  
     ![Salvar derivado hierarquia botão](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-03.jpg "salvar derivado de botão de hierarquia")  
  
7.  Arraste **Supplier** de **níveis disponíveis: SuppliersInState** para **níveis atuais: SuppliersInState**.  
  
     ![Entidades e hierarquias para o nível atual disponíveis](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-04.jpg "entidades e hierarquias para o nível atual disponíveis")  
  
8.  Arraste **estado** de **níveis disponíveis: SuppliersInState** para **níveis atuais: SuppliersInState**. A tela deve ter **níveis atuais** conforme mostrado na figura a seguir.  
  
     ![Visualização da hierarquia derivada e níveis atuais](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-05.jpg "níveis atuais e visualização de hierarquia derivada")  
  
9. No **visualização** janela, expanda **NY {New York}** e você deverá ver um fornecedor nesse estado, conforme mostrado na imagem anterior.  
  
10. Alterne para a página principal do **Master Data Manager** clicando **SQL Server 2012 Master Data Services** na parte superior da página.  
  
11. Clique em **Gerenciador**.  
  
12. Passe o mouse sobre **hierarquias** e clique em **Derived: SuppliersInState**.  
  
     ![Hierarquias derivadas: Menu SuppliersInState](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-06.jpg "hierarquias derivadas: Menu SuppliersInState")  
  
13. Clique em qualquer **estado** nó o **exibição de árvore** e você verá os fornecedores desse estado no painel direito.  
  
     ![Hierarquia no Pesquisador de objetos derivada](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-07.jpg "hierarquia no Pesquisador de objetos derivada")  
  
## <a name="next-step"></a>Próxima etapa  
 [Lição 5: Automatizando a limpeza e a correspondência usando o SSIS](../../2014/tutorials/lesson-5-automating-the-cleansing-and-matching-using-ssis.md)  
  
  