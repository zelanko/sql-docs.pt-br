---
title: Use o Designer de Tabela para gerenciar tabelas e relacionamentos
description: Familiarize-se com o Designer de Tabela. Confira como usar essa ferramenta para criar e editar a estrutura da tabela de banco de dados e para exibir relações entre objetos de banco de dados.
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
f1_keywords:
- sql.data.tools.design.table.columnspecification.index.dialog
- sql.data.tools.design.table.columnsgrid.view
- sql.data.tools.design.table.scriptpanel
ms.assetid: 322a2903-d7a6-4f52-9048-1bd413b4c799
author: markingmyname
ms.author: maghan
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: 4262242a0ac9822bed793e1bd78a4ce51294d485
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85895804"
---
# <a name="how-to-use-the-table-designer-to-manage-tables-and-relationships"></a>Como fazer: Usar o Designer de Tabela para gerenciar tabelas e relacionamentos

O Designer de Tabela fornece uma experiência visual juntamente com o Editor Transact\-SQL para criar e editar a estrutura de tabelas, incluindo objetos de programação específicos de tabela, para bancos de dados do SQL Server.  Ele é iniciado quando você cria uma nova tabela para um banco de dados conectado ou um projeto, ou quando você clica duas vezes para editar uma tabela no Pesquisador de Objetos do SQL Server ou no Gerenciador de Soluções.  
  
O designer é composto por Grade de Colunas, Painel de Script e Painel Contexto. A Grade de Colunas lista todas as colunas na tabela. Você pode adicionar, editar e excluir colunas nesta grade.  O Painel de Contexto lhe dá uma visão lógica da definição de tabela (Chaves, Índices, Restrições, Gatilhos, etc.) e permite que você selecione um objeto para realçar as relações com colunas individuais. Você também pode adicionar novos objetos à tabela nesse painel e editar as propriedades de um objeto selecionado na Grade de Propriedades. O Painel de Script mostra a definição da estrutura de tabela, realça o script do objeto selecionado no Painel Contexto ou Grade de Colunas. Você pode editar o script lado a lado com a Grade de Colunas e o Painel Contexto na exibição. As alterações de qualquer um dos três painéis serão propagadas para os outros dois imediatamente.  
  
> [!WARNING]  
> Os procedimentos a seguir usam entidades criadas em procedimentos nas seções [Desenvolvimento de banco de dados conectado](../ssdt/connected-database-development.md) e [Desenvolvimento de banco de dados offline orientado a projetos](../ssdt/project-oriented-offline-database-development.md).  
  
### <a name="to-create-a-new-table"></a>Para criar uma tabela nova  
  
1.  Abra o projeto TradeDev em que você tem trabalhado em procedimentos anteriores.  
  
2.  No **Gerenciador de Soluções**, expanda a pasta **dbo**, clique com o botão direito na pasta **Tabelas** e selecione **Adicionar** e **Tabela**.  
  
3.  Dê um nome à nova tabela **Shipper** e clique em **Adicionar**.  
  
4.  O Designer de Tabela é aberto. Na Grade de Colunas, adicione uma nova coluna à tabela com o nome **ShipperName** e o Tipo de Dados **int**.  
  
5.  Observe que você também pode editar as propriedades de colunas na janela **Propriedades**. Clique na coluna **ShipperName** e, na janela **Propriedades**, altere o **Tipo de Dados** desta coluna para **nvarchar** e o **comprimento** para **128**. Observe que, à medida que você desloca o foco para fora do campo, o Painel de Script e a Grade de Colunas do designer são atualizados automaticamente para refletir a sua alteração.  
  
### <a name="to-create-a-new-foreign-key-constraint"></a>Para criar uma nova restrição de chave estrangeira  
  
1.  Clique com o botão direito no nó **Chaves Estrangeiras** no Painel Contexto do designer e selecione **Adicionar Nova Chave Estrangeira**.  
  
2.  Observe que a contagem do nó é incrementada automaticamente em 1. Pressione ENTER para aceitar o nome padrão da restrição.  
  
3.  Substitua a definição padrão da restrição no Painel de Script pelo seguinte.  
  
    ```  
    CONSTRAINT [FK_Shipper_Products] FOREIGN KEY ([Id]) REFERENCES [dbo].[Products]([Id])  
    ```  
  
    Observe que a experiência de criar e editar entidades de banco de dados para um projeto offline é idêntica a executar as tarefas com um banco de dados conectado.  
  
## <a name="see-also"></a>Consulte Também  
[Como: Criar objetos de banco de dados usando o Designer de Tabela](../ssdt/how-to-create-database-objects-using-table-designer.md)  
  
