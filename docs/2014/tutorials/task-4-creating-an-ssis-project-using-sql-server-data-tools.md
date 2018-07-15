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
ms.topic: conceptual
ms.assetid: 8603ea91-2ec4-40b6-8070-4f824332f5d3
caps.latest.revision: 7
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a6fb09370b01a88c23d75b843d588626ed96c9b1
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37208066"
---
# <a name="task-4-creating-an-ssis-project-using-sql-server-data-tools"></a>Tarefa 4: Criando um projeto SSIS usando o SQL Server Data Tools
  Nesta tarefa, você criará um projeto do SSIS por meio **SQL Server Data Tools** para automatizar a limpeza e correspondência de dados do fornecedor.  
  
1.  Inicie o **SQL Server Data Tools**. Clique em Iniciar, aponte para **todos os programas**, expanda **Microsoft SQL Server 2012**e clique em **SQL Server Data Tools**.  
  
2.  No menu **Arquivo** , aponte para **Novo**e clique em **Projeto**.  
  
3.  Expandir **Business Intelligence** na **modelos instalados** painel e selecione **Integration Services**.  
  
     ![Visual Studio - caixa de diálogo Novo projeto](../../2014/tutorials/media/et-creatinganssisprojectusingsqlsdt-01.jpg "Visual Studio - caixa de diálogo Novo projeto")  
  
4.  Selecione **projeto do Integration Services** na **lista de tipos de projeto**.  
  
5.  Tipo de **CleanseAndCurateSuppliers** para **nome** e clique em **Okey**.  
  
6.  Na **Gerenciador de soluções** janela, clique com botão direito **Package. dtsx** e selecione **Renomear**. Se você não vir **Gerenciador de soluções** janela, clique em **exibição** na barra de menus, clique em **Gerenciador de soluções**.  
  
     ![Package. dtsx - Menu Renomear](../../2014/tutorials/media/et-creatinganssisprojectusingsqlsdt-02.jpg "Package. dtsx - Menu renomear")  
  
7.  Tipo de **Cleanseandcurate** e pressione **ENTER**. Certifique-se de que o **extensão** permanece **dtsx**.  
  
## <a name="next-step"></a>Próxima etapa  
 [Tarefa 5: Adicionando a tarefa de fluxo de dados](task-5-adding-data-flow-task.md)  
  
  
