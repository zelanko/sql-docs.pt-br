---
title: Como configurar a memória persistente (PMEM) para SQL Server no Linux | Microsoft Docs
description: Este artigo fornece um passo a passo para configurar PMEM no Linux.
author: DBArgenis
ms.author: argenisf
manager: craigg
ms.date: 09/24/2018
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 71c4af08573f54b5a33a95f0c821dfdb81b4f0a0
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47765580"
---
# <a name="how-to-configure-persistent-memory-pmem-for-sql-server-on-linux"></a>Como configurar a memória persistente (PMEM) para SQL Server no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este artigo descreve como configurar a memória persistente (PMEM) para SQL Server no Linux. Suporte PMEM no Linux foi introduzido no SQL Server de 2019 CTP 2.0.

## <a name="overview"></a>Visão geral

SQL Server 2016 introduziu o suporte para DIMMs não volátil, e uma otimização chamada [final do Log de armazenamento em cache no NVDIMM]( https://blogs.msdn.microsoft.com/bobsql/2016/11/08/how-it-works-it-just-runs-faster-non-volatile-memory-sql-server-tail-of-log-caching-on-nvdimm/) que reduziu a quantidade de operações necessárias para proteger um buffer de log para o armazenamento persistente. Isso aproveita a funcionalidade do Windows Server para acessar diretamente um dispositivo de memória persistente no modo DAX.

Visualização do SQL Server 2019 estende o suporte para memória persistente dispositivos (PMEM) para Linux, fornecendo iluminismo completo dos arquivos de log de transações e dados colocados em PMEM. Iluminismo refere-se para o método de acesso ao dispositivo de armazenamento usando operações de memcpy eficiente do espaço do usuário. Em vez de passar por arquivo sistema e armazenamento de pilha, do SQL Server utiliza o suporte DAX no Linux para colocar os dados diretamente em dispositivos, incorrendo em latência mínima.

## <a name="enable-enlightenment-of-database-files"></a>Habilitar iluminismo dos arquivos de banco de dados
Para habilitar iluminismo dos arquivos de banco de dados no SQL Server no Linux, siga as etapas a seguir:

1. Configurar os dispositivos no Linux, isso é feito usando o `ndctl` utilitário.

  - Instalar install `ndctl` Configurar dispositivo pmem. Você pode encontrá-lo [aqui](https://docs.pmem.io/getting-started-guide/installing-ndctl).
  - Use [ndctl] para criar um namespace.

  ```bash 
  ndctl create-namespace -f -e namespace0.0 --mode=fsdax* –map=mem
  ```

  >[!NOTE]
  >Se você estiver usando `ndctl` versão inferior a 59, use `--mode=memory`.

  Use `ndctl` para verificar se o namespace. Saída de exemplo a seguir:

```bash
ndctl list
[
  {
    "dev":"namespace0.0",
    "mode":"memory",
    "size":1099511627776,
    "blockdev":"pmem0",
    "numa_node":0
  }
]
```

  - Criar e montar o dispositivo pmem

    Por exemplo, com XFS

    ```bash
    mkfs.xfs -f /dev/pmem0
    mount –o dax,noatime /dev/pmem0 /mnt/dax
    xfs_io -c "extsize 2m" /mnt/dax
    ```

    Por exemplo, com EXT4

    ```bash
    mkfs.ext4 -b 4096 -E stride=512 -F /dev/pmem0
    mount –o dax,noatime /dev/pmem0 /mnt/dax
    ```

  Depois que o dispositivo foi configurado com ndctl, formatado e montado, você pode colocar arquivos de banco de dados nele. Você também pode criar um novo banco de dados 

1. Habilite iluminismo de arquivo de banco de dados do SQL Server usando o sinalizador de rastreamento 3979. Este sinalizador de rastreamento é um sinalizador de rastreamento de inicialização e como tal, precisa ser habilitado usando o utilitário mssql-conf.

1. Reinicie o SQL Server.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre o SQL Server no Linux, consulte [SQL Server no Linux](sql-server-linux-overview.md).
