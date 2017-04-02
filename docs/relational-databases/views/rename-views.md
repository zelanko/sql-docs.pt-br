---
title: "Renomear exibi&#231;&#245;es | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-views"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "exibições [SQL Server], renomeando"
  - "renomeando exibições"
ms.assetid: 5eed0488-81d2-40e8-8fdf-b0a640a591d0
caps.latest.revision: 17
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 17
---
# Renomear exibi&#231;&#245;es
  Você pode renomear uma exibição no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
> [!WARNING]  
>  Se você renomear uma exibição, os códigos e aplicativos dependentes da exibição poderão falhar. Isso inclui outras consultas, exibições, procedimentos armazenados, funções definidas pelo usuário e aplicativos clientes. Observe que essas falhas ocorrerão em cascata.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Pré-requisitos](#Prerequisites)  
  
     [Segurança](#Security)  
  
-   **Para renomear uma exibição usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Acompanhamento:**  [depois de renomear uma exibição](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Prerequisites"></a> Pré-requisitos  
 Obtenha uma lista de todas as dependências da exibição. Qualquer objeto, script ou aplicativo que faça referência à exibição deve ser modificado para refletir o novo nome da exibição. Para obter mais informações, consulte [Get Information About a View](../../relational-databases/views/get-information-about-a-view.md). Recomendamos que você remova a exibição e a recrie com um novo nome em vez de renomear a exibição. Recriando a exibição, você atualiza a informações de dependência dos objetos que são referenciados na exibição.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Exige a permissão ALTER em SCHEMA ou a permissão CONTROL em OBJECT, e a permissão CREATE VIEW no banco de dados.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### Para renomear uma exibição  
  
1.  No **Pesquisador de Objetos**, expanda o banco de dados que contém a exibição que deseja renomear e expanda a pasta **Exibição** .  
  
2.  Clique com o botão direito do mouse na exibição que você deseja renomear e clique em **Renomear**.  
  
3.  Digite o novo nome da exibição.  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
 **Para renomear uma exibição**  
  
 Embora seja possível usar **sp_rename** para alterar o nome da exibição, recomendamos que você exclua a exibição existente e a crie novamente com o novo nome.  
  
 Para obter mais informações, veja [CREATE VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md) e [DROP VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/drop-view-transact-sql.md).  
  
##  <a name="FollowUp"></a> Acompanhamento: depois de renomear uma exibição  
 Verifique se todos os objetos, scripts e aplicativos que fazem referência ao nome antigo da exibição agora usam o novo nome.  
  
  