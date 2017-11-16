---
title: Duplicar tabelas | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- copying tables
- tables [SQL Server], duplicating
- duplicating tables
- table copying [SQL Server]
ms.assetid: c6b07423-d1e5-4e5e-8681-5088921f5df3
caps.latest.revision: "15"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 5126bfa281db7e6b8fa295b338137e9d4b2bf1b7
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="duplicate-tables"></a>Duplicar tabelas
[!INCLUDE[tsql-appliesto-ss2016-all_md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  Você pode duplicar uma tabela existente no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)] criando uma nova tabela e copiando as informações de coluna de uma tabela existente.  
  
> [!IMPORTANT]  
>  Essa operação duplica apenas a estrutura de uma tabela; ela não duplica nenhuma linha da tabela.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para duplicar uma tabela usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Exige permissão CREATE DATABASE no banco de dados de destino.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-duplicate-a-table"></a>Para duplicar uma tabela  
  
1.  Verifique se você está conectado ao banco de dados em que deseja criar a tabela e se o banco de dados está selecionado no Pesquisador de Objetos.  
  
2.  No Pesquisador de Objetos, clique com o botão direito do mouse em **Tabelas** e clique em **Nova Tabela**.  
  
3.  No Pesquisador de Objetos, clique com o botão direito do mouse na tabela que deseja copiar e clique em **Design**.  
  
4.  Selecione as colunas na tabela existente e, no menu **Editar** , clique em **Copiar**.  
  
5.  Volte para a nova tabela nova e selecione a primeira linha.  
  
6.  No menu **Editar** , clique em **Colar**.  
  
7.  No menu **Arquivo** , clique em **Salvar***table name*.  
  
8.  Na caixa de diálogo **Escolher Nome** , digite um nome para a nova tabela e clique em **OK**.  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
  
#### <a name="to-duplicate-a-table-in-query-editor"></a>Para duplicar uma tabela no Editor de Consultas  
  
1.  Verifique se você está conectado ao banco de dados em que deseja criar a tabela e se o banco de dados está selecionado no Pesquisador de Objetos.  
  
2.  Clique com o botão direito do mouse na tabela que você deseja duplicar, aponte para **Gerar Script de Tabela como**e para **CREATE to**e selecione **Nova Janela do Editor de Consultas**.  
  
3.  Altere o nome da tabela.  
  
4.  Remova as colunas que não são necessárias na nova tabela.  
  
5.  Clique em **Executar**.  
  
  
