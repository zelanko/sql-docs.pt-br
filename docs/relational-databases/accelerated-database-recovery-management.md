---
title: Recuperação de banco de dados acelerada | Microsoft Docs
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- accelerated database recovery [SQL Server], recovery-only
- database recovery [SQL Server]
author: mashamsft
ms.author: mathoma
ms.reviewer: kfarlee
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 8fea43ea41bc3e65fa0a6b36c7557322431e95fd
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "75245259"
---
# <a name="manage-accelerated-database-recovery"></a>Gerenciar recuperação acelerada de banco de dados

[!INCLUDE[tsql-appliesto-ss-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss-xxxx-xxxx-xxx-md.md)]

## <a name="enabling-and-controlling-adr"></a>Habilitar e controlar a ADR

A ADR está desativada por padrão no [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] e pode ser controlada usando a sintaxe DDL:
```sql
ALTER DATABASE [DB] SET ACCELERATED_DATABASE_RECOVERY = {ON | OFF}
[(PERSISTENT_VERSION_STORE_FILEGROUP = { filegroup name }) ];

```

Use essa sintaxe para controlar se o recurso está ativado ou desativado e atribua um grupo de arquivos específico para os dados do PVS *(repositório de versão persistente)* . Se nenhum grupo de arquivos for especificado, o PVS será armazenado no grupo de arquivos PRIMARY.

## <a name="managing-the-persistent-version-store-filegroup"></a>Gerenciar o grupo de arquivos de repositório de versão persistente
O recurso ADR baseia-se na existência das alterações com controle de versão, com versões diferentes de um elemento de dados mantidas no PVS.
Há considerações para localizar onde o PVS está localizado e como gerenciar o tamanho dos dados no PVS.

### <a name="to-enable-adr-without-specifying-a-filegroup"></a>Para habilitar a ADR sem especificar um grupo de arquivos

```sql
ALTER DATABASE [MyDatabase] SET ACCELERATED_DATABASE_RECOVERY = ON;
GO
```

Nesse caso, quando o grupo de arquivos de PVS não é especificado, o grupo de arquivos `PRIMARY` mantém os dados de PVS.

### <a name="to-enable-adr-and-specify-that-the-pvs-should-be-stored-in-the-versionstorefg-filegroup"></a>Para habilitar a ADR e especificar que o PVS deve ser armazenado no grupo de arquivos [VersionStoreFG]

Antes de executar esse script, crie o grupo de arquivos.

```sql
ALTER DATABASE [MyDatabase] SET ACCELERATED_DATABASE_RECOVERY = ON
(PERSISTENT_VERSION_STORE_FILEGROUP = [VersionStoreFG])
```

### <a name="to-disable-the-adr-feature"></a>Para desabilitar o recurso de ADR

```sql
ALTER DATABASE [MyDatabase] SET ACCELERATED_DATABASE_RECOVERY = OFF;
GO
```

Mesmo depois que o recurso ADR estiver desabilitado, haverá versões armazenadas no repositório de versão persistente que ainda serão necessárias para a reversão lógica do sistema.

### <a name="change-the-location-of-the-pvs-to-a-different-filegroup"></a>Alterar o local do PVS para um grupo de arquivos diferente

Talvez seja necessário mover o local do PVS para um grupo de arquivos diferente por vários motivos. Por exemplo, o PVS pode exigir mais espaço ou um armazenamento mais rápido.

Alterar o local do PVS é um processo de três etapas.

1. Desative o recurso de ADR.

   ```sql
   ALTER DATABASE [MyDatabase] SET ACCELERATED_DATABASE_RECOVERY = OFF;
   GO
   ```

2. Aguarde até que todas as versões armazenadas no PVS possam ser liberadas

   Para poder ativar a ADR com um novo local para o repositório de versão persistente, você deve primeiro verificar se todas as informações de versão foram limpas do local do PVS anterior. Para forçar essa limpeza a acontecer, execute o comando:

   ```sql
   EXEC sys.sp_persistent_version_cleanup [database name]
   ```

   O procedimento armazenado `sys.sp_persistent_version_cleanup` é síncrono, o que significa que ele não será concluído até que todas as informações de versão sejam limpas do PVS atual.  Após a conclusão, você pode verificar se as informações de versão são realmente removidas consultando o DMV `sys.dm_persistent_version_store_stats` e examinando o valor de `persistent_version_store_size_kb`.

   ```sql
   SELECT DB_Name(database_id), persistent_version_store_size_kb 
   FROM sys.dm_tran_persistent_version_store_stats where database_id = [MyDatabaseID]
   ```

   Quando o valor de persistent_version_store_size_kb é 0, você pode reabilitar o recurso de ADR, configurando o PVS para ficar localizado no novo grupo de arquivos.

1. Ativar a ADR especificando o novo local do PVS

   ```sql
   ALTER DATABASE [MyDatabase] SET ACCELERATED_DATABASE_RECOVERY = ON
   (PERSISTENT_VERSION_STORE_FILEGROUP = [VersionStoreFG])
   ```

## <a name="troubleshooting"></a>solução de problemas

Consulte `sys.dm_tran_persistent_version_store_stats` para verificar os tamanhos de PVS.

Verifique o tamanho de `% of DB`. Observe também a diferença do tamanho típico.

O PVS será considerado grande se for significativamente maior do que a linha de base ou se estiver perto de 50% do tamanho do banco de dados. 

1. Recupere `oldest_active_transaction_id` e verifique se essa transação esteve ativa por muito tempo, consultando `sys.dm_tran_database_transactions` com base na ID da transação.

   As transações ativas impedem a limpeza do PVS.

1. Se o banco de dados fizer parte de um grupo de disponibilidade, verifique o `secondary_low_water_mark`. Isso é o mesmo que o `low_water_mark_for_ghosts` relatado por `sys.dm_hadr_database_replica_states`. Consulte `sys.dm_hadr_database_replica_states` para ver se uma das réplicas contém esse valor por trás, pois isso também impedirá a limpeza do PVS.
1. Verifique `min_transaction_timestamp` (ou `online_index_min_transaction_timestamp` se o PVS online está se mantendo) e, com base nisso, verifique `sys.dm_tran_active_snapshot_database_transactions` para a coluna `transaction_sequence_num` para localizar a sessão que tem a transação de instantâneo antiga que contém a limpeza do PVS.
1. Se nenhuma das alternativas acima se aplica, isso significa que a limpeza está sendo impedida devido a transações anuladas. Verifique pela última vez o `aborted_version_cleaner_last_start_time` e o `aborted_version_cleaner_last_end_time` para ver se a limpeza da transação anulada foi concluída. O `oldest_aborted_transaction_id` deve ser movido para cima depois que a limpeza da transação anulada é concluída.
1. Se a transação anulada não foi concluída com êxito recentemente, verifique o log de erros em busca de mensagens relatando problemas de `VersionCleaner`.
