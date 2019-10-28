---
title: Renomear exibições | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: table-view-index, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- views [SQL Server], renaming
- renaming views
ms.assetid: 5eed0488-81d2-40e8-8fdf-b0a640a591d0
author: stevestein
ms.author: sstein
ms.manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 132a9d08f41d29ef5b11404d7b662122abdc8516
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/25/2019
ms.locfileid: "72909383"
---
# <a name="rename-views"></a>Renomear exibições
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-all-md.md)]
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
  
-   **Acompanhamento:**  [Depois de renomear uma exibição](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Prerequisites"></a> Pré-requisitos  
 Obtenha uma lista de todas as dependências da exibição. Qualquer objeto, script ou aplicativo que faça referência à exibição deve ser modificado para refletir o novo nome da exibição. Para obter mais informações, consulte [Get Information About a View](../../relational-databases/views/get-information-about-a-view.md). Recomendamos que você remova a exibição e a recrie com um novo nome em vez de renomear a exibição. Recriando a exibição, você atualiza a informações de dependência dos objetos que são referenciados na exibição.  
  
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
  
 Para obter mais informações, veja [CREATE VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md) e [DROP VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/drop-view-transact-sql.md).  
  
##  <a name="FollowUp"></a> Acompanhamento: Depois de renomear uma exibição  
 Verifique se todos os objetos, scripts e aplicativos que fazem referência ao nome antigo da exibição agora usam o novo nome.  
  
  
