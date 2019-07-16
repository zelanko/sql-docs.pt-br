---
title: Como configurar a memória persistente (PMEM) para SQL Server no Linux
description: Este artigo fornece um passo a passo para configurar PMEM no Linux.
author: DBArgenis
ms.author: argenisf
ms.reviewer: vanto
ms.date: 11/06/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 4ed705b1b26193585a6278508ac98666d069418a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68077559"
---
# <a name="how-to-configure-persistent-memory-pmem-for-sql-server-on-linux"></a>Como configurar a memória persistente (PMEM) para SQL Server no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este artigo descreve como configurar a memória persistente (PMEM) para SQL Server no Linux. Suporte PMEM no Linux foi introduzido na versão prévia do SQL Server de 2019.

## <a name="overview"></a>Visão geral

SQL Server 2016 introduziu o suporte para DIMMs não volátil, e uma otimização chamada [final do Log de armazenamento em cache no NVDIMM]( https://blogs.msdn.microsoft.com/bobsql/2016/11/08/how-it-works-it-just-runs-faster-non-volatile-memory-sql-server-tail-of-log-caching-on-nvdimm/). Essas otimizações reduzimos o número de operações necessárias para proteger um buffer de log para o armazenamento persistente. Isso aproveita o acesso direto do Windows Server para um dispositivo de memória persistente no modo DAX.

Visualização do SQL Server 2019 estende o suporte para memória persistente dispositivos (PMEM) para Linux, fornecendo iluminismo completo dos arquivos de log de transações e dados colocados em PMEM. Iluminismo refere-se para o método de acesso ao dispositivo de armazenamento usando o espaço de usuário eficiente `memcpy()` operações. Em vez de contínuo por meio da pilha de armazenamento e sistema de arquivos, SQL Server aproveita o suporte DAX no Linux para colocar os dados diretamente em dispositivos, o que reduz a latência.

## <a name="enable-enlightenment-of-database-files"></a>Habilitar iluminismo dos arquivos de banco de dados
Para habilitar iluminismo dos arquivos de banco de dados no SQL Server no Linux, siga as etapas a seguir:

1. Configure os dispositivos.

  No Linux, use o `ndctl` utilitário.

  - Instalar `ndctl` Configurar dispositivo PMEM. Você pode encontrá-lo [aqui](https://docs.pmem.io/getting-started-guide/installing-ndctl).
  - Use [ndctl] para criar um namespace.

  ```bash 
  ndctl create-namespace -f -e namespace0.0 --mode=fsdax* --map=mem
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

  - Criar e montar o dispositivo PMEM

    Por exemplo, com XFS

    ```bash
    mkfs.xfs -f /dev/pmem0
    mount -o dax,noatime /dev/pmem0 /mnt/dax
    xfs_io -c "extsize 2m" /mnt/dax
    ```

    Por exemplo, com EXT4

    ```bash
    mkfs.ext4 -b 4096 -E stride=512 -F /dev/pmem0
    mount -o dax,noatime /dev/pmem0 /mnt/dax
    ```

  Depois que o dispositivo foi configurado com ndctl, formatado e montado, você pode colocar arquivos de banco de dados nele. Você também pode criar um novo banco de dados 

1. Como os dispositivos PMEM são O_DIRECT seguro, habilite o sinalizador de rastreamento 3979 para desabilitar o mecanismo de liberação forçado. Este sinalizador de rastreamento é um sinalizador de rastreamento de inicialização e como tal, precisa ser habilitado usando o utilitário mssql-conf. Observe que essa é uma alteração de configuração do servidor, e você não deve usar este sinalizador de rastreamento se você tiver quaisquer dispositivos sem conformidade O_DIRECT que precisam o mecanismo de liberação forçado para garantir a integridade dos dados. Para obter mais informações, consulte https://support.microsoft.com/en-us/help/4131496/enable-forced-flush-mechanism-in-sql-server-2017-on-linux

1. Reinicie o SQL Server.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre o SQL Server no Linux, consulte [SQL Server no Linux](sql-server-linux-overview.md).
