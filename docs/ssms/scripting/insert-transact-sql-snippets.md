---
title: Inserir snippets Transact-SQL
description: Saiba como escolher, inserir e modificar um snippet de código Transact-SQL que pode funcionar como ponto de partida ao gravar novas instruções Transact-SQL no Editor de Consultas do Mecanismo de Banco de Dados.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: scripting
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- IntelliSense [SQL Server], snippets
- Transact-SQL snippets, code
- snippets [Transact-SQL], how to insert
ms.assetid: d66c96f4-2e84-4d79-9bfd-3635fdd98425
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 387bb2bf62146503b8c086dd5706697b024846fa
ms.sourcegitcommit: d855def79af642233cbc3c5909bc7dfe04c4aa23
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/24/2020
ms.locfileid: "87122605"
---
# <a name="insert-transact-sql-snippets"></a>Inserir snippets Transact-SQL
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
  Um snippet de código [!INCLUDE[tsql](../../includes/tsql-md.md)] é um modelo que você pode usar como um ponto de partida ao escrever novas instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] no Editor de Consultas do [!INCLUDE[ssDE](../../includes/ssde-md.md)] .  
  
## <a name="inserting-snippets"></a>Inserindo snippets  
 Você pode usar o menu **Inserir Snippet** para abrir uma lista categorizada de snippets a serem selecionados.  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] Os snippets contêm pontos de substituição: texto que sugere a sintaxe pertinente àquele ponto. Por exemplo, o snippet CREATE TABLE tem pontos de substituição para elementos como o nome de tabela, nomes de coluna e tipos de dados de coluna. Após a inserção do snippet, você deve alterar o texto de substituição para formar uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] válida. Para obter mais informações, veja [Concluir snippets Transact-SQL](../../relational-databases/scripting/complete-transact-sql-snippets.md).  
  
#### <a name="inserting-a-snippet-by-using-the-insert-snippet-menu"></a>Inserindo um snippet usando o menu de snippet de inserção  
  
1.  Na janela do Editor de Consultas do [!INCLUDE[ssDE](../../includes/ssde-md.md)] , coloque o cursor onde você deseja inserir o snippet [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  
2.  Inicie a dica de ferramenta do seletor de snippet em um de três modos:  
  
    -   Pressione CTRL+K, CTRL+X.  
  
    -   No menu **Editar** , aponte para **IntelliSense**e clique em **Inserir Snippet**.  
  
    -   Clique com o botão direito do mouse e selecione o comando **Inserir Snippet** no menu de atalho.  
  
3.  Clique duas vezes em o snippet ou selecione o snippet do seletor de snippet e pressione TAB ou ENTER.  
  
## <a name="see-also"></a>Consulte Também  
 [Inserir snippets Transact-SQL com Surround](../../relational-databases/scripting/insert-surround-with-transact-sql-snippets.md)  
  
  
