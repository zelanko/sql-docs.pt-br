---
title: Configurar a memória persistente (PMEM)
description: Saiba como configurar a PMEM (memória persistente) para SQL Server em Linux e também como criar namespaces para dispositivos de PMEM.
ms.custom: seo-lt-2019
author: briancarrig
ms.author: brcarrig
ms.date: 10/31/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
monikerRange: '>= sql-server-linux-ver15  || >= sql-server-ver15'
ms.openlocfilehash: 4630a96f1abf961174ece179aabfd160a5784ad9
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97471607"
---
# <a name="configure-persistent-memory-pmem-for-sql-server-on-linux"></a>Configurar a PMEM (memória persistente) para o SQL Server em Linux

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

Este artigo descreve como configurar a memória persistente (PMEM) para [!INCLUDE[sqlv15](../includes/sssqlv15-md.md)] no Linux.

## <a name="overview"></a>Visão geral

[!INCLUDE[sqlv15](../includes/sssqlv15-md.md)] tem vários recursos na memória que usam memória persistente. Este documento aborda as etapas necessárias para configurar a memória persistente para SQL Server em Linux.

> [!NOTE]
> O termo _capacitação_ foi introduzido para transmitir o conceito de trabalhar com um sistema de arquivos com reconhecimento de memória persistente. O acesso direto ao sistema de arquivos de aplicativos de espaço do usuário é facilitado usando o mapeamento de memória (`mmap()`). Quando um mapeamento de memória para um arquivo é criado, o aplicativo pode emitir instruções de carregamento/armazenamento ignorando completamente a pilha de E/S. Isso é considerado um método de acesso de arquivo "capacitado" da perspectiva do aplicativo de extensão de host (que é o código de caixa preta que permite que o SQLPAL interaja com o sistema operacional Windows ou Linux).

## <a name="create-namespaces-for-pmem-devices"></a>Criar namespaces para dispositivos PMEM

### <a name="configure-the-devices"></a>Configurar os dispositivos

No Linux, use o utilitário `ndctl`.

- Instale `ndctl` para configurar o dispositivo PMEM. Você pode encontrá-lo [aqui](https://docs.pmem.io/getting-started-guide/installing-ndctl).
- Use `ndctl` para criar um namespace. Os namespaces são intercalados pelos NVDIMMs da PMEM e podem fornecer tipos diferentes de acesso ao espaço de usuário para regiões de memória no dispositivo. `fsdax` é o padrão e o modo desejado para SQL Server.

```bash 
ndctl create-namespace -f -e namespace0.0 --mode=fsdax* --map=dev
```

Observe que escolhemos o modo `fsdax` e estamos usando a memória do sistema para armazenar os metadados por página. É recomendável usar o `--map=dev`. Isso armazena os metadados diretamente no namespace. O armazenamento de metadados na memória usando `--map=mem` é considerado experimental no momento.

Use `ndctl` para verificar o namespace. 
  
Após a saída de exemplo, segue:

```bash
# ndctl list -N
{
  "dev":"namespace0.0",
  "mode":"fsdax",
  "map":"dev",
  "size":4294967296,
  "sector_size":512,
  "blockdev":"pmem0",
  "numa_node":0
}
```

### <a name="create-and-mount-pmem-device"></a>Criar e montar o dispositivo PMEM

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

## <a name="technical-considerations"></a>Considerações técnicas

- Bloquear a alocação de 2 MB para XFS/EXT4, conforme descrito acima
- O alinhamento incorreto entre alocação de bloco e `mmap` resulta em um fallback silencioso para 4 KB
- Os tamanhos de arquivo devem ser múltiplos de 2 MB (módulo 2 MB)
- Não desabilite THPs (páginas enormes transparentes) (habilitadas por padrão na maioria dos distribuições)

Depois que o dispositivo tiver sido configurado com `ndctl`, criado e montado, você poderá colocar arquivos de banco de dados nele ou criar um banco de dados.

Como o uso de O_DIRECT (E/S direta) é seguro nos dispositivos PMEM, é recomendável habilitar o sinalizador de rastreamento 3979 para desabilitar o mecanismo de liberação desabilitados. Para saber mais, confira o [Suporte do FUA](https://support.microsoft.com/help/4131496/enable-forced-flush-mechanism-in-sql-server-2017-on-linux). Os internos de acesso à unidade forçada são abordados aqui em [Elementos internos do FUA](/archive/blogs/bobsql/sql-server-on-linux-forced-unit-access-fua-internals).

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre o SQL Server em Linux, confira [SQL Server em Linux](sql-server-linux-overview.md).
Para encontrar melhores práticas de desempenho para o SQL Server em Linux, confira [Melhor prática de desempenho](sql-server-linux-performance-best-practices.md).