---
title: 'Tarefa 4: Criando um projeto SSIS usando o SQL Server Data Tools | Microsoft Docs'
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 8603ea91-2ec4-40b6-8070-4f824332f5d3
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 03c0a6599990357a255fab3beeb434db3cb5d97d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36117058"
---
# <a name="task-4-creating-an-ssis-project-using-sql-server-data-tools"></a>Tarefa 4: Criando um projeto SSIS usando o SQL Server Data Tools
  Nesta tarefa, você deve criar um projeto SSIS usando **SQL Server Data Tools** para automatizar a limpeza e correspondência de dados do fornecedor.  
  
1.  Inicie o **SQL Server Data Tools**. Clique em Iniciar, aponte para **todos os programas**, expanda **Microsoft SQL Server 2012**e clique em **SQL Server Data Tools**.  
  
2.  No menu **Arquivo** , aponte para **Novo**e clique em **Projeto**.  
  
3.  Expanda **Business Intelligence** no **modelos instalados** painel e selecione **Integration Services**.  
  
     ![Visual Studio - caixa de diálogo Novo projeto](../../2014/tutorials/media/et-creatinganssisprojectusingsqlsdt-01.jpg "Visual Studio - caixa de diálogo Novo projeto")  
  
4.  Selecione **projeto do Integration Services** no **lista de tipos de projeto**.  
  
5.  Tipo **CleanseAndCurateSuppliers** para **nome** e clique em **Okey**.  
  
6.  Em **Solution Explorer** janela, clique com botão direito **dtsx** e selecione **Renomear**. Se você não vir **Solution Explorer** janela, clique em **exibição** na barra de menus, clique em **Gerenciador de soluções**.  
  
     ![Package. dtsx - Menu Renomear](../../2014/tutorials/media/et-creatinganssisprojectusingsqlsdt-02.jpg "Package. dtsx - Menu renomear")  
  
7.  Tipo **Cleanseandcurate** e pressione **ENTER**. Verifique se o **extensão** permanece **dtsx**.  
  
## <a name="next-step"></a>Próxima etapa  
 [Tarefa 5: Adicionando a tarefa de fluxo de dados](task-5-adding-data-flow-task.md)  
  
  