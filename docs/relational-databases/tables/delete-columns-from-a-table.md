---
description: Excluir colunas de uma tabela
title: Excluir colunas de uma tabela | Microsoft Docs
ms.custom: ''
ms.date: 04/11/2017
ms.prod: sql
ms.prod_service: table-view-index, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- columns [SQL Server], deleting
- removing columns
- deleting columns
- dropping columns
ms.assetid: 0d8f6e4f-bc71-4fa3-8615-74249c8e072d
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2ad600234ac931f408cdf60ba5b2a855823f8151
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88446431"
---
# <a name="delete-columns-from-a-table"></a>Excluir colunas de uma tabela

[!INCLUDE [sqlserver2016-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi-asa-pdw.md)]

Este tópico descreve como excluir colunas de tabelas no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)].

> [!CAUTION]
> Ao excluir uma coluna de uma tabela, ela e todos os dados que ela contém serão excluídos.

 **Neste tópico**

- **Antes de começar:**

   [Limitações e restrições](#Restrictions)

   [Segurança](#Security)

- **Para excluir uma coluna de uma tabela usando:**

   [SQL Server Management Studio](#SSMSProcedure)

   [Transact-SQL](#TsqlProcedure)

## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar

### <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitações e restrições

Você não pode excluir uma coluna que tenha uma restrição CHECK. Você deve excluir primeiramente a restrição.

Você não pode excluir uma coluna que tenha restrições PRIMARY KEY ou FOREIGN KEY ou outras dependências, exceto quando estiver usando o Designer de Tabela. No Pesquisador de Objetos ou no [!INCLUDE[tsql](../../includes/tsql-md.md)], você deve primeiramente remover todas as dependências da coluna.

### <a name="security"></a><a name="Security"></a> Segurança

#### <a name="permissions"></a><a name="Permissions"></a> Permissões

Exige a permissão ALTER na tabela.

## <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio

### <a name="to-delete-columns-by-using-object-explorer"></a>Para excluir colunas usando o Pesquisador de Objetos

1. No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].
2. No **Pesquisador de Objetos**, localize a tabela da qual você deseja excluir colunas e expanda para expor os nomes das colunas.
3. Clique com o botão direito do mouse na coluna que você quer excluir e escolha **Excluir**.
4. Na caixa de diálogo **Excluir Objeto** , clique em **OK**.

Se a coluna contiver restrições ou outras dependências, uma mensagem de erro será exibida na caixa de diálogo **Excluir Objeto** . Resolva o erro excluindo as restrições referenciadas.

### <a name="to-delete-columns-by-using-table-designer"></a>Para excluir colunas usando o Designer de Tabela

1. No **Pesquisador de Objetos**, clique com o botão direito do mouse na tabela da qual você deseja excluir colunas e selecione **Design**.
2. Clique com o botão direito do mouse na coluna que deseja excluir e escolha **Excluir Coluna** no menu de atalho.
3. Se a coluna participar de uma relação (FOREIGN KEY ou PRIMARY KEY), uma mensagem solicitará que você confirme a exclusão das colunas selecionadas e suas relações. Escolha **Sim**.

## <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL

### <a name="to-delete-columns"></a>Para excluir colunas

O exemplo a seguir mostra como excluir a coluna.

```sql
ALTER TABLE dbo.doc_exb DROP COLUMN column_b;
```

Se a coluna contiver restrições ou outras dependências, uma mensagem de erro será retornada. Resolva o erro excluindo as restrições referenciadas.

Para obter exemplos adicionais, consulte [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md).

## <a name="FollowUp"></a>
