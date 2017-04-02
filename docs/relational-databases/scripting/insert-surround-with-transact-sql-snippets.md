---
title: "Inserir trechos Transact-SQL com Surround | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "trechos [Transact-SQL], cercar com"
  - "IntelliSense [SQL Server], cercar com trechos"
  - "trechos do Transact-SQL, cercar com"
ms.assetid: 5b5a8c6c-968e-4361-a7f5-9e2ac186d927
caps.latest.revision: 6
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 6
---
# Inserir trechos Transact-SQL com Surround
  Um trecho com surround é um modelo que você pode usar como ponto de partida ao colocar um conjunto de instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] em um bloco BEGIN, IF ou WHILE.  
  
## Inserindo trechos com surround  
 Trechos com surround podem ser iniciados por uma das três maneiras: por meio de um atalho de teclado, menu **Editar** e menu de contexto.  
  
 Após a inserção do trecho, você deve alterar o texto de substituição para formar uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] válida. Para obter mais informações, veja [Concluir trechos de código Transact-SQL](../../relational-databases/scripting/complete-transact-sql-snippets.md).  
  
#### Para inserir um trecho com surround  
  
1.  Na janela Editor de Consulta do [!INCLUDE[ssDE](../../includes/ssde-md.md)], selecione o conjunto de instruções a serem incluídas no bloco.  
  
2.  Use um destes três métodos para exibir a lista de trechos com surround:  
  
    -   Digite CTRL+K, CTRL+S.  
  
    -   No menu **Editar**, aponte para **IntelliSense** e selecione o comando **Surround With**.  
  
    -   Clique com o botão direito do mouse no texto selecionado e selecione o comando **Surround With** no menu de contexto.  
  
3.  Selecione o nome do trecho (BEGIN, IF ou WHILE) na lista usando o mouse ou digitando-o e pressionando TAB ou ENTER.  
  
## Consulte também  
 [Inserir trechos Transact-SQL](../../relational-databases/scripting/insert-transact-sql-snippets.md)  
  
  