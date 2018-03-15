---
title: "Instruções | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, database-engine, pdw, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: d8d6f62a-e815-425c-a80e-a63fd34ec275
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: e6e36b056aaca063970c81d2932ec47ee7cef29e
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="transact-sql-statements"></a>instruções Transact-SQL
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

Este tópico de referência resume as categorias de instruções para uso com o Transact-SQL (T-SQL). Você pode encontrar todas as instruções listadas no painel de navegação esquerdo.

## <a name="backup-and-restore"></a>Backup e restauração
As instruções de backup e restauração oferecem maneiras de criar backups e fazer a restauração de backups.  Para obter mais informações, veja a [Visão geral de backup e restauração](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md).

## <a name="data-definition-language"></a>Linguagem de definição de dados
Instruções DDL (linguagem de definição de dados) definem as estruturas de dados. Use estas instruções para criar, alterar ou remover estruturas de dados em um banco de dados.
- ALTER
- Agrupamentos
- CREATE
- DROP
- DISABLE TRIGGER
- ENABLE TRIGGER
- RENAME
- UPDATE STATISTICS

## <a name="data-manipulation-language"></a>Linguagem de manipulação de dados
A DML (linguagem de manipulação de dados) afeta as informações armazenadas no banco de dados. Use estas instruções para inserir, atualizar e alterar as linhas no banco de dados.

- BULK INSERT
- Delete (excluir)
- INSERT
- MERGE
- TRUNCATE TABLE

## <a name="permissions-statements"></a>Instruções de permissões
Instruções de permissões determinam quais logons e usuários podem acessar os dados e executar operações. Para obter mais informações sobre o acesso e autenticação, veja a [Central de segurança](../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md).

## <a name="service-broker-statements"></a>Instruções do Service Broker
O Service Broker é um recurso que oferece suporte nativo para aplicativos de mensagens e enfileiramento. Para obter mais informações, veja [Service Broker](../../relational-databases/service-broker/event-notifications.md).

## <a name="session-settings"></a>Configurações da sessão
Instruções SET determinam como os identificadores de sessão atual lidam com configurações de tempo. Para obter uma visão geral, veja [instruções SET](set-statements-transact-sql.md).
