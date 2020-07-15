---
title: Criar uma chave mestra do banco de dados | Microsoft Docs
description: Crie uma chave mestra do banco de dados no SQL Server usando o Transact-SQL. Certifique-se de ter as permissões necessárias.
ms.custom: ''
ms.date: 09/12/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- database master key [SQL Server], creating
ms.assetid: 8cb24263-e97d-4e4d-9429-6cf494a4d5eb
author: jaszymas
ms.author: jaszymas
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 200f10a76629eb94e1e9fc1b3e1c29811d9e7f67
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86005575"
---
# <a name="create-a-database-master-key"></a>Criar uma chave mestra de banco de dados

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
Este tópico descreve como criar uma chave mestra de banco de dados no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando o [!INCLUDE[tsql](../../../includes/tsql-md.md)].

## <a name="security"></a>Segurança

### <a name="permissions"></a>Permissões

Exige a permissão CONTROL no banco de dados.

## <a name="using-transact-sql"></a>Usando o Transact-SQL

### <a name="to-create-a-database-master-key"></a>Criar uma chave mestra de banco de dados

1. Escolha uma senha por criptografar a cópia da chave mestra que será armazenada no banco de dados.
2. No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../../includes/ssde-md.md)].
3. Expanda **Bancos de Dados do Sistema**, clique com o botão direito do mouse `master` e clique em **Nova Consulta**.
4. Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.

   ```sql
     -- Creates the master key.
     -- The key is encrypted using the password "23987hxJ#KL95234nl0zBe".  
     CREATE MASTER KEY ENCRYPTION BY PASSWORD = '23987hxJ#KL95234nl0zBe';  

   ```

Para obter mais informações, veja [CREATE MASTER KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-master-key-transact-sql.md).
