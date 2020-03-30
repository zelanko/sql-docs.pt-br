---
title: Exibir e editar dados em uma tabela
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
f1_keywords:
- SQL.DATA.TOOLS.QUERYRESULTS.F1
- sql.data.tools.queryresults.executequerydeletingrow
ms.assetid: bb67ce83-a87a-4e14-84cd-9a5930fe74c8
author: markingmyname
ms.author: maghan
manager: jroth
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: 557b5d5c5986b47eab22bb9d70bd8103c5032eeb
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75226756"
---
# <a name="how-to-view-and-edit-data-in-a-table"></a>Como: Exibir e editar dados em uma tabela

Você pode exibir, editar e excluir dados de uma tabela existente usando um Editor de Dados visual.  
  
> [!WARNING]  
> Os procedimentos a seguir usam entidades criadas em procedimentos anteriores na seção [Desenvolvimento de banco de dados conectado](../ssdt/connected-database-development.md).  
  
### <a name="to-edit-data-in-a-table-visually-using-the-data-editor"></a>Para editar dados visualmente em uma tabela usando o Editor de Dados  
  
1.  Clique com o botão direito do mouse na tabela **Produtos** no **Pesquisador de Objetos do SQL Server** e selecione **Exibir Dados**.  
  
2.  O Editor de Dados é lançado. Observe as linhas que nós adicionamos à tabela em procedimentos anteriores.  
  
3.  Clique com o botão direito do mouse na tabela **Frutas** no Pesquisador de Objetos do SQL Server e selecione **Exibir Dados**.  
  
4.  No Editor de Dados, digite **1** para **Id** e **True** para **Perecíveis**, em seguida, pressione ENTER ou TAB para deslocar o foco da nova linha para confirmá-la no banco de dados.  
  
5.  Repita a etapa anterior para inserir **2**, **False** e **3**, **False** na tabela.  
  
    Observe que, enquanto você está editando uma linha, sempre pode reverter as alterações para uma célula pressionando ESC.  
  
6.  Você pode exibir suas edições como um script clicando no botão **Script** na barra de ferramentas. Como alternativa, você pode usar o botão **Script para Arquivo** para salvá-los em um arquivo de script .sql a ser executado posteriormente.  
  
7.  Clique com o botão direito do mouse no banco de dados **Trade** no **Pesquisador de Objetos do SQL Server** e selecione **Nova Consulta**. No editor, digite `select * from dbo.PerishableFruits` e pressione o botão **Executar Consulta** para retornar os dados representados pela exibição `PerishableFruits`.  
  
