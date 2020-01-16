---
title: Configurar a pasta de instantâneo de replicação (portas não padrão)
titleSuffix: SQL Server on Linux
description: Saiba como configurar compartilhamentos de pasta de instantâneo com portas não padrão para a replicação do SQL Server em Linux.
ms.custom: seo-lt-2019
author: MikeRayMSFT
ms.author: mikerayW
ms.reviewer: vanto
ms.date: 09/24/2018
ms.topic: article
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: cb715e2a0a056c18352361b58ce8ffd67e3da78e
ms.sourcegitcommit: 035ad9197cb9799852ed705432740ad52e0a256d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/31/2019
ms.locfileid: "75558583"
---
# <a name="configure-replication-with-non-default-ports-sql-server-linux"></a>Configurar a replicação com portas não padrão (SQL Server Linux)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Você pode configurar a replicação com instâncias de SQL Server em Linux escutando em qualquer porta configurada com a configuração network.tcpport mssql-conf. A porta precisará ser acrescentada ao nome do servidor durante a configuração se as seguintes condições forem verdadeiras:

1. A configuração de replicação envolve uma instância do SQL Server em Linux
2. Qualquer instância (Windows ou Linux) está escutando em uma porta não padrão. 

O nome do servidor de uma instância pode ser encontrado executando @@servername nessa instância.

## <a name="examples"></a>Exemplos

'Server1' escuta na porta 1500 no Linux. Para configurar 'Server1' para distribuição, execute `sp_adddistributor` com `@distributor`. Por exemplo: 

```sql
exec sp_adddistributor @distributor = 'Server1,1500'
```

'Server1' escuta na porta 1500 no Linux. Para configurar um editor para o distribuidor, execute `sp_adddistpublisher` com `@publisher`. Por exemplo:

```sql
exec sp_adddistpublisher @publisher = 'Server1,1500' ,  ,  
```

"Server2" escuta na porta 6549 no Linux. Para configurar 'Server2' como um assinante, execute `sp_addsubscription` com `@subscriber`. Por exemplo:

```sql
exec sp_addsubscription @subscriber = 'Server2,6549' ,  ,  
```

'Server3' escuta na porta 6549 no Windows com o nome do servidor Server3 e o nome da instância MSSQL2017. Para configurar 'Server3' como um assinante, execute o `sp_addsubscription` com `@subscriber`. Por exemplo:

```sql
exec sp_addsubscription @subscriber = 'Server3/MSSQL2017,6549',  ,  
```

## <a name="next-steps"></a>Próximas etapas

[Conceitos: Replicação do SQL Server em Linux](sql-server-linux-replication.md)

[Procedimentos armazenados de replicação](../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md).

