---
description: MSSQLSERVER_3023
title: MSSQLSERVER_3023
ms.custom: ''
ms.date: 08/20/2020
ms.prod: sql
ms.reviewer: ramakoni1, pijocoder, suresh-kandoth, Masha
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 3023 (Database Engine error)
ms.assetid: ''
author: suresh-kandoth
ms.author: ramakoni
ms.openlocfilehash: 0197c7e5b75164615572e4041a5b348a4d5abcc4
ms.sourcegitcommit: ead0b8c334d487a07e41256ce5d6acafa2d23c9d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/22/2020
ms.locfileid: "92418652"
---
# <a name="mssqlserver_3023"></a>MSSQLSERVER_3023
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

## <a name="details"></a>Detalhes

|Atributo|Valor|
|---|---|
|Nome do Produto|SQL Server|
|ID do evento|3023|
|Origem do Evento|MSSQLSERVER|
|Componente|SQLEngine|
|Nome simbólico|DB_IN_USE_DUMP|
|Texto da mensagem|As operações de manipulação de arquivos e backup (como ALTER DATABASE ADD FILE) em um banco de dados precisam ser serializadas. Emita novamente a instrução após a conclusão da operação atual de backup ou de manipulação de arquivo|
||

## <a name="explanation"></a>Explicação

Você tenta executar um comando de backup, redução ou alteração de banco de dados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e recebe as seguintes mensagens:

> Mensagem 3023, Nível 16, Estado 2, Linha 1  
As operações de manipulação de arquivos e backup (como ALTER DATABASE ADD FILE) em um banco de dados precisam ser serializadas. Emita novamente a instrução após a conclusão da operação atual de backup ou de manipulação de arquivo.

> Mensagem 3013, Nível 16, Estado 1, Linha 1  
BACKUP DATABASE está sendo encerrado de forma anormal.

Além disso, o log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contém mensagens como as seguintes:

> \<Datetime> Erro de Backup: 3041, Gravidade: 16, Estado: 1.  
\<Datetime> Backup Falha do BACKUP em concluir o comando BACKUP DATABASE MyDatabase WITH DIFFERENTIAL. Verifique o log do aplicativo de backup para obter mensagens detalhadas.

Você também poderá observar que esses comandos recebem um `wait_type = LCK_M_U` e um `wait_resource = DATABASE: <id> [BULKOP_BACKUP_DB]` quando o status desses comandos é exibido nas várias DMVs (exibições de gerenciamento dinâmico), como em `sys.dm_exec_requests` ou `sys.dm_os_waiting_tasks`.

## <a name="possible-causes"></a>Possíveis causas

Há várias regras nas quais as operações são ou não permitidas quando um banco de dados completo está em andamento em um banco de dados. Alguns exemplos são os seguintes:

- Somente um backup de dados pode ocorrer por vez (quando ocorre um backup completo de banco de dados, backups diferenciais ou incrementais não podem ocorrer simultaneamente).
- Somente um backup de log pode ocorrer por vez (um backup de log é permitido quando um backup completo de banco de dados está ocorrendo).
- Não é possível adicionar nem remover arquivos em um banco de dados durante um backup.
- Não é possível reduzir arquivos durante os backups de banco de dados.
- Há alterações limitadas de modelo de recuperação permitidas durante os backups.

Quando uma dessas operações conflitantes forem executadas, os comandos receberão as esperas de bloqueio mencionadas na seção "Explicação" e, na sequência, você receberá as mensagens 3023 e 3041.

## <a name="user-action"></a>Ação do usuário

Examine os agendamentos das várias atividades de manutenção de banco de dados e ajuste-os para que essas operações ou esses comandos não entrem em conflito entre si.

## <a name="more-information"></a>Mais informações

O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] registra a hora de início e a hora de término do backup no banco de dados `msdb`. Examine o histórico de backup para determinar se um backup completo de banco de dados ocorreu durante a tentativa de um backup incremental e, portanto, foi a causa do erro. Use a seguinte consulta para ajudar você com esse processo:

```sql
select database_name, type, backup_start_date, backup_finish_date
from msdb.dbo.backupset
order by database_name, type, backup_start_date, backup_finish_date
go
```

Use também o evento **Mensagem de Erro do Usuário** no Rastreamento do SQL Profiler ou o evento **error_reported** nos Eventos Estendidos para acompanhar o relatório das mensagens 3023 no aplicativo que iniciou o backup ou outro comando de manutenção.
