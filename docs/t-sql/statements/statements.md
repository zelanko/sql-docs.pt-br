---
title: Instruções | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, database-engine, pdw, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: d8d6f62a-e815-425c-a80e-a63fd34ec275
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 43d4405411005ab43e3f2b2fe9b2136a5793e8a5
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68099968"
---
# <a name="transact-sql-statements"></a>instruções Transact-SQL
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Este tópico de referência resume as categorias de instruções para uso com o Transact-SQL (T-SQL). Você pode encontrar todas as instruções listadas no painel de navegação esquerdo.

## <a name="backup-and-restore"></a>Backup e restauração
As instruções de backup e restauração oferecem maneiras de criar backups e fazer a restauração de backups.  Para obter mais informações, veja a [Visão geral de backup e restauração](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md).

## <a name="data-definition-language"></a>Linguagem de definição de dados
Instruções DDL (linguagem de definição de dados) definem as estruturas de dados. Use estas instruções para criar, alterar ou remover estruturas de dados em um banco de dados.
- ALTER
- Ordenações
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
- UPDATE
- MESCLAR
- TRUNCATE TABLE

## <a name="permissions-statements"></a>Instruções de permissões
Instruções de permissões determinam quais logons e usuários podem acessar os dados e executar operações. Para obter mais informações sobre o acesso e autenticação, veja a [Central de segurança](../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md).

## <a name="service-broker-statements"></a>Instruções do Service Broker
O Service Broker é um recurso que oferece suporte nativo para aplicativos de mensagens e enfileiramento. Para obter mais informações, veja [Service Broker](../../relational-databases/service-broker/event-notifications.md).

## <a name="session-settings"></a>Configurações da sessão
Instruções SET determinam como os identificadores de sessão atual lidam com configurações de tempo. Para obter uma visão geral, veja [instruções SET](set-statements-transact-sql.md).
