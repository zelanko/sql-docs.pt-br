---
title: Criar uma chave mestra do banco de dados | Microsoft Docs
ms.custom: ''
ms.date: 09/12/2019
ms.prod: sql-server-2014
ms.reviewer: carlrab
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- database master key [SQL Server], creating
ms.assetid: 8cb24263-e97d-4e4d-9429-6cf494a4d5eb
author: aliceku
ms.author: aliceku
manager: craigg
ms.openlocfilehash: 757b6c62d63da2b8f1fa33e5d704d7a2c4fabd38
ms.sourcegitcommit: 5a61854ddcd2c61bb6da30ccad68f0ad90da0c96
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/13/2019
ms.locfileid: "70978374"
---
# <a name="create-a-database-master-key"></a>Criar uma chave mestra de banco de dados

Este tópico descreve como criar uma chave mestra de banco de dados `master` no usando [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] o [!INCLUDE[tsql](../../../includes/tsql-md.md)].

**Neste tópico**

- **Antes de começar:**

  [Segurança](#Security)

- [Para criar uma chave mestra do banco de dados usando o Transact-SQL](#TsqlProcedure)

## <a name="BeforeYouBegin"></a> Antes de começar

### <a name="Security"></a> Segurança

#### <a name="Permissions"></a> Permissões

Exige a permissão CONTROL no banco de dados.

## <a name="TsqlProcedure"></a> Usando o Transact-SQL

### <a name="to-create-a-database-master-key"></a>Criar uma chave mestra de banco de dados

1. Escolha uma senha por criptografar a cópia da chave mestra que será armazenada no banco de dados.
2. No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../../includes/ssde-md.md)].
3. Expanda **bancos de dados do sistema**, clique `master` com o botão direito do mouse e clique em **nova consulta**.
4. Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.

  ```sql
  -- Creates the master key.
  -- The key is encrypted using the password "23987hxJ#KL95234nl0zBe."
  CREATE MASTER KEY ENCRYPTION BY PASSWORD = '23987hxJ#KL95234nl0zBe';
```

Para obter mais informações, veja [CREATE MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-master-key-transact-sql).
