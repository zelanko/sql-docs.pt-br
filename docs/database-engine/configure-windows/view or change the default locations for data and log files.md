---
title: "Exibir ou alterar os locais padr&#227;o de arquivos de log e de dados (SQL Server Management Studio) | Microsoft Docs"
ms.custom: ""
ms.date: "03/13/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "arquivos de log [SQL Server], alterando local padrão"
  - "arquivos de dados [SQL Server], alterando local padrão"
ms.assetid: 70a57fda-fcfe-490f-9cf6-5df620e32b2a
caps.latest.revision: 16
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
---
# Exibir ou alterar os locais padr&#227;o de arquivos de log e de dados (SQL Server Management Studio)
  Este tópico descreve como exibir e alterar os locais padrão de novos arquivos de log e de dados no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. O caminho padrão é obtido do Registro. Depois que você alterar o local, todos os novos bancos de dados criados na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usarão esse local se um local diferente não for especificado.  
  
 
##  <a name="Recommendations"></a> Recomendações  
 A prática recomendada para proteger seus arquivos de dados e arquivos de log é garantir que eles sejam protegidos por ACLs (listas de controle de acesso). Defina as ACLs no diretório raiz em que os arquivos são criados.  
  
  
## Exibir ou alterar os locais padrão dos arquivos de banco de dados  
  
1.  No Pesquisador de Objetos, clique com o botão direito do mouse no servidor e clique em **Propriedades**.  
  
2.  No painel esquerdo, na página Propriedades, clique na **Configurações do banco de dados**.  
  
3.  Em **Locais padrão de banco de dados**, exiba os locais atuais padrão dos novos arquivos de dados e novos arquivos de log. Para alterar um local padrão, digite um novo nome de caminho padrão no campo **Dados** ou **Log** ou clique no botão Procurar para localizar e selecionar um nome de caminho.  
  
>**OBSERVAÇÃO:** depois de alterar os locais padrão, é necessário interromper e iniciar o serviço SQL Server para concluir a alteração.  
  
## Consulte também  
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [Criar um banco de dados](../../relational-databases/databases/create-a-database.md)  
  
  