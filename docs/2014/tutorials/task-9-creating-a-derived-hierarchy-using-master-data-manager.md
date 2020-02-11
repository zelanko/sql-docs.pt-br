---
title: 'Tarefa 9: criando uma hierarquia derivada usando Master Data Manager | Microsoft Docs'
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 3bd2ec05-933f-4947-b1fe-c9226961eb7d
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 7cb2f12115e3fe743c49c2f7e69f765da4501ba2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "65489533"
---
# <a name="task-9-creating-a-derived-hierarchy-using-master-data-manager"></a>Tarefa 9: Criando uma hierarquia derivada usando o Master Data Manager
  Nesta tarefa, você criará uma hierarquia derivada usando o Master Data Manager. Essa hierarquia derivada é derivada das relações de atributo baseadas em domínio entre as entidades **fornecedor** e **estado** .  
  
1.  Alterne para a página principal do **Master Data Manager** clicando em **SQL Server 2012 Master Data Services** na parte superior da página.  
  
2.  Clique em **Administração do Sistema** na seção **Tarefas Administrativas** .  
  
3.  Passe o mouse sobre **gerenciar** na barra de menus e clique em **hierarquias derivadas**.  
  
     ![Menu Gerenciar - Hierarquias Derivadas selecionada](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-01.jpg "Menu Gerenciar - Hierarquias Derivadas selecionada")  
  
4.  Clique no botão **Adicionar hierarquia derivada (+)** na barra de ferramentas.  
  
     ![Botão Adicionar Hierarquia Derivada](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-02.jpg "Botão Adicionar Hierarquia Derivada")  
  
5.  Digite **SuppliersInState** para o **nome da hierarquia derivada**.  
  
6.  Clique no botão **salvar** na barra de ferramentas.  
  
     ![Botão Salvar Hierarquia Derivada](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-03.jpg "Botão Salvar Hierarquia Derivada")  
  
7.  Arraste **fornecedor** dos **níveis disponíveis: SuppliersInState** para **os níveis atuais: SuppliersInState**.  
  
     ![Entidades e Hierarquias Disponíveis para nível atual](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-04.jpg "Entidades e Hierarquias Disponíveis para nível atual")  
  
8.  Arraste o **estado** dos **níveis disponíveis: SuppliersInState** para **os níveis atuais: SuppliersInState**. A tela deve ter **níveis atuais** , conforme mostrado na imagem a seguir.  
  
     ![Visualização e níveis atuais de Hierarquia Derivada](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-05.jpg "Visualização e níveis atuais de Hierarquia Derivada")  
  
9. Na janela de **Visualização** , expanda **NY {Nova York}** e você verá um fornecedor nesse estado, conforme mostrado na imagem anterior.  
  
10. Alterne para a página principal do **Master Data Manager** clicando em **SQL Server 2012 Master Data Services** na parte superior da página.  
  
11. Clique em **Gerenciador**.  
  
12. Passe o mouse sobre **hierarquias** e clique em **derivado: SuppliersInState**.  
  
     ![Hierarquias Derivadas: Menu SuppliersInState](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-06.jpg "Hierarquias Derivadas: Menu SuppliersInState")  
  
13. Clique em qualquer nó de **estado** no **modo de exibição de árvore** e você deverá ver os fornecedores nesse estado no painel direito.  
  
     ![Hierarquia Derivada no Explorer](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-07.jpg "Hierarquia Derivada no Explorer")  
  
## <a name="next-step"></a>Próxima etapa  
 [Lição 5: Automatizando a limpeza e a correspondência usando o SSIS](../../2014/tutorials/lesson-5-automating-the-cleansing-and-matching-using-ssis.md)  
  
  
