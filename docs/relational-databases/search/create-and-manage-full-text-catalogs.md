---
title: "Criar e gerenciar cat&#225;logos de texto completo | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-search"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "catálogos de texto completo [SQL Server], criando"
  - "pesquisa de texto completo [SQL Server], usando o SQL Server Management Studio"
ms.assetid: 824b7131-44a6-4815-89e6-62b7bab060e3
caps.latest.revision: 21
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 20
---
# Criar e gerenciar cat&#225;logos de texto completo
  Um catálogo de texto completo é um objeto virtual que não pertence a nenhum grupo de arquivos; trata-se de um conceito lógico que faz referência a um grupo de índices de texto completo.  
  
##  <a name="creating"></a> Criando um catálogo de texto completo  
  
#### Para criar um catálogo de texto completo  
  
1.  No Pesquisador de Objetos, expanda o servidor, **Bancos de Dados** e o banco de dados em que deseja criar um catálogo de texto completo.  
  
2.  Expanda **Armazenamento** e clique com o botão direito do mouse em **Catálogos de Texto Completo**.  
  
3.  Selecione **Novo Catálogo de Texto Completo**.  
  
4.  Na caixa de diálogo **Novo Catálogo de Texto Completo**, especifique as informações do catálogo que você está recriando. Para obter mais informações, veja [Catálogo de texto completo novo &#40;Página Geral&#41;](../Topic/New%20Full-Text%20Catalog%20\(General%20Page\).md).  
  
    > [!NOTE]  
    >  Os identificadores de catálogos de texto completo começam em 00005 e são incrementados em um para cada novo catálogo criado.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
   
  
##  <a name="props"></a> Exibindo as propriedades de um catálogo de texto completo  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] funções, como FULLTEXTCATALOGPROPERTY, podem ser usadas para obter o valor de diversas propriedades relativas à indexação de texto completo. Essas informações são úteis para administrar e solucionar problemas de pesquisa de texto completo.  
  
 A tabela a seguir lista as propriedades relacionadas a catálogos de texto completo.  
  
|Propriedade|Descrição|Função|  
|--------------|-----------------|--------------|  
|**AccentSensitivity**|Configuração da diferenciação de caracteres com/sem acento.|[FULLTEXTCATALOGPROPERTY](../../t-sql/functions/fulltextcatalogproperty-transact-sql.md)|  
|**ImportStatus**|Se o catálogo de texto completo está sendo importado.|FULLTEXTCATALOGPROPERTY|  
|**IndexSize**|Tamanho do catálogo de texto completo em megabytes (MB).|FULLTEXTCATALOGPROPERTY|  
|**ItemCount**|Número atual de itens indexados de texto completo no catálogo de texto completo.|FULLTEXTCATALOGPROPERTY|  
|**MergeStatus**|Se uma mesclagem mestra está em andamento.|FULLTEXTCATALOGPROPERTY|  
|**PopulateCompletionAge**|Diferença, em segundos, entre a conclusão da última população do índice de texto completo e 01/01/1990 00:00:00.|FULLTEXTCATALOGPROPERTY|  
|**PopulateStatus**|Status da população.<br /><br /> [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]|FULLTEXTCATALOGPROPERTY|  
|**UniqueKeyCount**|Número de chaves exclusivas no catálogo de texto completo.|FULLTEXTCATALOGPROPERTY|  
  
   
  
##  <a name="rebuildone"></a> Recriando um catálogo de texto completo  
  
#### Para recriar um catálogo de texto completo  
  
1.  No Pesquisador de Objetos, expanda o servidor, expanda **Bancos de Dados** e o banco de dados que contém o catálogo de texto completo a ser recriado.  
  
2.  Expanda **Armazenamento**e, depois, **Catálogos de texto completo**.  
  
3.  Clique com o botão direito do mouse no nome do catálogo de texto completo que deseja recriar e selecione **Recriar**.  
  
4.  Para a pergunta **Deseja excluir o catálogo de texto completo e recriá-lo?**, clique em **OK**.  
  
5.  Na caixa de diálogo **Recriar Catálogo de Texto Completo**, clique em **Fechar**.  
  
   
  
##  <a name="rebuildall"></a> Recriando todos os catálogos de texto completo para um banco de dados  
  
#### Para recriar os catálogos de texto completo para um banco de dados  
  
1.  No Pesquisador de Objetos, expanda o servidor, expanda **Bancos de Dados** e o banco de dados contendo os catálogos de texto completo a serem recriados.  
  
2.  Expanda **Armazenamento** e clique com o botão direito do mouse em **Catálogos de Texto Completo**.  
  
3.  Selecione **Recriar Tudo**.  
  
4.  Para a pergunta **Deseja excluir todos os catálogos de texto completo e recriá-los?**, clique em **OK**.  
  
5.  Na caixa de diálogo **Recriar Todos os Catálogos de Texto Completo**, clique em **Fechar**.  
  
  
  
##  <a name="removing"></a> Removendo um catálogo de texto completo de um banco de dados  
  
#### Para remover um catálogo de texto completo de um Banco de Dados  
  
1.  No Pesquisador de Objetos, expanda o servidor, **Bancos de Dados** e o banco de dados que contém o catálogo de texto completo a ser removido.  
  
2.  Expanda **Armazenamento**e **Catálogo de texto completo**.  
  
3.  Clique com o botão direito do mouse no catálogo de texto completo que deseja remover e selecione **Excluir**.  
  
4.  Na caixa de diálogo **Excluir Objetos** , clique em **OK**.  
  
  
## Consulte também  
 [CREATE FULLTEXT CATALOG &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-catalog-transact-sql.md)  
  
  