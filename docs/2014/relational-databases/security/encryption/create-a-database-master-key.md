---
title: Criar uma chave mestra do banco de dados | Microsoft Docs
ms.custom: ''
ms.date: 09/12/2019
ms.prod: sql-server-2014
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- database master key [SQL Server], creating
ms.assetid: 8cb24263-e97d-4e4d-9429-6cf494a4d5eb
author: jaszymas
ms.author: jaszymas
ms.reviewer: carlrab
ms.openlocfilehash: cb8305d9d5a3c72e6dffafd231f21110a5abdd14
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85055342"
---
# <a name="create-a-database-master-key"></a>Criar uma chave mestra de banco de dados

Este tópico descreve como criar uma chave mestra de banco de dados no usando o `master` [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] [!INCLUDE[tsql](../../../includes/tsql-md.md)] .

**Neste tópico**

- **Antes de começar:**

  [Segurança](#Security)

- [Para criar uma chave mestra do banco de dados usando o Transact-SQL](#TsqlProcedure)

## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar

### <a name="security"></a><a name="Security"></a> Segurança

#### <a name="permissions"></a><a name="Permissions"></a> Permissões

Exige a permissão CONTROL no banco de dados.

## <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL

### <a name="to-create-a-database-master-key"></a>Criar uma chave mestra de banco de dados

1. Escolha uma senha por criptografar a cópia da chave mestra que será armazenada no banco de dados.
2. No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../../includes/ssde-md.md)].
3. Expanda **Bancos de Dados do Sistema**, clique com o botão direito do mouse `master` e clique em **Nova Consulta**.
4. Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.

  ```sql
  -- Creates the master key.
  -- The key is encrypted using the password "23987hxJ#KL95234nl0zBe."
  CREATE MASTER KEY ENCRYPTION BY PASSWORD = '23987hxJ#KL95234nl0zBe';
```

Para obter mais informações, veja [CREATE MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-master-key-transact-sql).
