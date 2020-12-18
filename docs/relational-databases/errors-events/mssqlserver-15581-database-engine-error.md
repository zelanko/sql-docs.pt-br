---
description: MSSQLSERVER_15581
title: MSSQLSERVER_15581
ms.custom: ''
ms.date: 09/03/2020
ms.prod: sql
ms.reviewer: ramakoni1, pijocoder, suresh-kandoth, Masha, VenCher
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 15581 (Database Engine error)
ms.assetid: ''
author: suresh-kandoth
ms.author: ramakoni
ms.openlocfilehash: f1221474d86d95400ca955d64b4a0812cffe1c0d
ms.sourcegitcommit: f87f2f0f1edc91fe400040d8e3a5810347aa8d70
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2020
ms.locfileid: "96868888"
---
# <a name="mssqlserver_15581"></a>MSSQLSERVER_15581
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

## <a name="details"></a>Detalhes

|Atributo|Valor|
|---|---|
|Nome do Produto|SQL Server|
|ID do evento|15581|
|Origem do Evento|MSSQLSERVER|
|Componente|SQLEngine|
|Nome simbólico|SEC_NODBMASTERKEYERR|
|Texto da mensagem|Crie uma chave mestra no banco de dados ou abra a chave mestra na sessão antes de executar esta operação.|
||

## <a name="explanation"></a>Explicação

O erro 15581 é gerado quando um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não é capaz de recuperar um banco de dados habilitado para TDE (transparent data encryption). Uma mensagem de erro semelhante à seguinte é registro no log de erros [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

> 2020-01-14 22:16:26.47 spid20s Erro: 15581, Gravidade: 16, Estado: 3.  
2020-01-14 22:16:26.47 spid20s Crie uma chave mestra no banco de dados ou abra a chave mestra na sessão antes de executar esta operação.

## <a name="possible-cause"></a>Causa possível

Esse problema ocorre quando a criptografia da chave mestra de serviço para a chave mestra do banco de dados no banco de dados mestre é removida quando o seguinte comando é executado:

```sql
Use master
go
alter master key drop encryption by service master key
```

A chave mestra de serviço é usada para criptografar o certificado usado pela chave mestra do banco de dados. Qualquer tentativa de usar o banco de dados habilitado para TDE requer acesso à chave mestra do banco de dados no banco de dados mestre. Uma chave mestra que não é criptografada pela chave mestra de serviço deve ser aberta usando a instrução [OPEN MASTER KEY (Transact-SQL)](/sql/t-sql/statements/open-master-key-transact-sql) com uma senha em cada sessão que requer acesso à chave mestra. Como esse comando não pode ser executado em sessões do sistema, a recuperação não pode ser concluída em bancos de dados habilitados para TDE.

## <a name="user-action"></a>Ação do usuário

Para resolver o problema, habilite a descriptografia automática da chave mestra. Para fazer isso, execute os seguintes comandos:

```sql
Use master
go
open master key DECRYPTION BY PASSWORD = 'password'
alter master key add encryption by service master key
```

Use a consulta a seguir para determinar se a descriptografia automática da chave mestra pela chave mestra de serviço foi desabilitada para o banco de dados mestre:

```sql
select is_master_key_encrypted_by_server from sys.databases where name = 'master'
```

Se essa consulta retornar um valor 0, a descriptografia automática da chave mestra pela chave mestra de serviço foi desabilitada.

## <a name="more-information"></a>Mais informações

Em alguns casos, a instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode parecer sem resposta. Se você consultar a exibição de gerenciamento dinâmico `sys.dm_exec_requests`, observará que o thread `LogWriter` e outros threads que estão executando operações DML estão aguardando indefinidamente com WRITELOG wait_type. Outras sessões também podem estar aguardando enquanto tentam obter bloqueios.
