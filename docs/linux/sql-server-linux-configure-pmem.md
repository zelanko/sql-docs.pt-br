---
title: Como configurar a PMEM (memória persistente) para SQL Server em Linux
description: Este artigo fornece um passo a passo para configurar o PMEM no Linux.
author: briancarrig
ms.author: brcarrig
ms.reviewer: vanto
ms.date: 11/06/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
monikerRange: '>= sql-server-linux-ver15  || >= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 6f9a5d8c6b2db65bd237f0a3a267638a8cc16b68
ms.sourcegitcommit: 071065bc5433163ebfda4fdf6576349f9d195663
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/03/2019
ms.locfileid: "71923825"
---
# <a name="how-to-configure-persistent-memory-pmem-for-sql-server-on-linux"></a>Como configurar a PMEM (memória persistente) para SQL Server em Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este artigo descreve como configurar a PMEM (memória persistente) para SQL Server em Linux. O suporte a PMEM no Linux foi introduzido na versão prévia do SQL Server 2019.

## <a name="overview"></a>Visão geral

O SQL Server 2016 introduziu o suporte para DIMMs não voláteis e uma otimização chamada [Parte final do cache de log no NVDIMM]( https://blogs.msdn.microsoft.com/bobsql/2016/11/08/how-it-works-it-just-runs-faster-non-volatile-memory-sql-server-tail-of-log-caching-on-nvdimm/). Essas otimizações reduziram o número de operações necessárias para proteger um buffer de log para o armazenamento persistente. Isso se beneficia do acesso direto do Windows Server a um dispositivo de memória persistente no modo DAX.

A versão prévia do SQL Server 2019 estende o suporte para dispositivos PMEM (Memória Persistente) ao Linux, fornecendo capacitação completa de arquivos de log de transações e de dados colocados na PMEM. O esclarecimento refere-se ao método de acesso ao dispositivo de armazenamento usando operações `memcpy()` de espaço de usuário eficientes. Em vez de passar pelo sistema de arquivos e pela pilha de armazenamento, o SQL Server se beneficia do suporte a DAX no Linux para posicionar dados diretamente em dispositivos, o que reduz a latência.

## <a name="enable-enlightenment-of-database-files"></a>Habilitar a capacitação dos arquivos de banco de dados
Para habilitar o esclarecimento dos arquivos de banco de dados no SQL Server em Linux, siga as seguintes etapas:

1. Configure os dispositivos.

  No Linux, use o utilitário `ndctl`.

  - Instale `ndctl` para configurar o dispositivo PMEM. Você pode encontrá-lo [aqui](https://docs.pmem.io/getting-started-guide/installing-ndctl).
  - Use [ndctl] para criar um namespace.

  ```bash 
  ndctl create-namespace -f -e namespace0.0 --mode=fsdax* --map=mem
  ```

  >[!NOTE]
  >Se você estiver usando uma versão de `ndctl` inferior a 59, use `--mode=memory`.

  Use `ndctl` para verificar o namespace. Após a saída de exemplo, segue:

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

  Depois que o dispositivo tiver sido configurado com ndctl, formatado e montado, você poderá colocar arquivos de banco de dados nele. Também é possível criar um banco de dados 

1. Já que o uso de O_DIRECT é seguro nos dispositivos PMEM, habilite o sinalizador de rastreamento 3979 para desabilitar o mecanismo de liberação forçada. Esse sinalizador de rastreamento é de inicialização e, como tal, precisa ser habilitado usando o utilitário mssql-conf. Observe que essa é uma alteração de configuração de todo o servidor e você não deverá usar esse sinalizador de rastreamento se tiver qualquer dispositivo em não conformidade com O_DIRECT que precise do mecanismo de liberação forçada para assegurar a integridade dos dados. Para obter mais informações, confira https://support.microsoft.com/en-us/help/4131496/enable-forced-flush-mechanism-in-sql-server-2017-on-linux

1. Reinicie o SQL Server.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre o SQL Server em Linux, confira [SQL Server em Linux](sql-server-linux-overview.md).
