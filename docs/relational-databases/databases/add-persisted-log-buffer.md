---
title: Adicionar buffer de log persistente a um banco de dados
ms.custom: ''
ms.date: 10/30/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- PMEM
- persistent memory
- persisted log buffer
- add log file
- create log buffer
- remove log buffer
ms.assetid: 8ead516a-1334-4f40-84b2-509d0a8ffa45
author: briancarrig
ms.author: brcarrig
manager: amitban
ms.openlocfilehash: cc455ce62708f488224c4df6245f14eef8b2053d
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "76832227"
---
# <a name="add-persisted-log-buffer-to-a-database"></a>Adicionar buffer de log persistente a um banco de dados
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este tópico descreve como adicionar um buffer de log persistente a um banco de dados no [!INCLUDE[sqlv15](../../includes/sssqlv15-md.md)] usando [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
## <a name="permissions"></a>Permissões

Requer a permissão ALTER no banco de dados.  

## <a name="configure-persistent-memory-device-linux"></a>Configurar o dispositivo de memória persistente (Linux)

Para configurar um dispositivo de memória persistente no [Linux](../../linux/sql-server-linux-configure-pmem.md).

## <a name="configure-persistent-memory-device-windows"></a>Configurar o dispositivo de memória persistente (Windows)

Para configurar um dispositivo de memória persistente no [Windows](/windows-server/storage/storage-spaces/deploy-pmem/).
  
## <a name="add-a-persisted-log-buffer-to-a-database"></a>Adicionar um buffer de log persistente a um banco de dados  

Os exemplos a seguir adicionam um buffer de log persistente.

```sql
ALTER DATABASE <MyDB> 
  ADD LOG FILE 
  (
    NAME = <DAXlog>, 
    FILENAME = '<Filepath to DAX Log File>', 
    SIZE = 20MB
  );
```

O volume ou a montagem em que o novo arquivo de log é colocado deve ser formatado com DAX (NTFS) ou montado com a opção DAX (XFS/EXT4).

## <a name="remove-a-persisted-log-buffer"></a>Remover buffer de log persistente

Para remover com segurança um buffer de log persistente, o banco de dados deve ser colocado no modo de usuário único para drenar o buffer de log persistente.

Os locais de exemplo a seguir removem um buffer de log persistente.

```sql
ALTER DATABASE <MyDB> SET SINGLE_USER;
ALTER DATABASE <MyDB> REMOVE FILE <DAXlog>;
ALTER DATABASE <MyDB> SET MULTI_USER;
```

## <a name="limitations"></a>Limitações

O [TDE (Transparent Data Encryption)](../security/encryption/transparent-data-encryption.md) não é compatível com o buffer de log persistente.

Os [grupos de disponibilidade](../../t-sql/statements/create-availability-group-transact-sql.md) podem usar esse recurso apenas em réplicas secundárias devido à necessidade de semântica de gravação de log normal na primária. No entanto, o pequeno arquivo de log deve ser criado em todos os nós (idealmente em volumes ou montagens DAX).

## <a name="backup-and-restore-operations"></a>Operações de backup e restauração

As condições de restauração normais se aplicam. Se o buffer de log persistente for restaurado para um volume ou montagem DAX, ele continuará a funcionar, caso contrário, ele poderá ser removido com segurança.
  
## <a name="next-steps"></a>Próximas etapas

- [Como funciona (ele apenas é executado mais rapidamente): Final do cache de log do SQL Server de memória não volátil no NVDIMM](https://blogs.msdn.microsoft.com/bobsql/2016/11/08/how-it-works-it-just-runs-faster-non-volatile-memory-sql-server-tail-of-log-caching-on-nvdimm/)
- [Dados expostos: Latência e durabilidade com o SQL Server 2016](https://channel9.msdn.com/Shows/Data-Exposed/Latency-and-Durability-with-SQL-Server-2016)
- [Aceleração de latência de confirmação de transação usando a Memória de Classe de Armazenamento no Windows Server 2016/SQL Server 2016 SP1](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/12/02/transaction-commit-latency-acceleration-using-storage-class-memory-in-windows-server-2016sql-server-2016-sp1/)
