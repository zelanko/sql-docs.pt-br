---
title: Renomear exibições | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-views
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- views [SQL Server], renaming
- renaming views
ms.assetid: 5eed0488-81d2-40e8-8fdf-b0a640a591d0
caps.latest.revision: 16
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 84951488cfa1966468152f97b204ea6e0d08f92e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36117102"
---
# <a name="rename-views"></a>Renomear exibições
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
  
-   **Follow Up:**  [After renaming a view](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Prerequisites"></a> Pré-requisitos  
 Obtenha uma lista de todas as dependências da exibição. Qualquer objeto, script ou aplicativo que faça referência à exibição deve ser modificado para refletir o novo nome da exibição. Para obter mais informações, consulte [Get Information About a View](get-information-about-a-view.md). Recomendamos que você remova a exibição e a recrie com um novo nome em vez de renomear a exibição. Recriando a exibição, você atualiza a informações de dependência dos objetos que são referenciados na exibição.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Exige a permissão ALTER em SCHEMA ou a permissão CONTROL em OBJECT, e a permissão CREATE VIEW no banco de dados.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-rename-a-view"></a>Para renomear uma exibição  
  
1.  No **Pesquisador de Objetos**, expanda o banco de dados que contém a exibição que deseja renomear e expanda a pasta **Exibição** .  
  
2.  Clique com o botão direito do mouse na exibição que você deseja renomear e clique em **Renomear**.  
  
3.  Digite o novo nome da exibição.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
 **Para renomear uma exibição**  
  
 Embora seja possível usar **sp_rename** para alterar o nome da exibição, recomendamos que você exclua a exibição existente e a crie novamente com o novo nome.  
  
 Para obter mais informações, veja [CREATE VIEW &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-view-transact-sql) e [DROP VIEW &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-view-transact-sql).  
  
##  <a name="FollowUp"></a> Acompanhamento: depois de renomear uma exibição  
 Verifique se todos os objetos, scripts e aplicativos que fazem referência ao nome antigo da exibição agora usam o novo nome.  
  
  
