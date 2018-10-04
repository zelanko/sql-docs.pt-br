---
title: 'Tarefa 9: Criando uma hierarquia derivada usando o Master Data Manager | Microsoft Docs'
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.topic: conceptual
ms.assetid: 3bd2ec05-933f-4947-b1fe-c9226961eb7d
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 3004c9d5ae6637f288a87c50444b46fb958e7d22
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48076876"
---
# <a name="task-9-creating-a-derived-hierarchy-using-master-data-manager"></a>Tarefa 9: Criando uma hierarquia derivada usando o Master Data Manager
  Nesta tarefa, você criará uma hierarquia derivada usando o Master Data Manager. Essa hierarquia é derivada de relações de atributo baseado em domínio entre o **Supplier** e **estado** entidades.  
  
1.  Alterne para a página principal do **Master Data Manager** clicando **SQL Server 2012 Master Data Services** na parte superior da página.  
  
2.  Clique em **Administração do Sistema** na seção **Tarefas Administrativas** .  
  
3.  Passe o mouse sobre **Manage** na barra de menus e clique **hierarquias derivadas**.  
  
     ![Menu gerenciar - hierarquias derivadas selecionada](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-01.jpg "Menu gerenciar - hierarquias derivadas selecionada")  
  
4.  Clique em **adicionar a hierarquia derivada (+)** na barra de ferramentas.  
  
     ![Botão Adicionar hierarquia derivada](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-02.jpg "botão Adicionar hierarquia derivada")  
  
5.  Tipo de **SuppliersInState** para o **nome da hierarquia derivada**.  
  
6.  Clique em **salvar** na barra de ferramentas.  
  
     ![Salvar derivada botão de hierarquia](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-03.jpg "salvar derivada botão de hierarquia")  
  
7.  Arraste **Supplier** partir **níveis disponíveis: SuppliersInState** para **níveis atuais: SuppliersInState**.  
  
     ![Entidades e hierarquias para o nível atual disponíveis](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-04.jpg "entidades e hierarquias para o nível atual disponíveis")  
  
8.  Arraste **estado** partir **níveis disponíveis: SuppliersInState** para **níveis atuais: SuppliersInState**. A tela deve ter **níveis atuais** conforme mostrado na imagem a seguir.  
  
     ![Visualização da hierarquia derivada e níveis atuais](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-05.jpg "níveis atuais e visualização de hierarquia derivada")  
  
9. No **versão prévia** janela, expanda **NY {New York}** e você deverá ver um fornecedor nesse estado, conforme mostrado na imagem anterior.  
  
10. Alterne para a página principal do **Master Data Manager** clicando **SQL Server 2012 Master Data Services** na parte superior da página.  
  
11. Clique em **Gerenciador**.  
  
12. Passe o mouse sobre **hierarquias** e clique em **Derived: SuppliersInState**.  
  
     ![Hierarquias derivadas: Menu SuppliersInState](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-06.jpg "hierarquias derivadas: Menu SuppliersInState")  
  
13. Clique em qualquer **estado** nó na **exibição de árvore** e você verá os fornecedores desse estado no painel à direita.  
  
     ![Hierarquia no Gerenciador de derivada](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-07.jpg "derivado da hierarquia no Gerenciador")  
  
## <a name="next-step"></a>Próxima etapa  
 [Lição 5: Automatizando a limpeza e a correspondência usando o SSIS](../../2014/tutorials/lesson-5-automating-the-cleansing-and-matching-using-ssis.md)  
  
  
