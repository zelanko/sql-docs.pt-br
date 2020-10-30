---
description: MSSQLSERVER_
title: MSSQLSERVER_4214
ms.custom: ''
ms.date: 08/20/2020
ms.prod: sql
ms.reviewer: ramakoni1, pijocoder, suresh-kandoth, Masha
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 4214 (Database Engine error)
ms.assetid: ''
author: suresh-kandoth
ms.author: ramakoni
ms.openlocfilehash: 0a04ec00e94dca9a4d940a3b0182123f0716d472
ms.sourcegitcommit: ead0b8c334d487a07e41256ce5d6acafa2d23c9d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/22/2020
ms.locfileid: "92418665"
---
# <a name="mssqlserver_4214"></a>MSSQLSERVER_4214
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

## <a name="details"></a>Detalhes

|Atributo|Valor|
|---|---|
|Nome do Produto|SQL Server|
|ID do evento|4214|
|Origem do Evento|MSSQLSERVER|
|Componente|SQLEngine|
|Nome simbólico|DMPX_NODBBACKUP|
|Texto da mensagem|BACKUP LOG não pode ser executado porque não há um backup de banco de dados atual|
||

## <a name="explanation"></a>Explicação

O erro é gerado quando você tenta fazer um backup de log de transações antes de fazer um backup completo de um banco de dados. Antes de tentar fazer backup do log de transações para um banco de dados, você precisará fazer um backup completo de banco de dados. Além disso, você receberá a seguinte mensagem no log de erros:

> \<Datetime> Erro de backup: 3041, Gravidade: 16, Estado: 1.  
\<Datetime> Backup Falha de BACKUP em concluir o comando BACKUP LOG \<db_name>. Verifique o log do aplicativo de backup para obter mensagens detalhadas.

## <a name="user-action"></a>Ação do usuário

Execute um backup completo de banco de dados antes de tentar fazer backup do log de transações de um banco de dados.

## <a name="more-information"></a>Mais informações

Para obter mais informações, confira: [Backup e restauração de bancos de dados do SQL Server](/sql/relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases).