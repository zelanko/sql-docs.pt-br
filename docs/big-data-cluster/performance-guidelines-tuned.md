---
title: Melhores práticas de desempenho para Clusters de Big Data do SQL Server
description: Este artigo fornece diretrizes e melhores práticas de desempenho para a execução de Clusters de Big Data do SQL Server em Kubernetes
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 06/30/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: abb5a73f472ccefa53517c54a3d403af82d0beb2
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85906227"
---
# <a name="performance-best-practices-and-configuration-guidelines-for-sql-server-big-data-clusters"></a>Melhores práticas de desempenho e diretrizes de configuração para Clusters de Big Data do SQL Server

[!INCLUDE [sqlserver2019](../includes/applies-to-version/sqlserver2019.md)]

Este artigo fornece melhores práticas e recomendações para maximizar o desempenho de aplicativos que têm como destino serviços em execução em um cluster de Big Data.

As diretrizes a seguir concentram-se nas recomendações para configurar o sistema operacional Linux que hospeda os nós de trabalho do Kubernetes em que o BDC será implantado. Como melhor prática, configure o perfil de ajuste antes de implantar o cluster de Big Data. As configurações incluídas no perfil de ajuste proposto foram validadas durante o estudo de caso realizado pela Microsoft e pela Intel. Os resultados do estudo estão publicados para download neste [white paper](https://aka.ms/sql-bdc-spark-perf/).

> [!TIP]
> Para conhecer as configurações de ajuste específicas do SQL Server em Linux, confira [Práticas recomendadas de desempenho e diretrizes de configuração do SQL Server em Linux](../linux/sql-server-linux-performance-best-practices.md). Além disso, outras melhores práticas, como o design de índices para bancos de dados do SQL Server, ainda se aplicam.

## <a name="proposed-linux-settings-using-a-tuned-mssql-bdc-profile"></a>Configurações do Linux propostas usando um perfil `mssql-bdc` ajustado

Crie um perfil de configuração **tuned.conf** com o conteúdo abaixo.

```bash
[main]
summary=Optimize for Microsoft SQL Server Big Data Clusters TPC-DS performance
include=throughput-performance
 
[sysctl]
#network tunings
net.ipv4.conf.default.rp_filter=1
net.ipv4.tcp_timestamps=0
net.ipv4.tcp_sack = 1
net.core.netdev_max_backlog = 25000
net.core.rmem_max = 2147483647
net.core.wmem_max = 2147483647
net.core.rmem_default = 33554431
net.core.wmem_default = 33554432
net.core.optmem_max = 33554432
net.ipv4.tcp_rmem =8192 33554432 2147483647
net.ipv4.tcp_wmem =8192 33554432 2147483647
net.ipv4.tcp_low_latency=1
net.ipv4.tcp_adv_win_scale=1
net.ipv6.conf.all.disable_ipv6 = 1
net.ipv6.conf.default.disable_ipv6 = 1
net.ipv4.conf.all.arp_filter=1
net.ipv4.tcp_retries2=5
net.ipv6.conf.lo.disable_ipv6 = 1
net.core.somaxconn = 65535
 
#memory cache settings
vm.swappiness=1
vm.overcommit_memory=0
vm.dirty_background_ratio=1
 
#kernel NUMA
kernel.numa_balancing=0

#filesystem
fs.aio-max-nr=1048576
 
[vm]
#should be revisited for SQL large pages use in master/data/compute pods
transparent_hugepages=never
```

## <a name="install-tuned-utility-on-all-the-kubernetes-worker-nodes"></a>Instalar o utilitário **tuned** ajustado em todos os nós de trabalho do Kubernetes

Para instalar o **tuned**, execute:

```bash
apt-get -y install tuned
```

## <a name="apply-tuning-settings-to-all-kubernetes-worker-nodes"></a>Aplicar configurações de ajuste a todos os nós de trabalho do Kubernetes

Em cada um dos nós de trabalho de destino, copie o arquivo **tuned.conf** criado acima:

```bash
cd /usr/lib/tuned
scp -r <sourcePath> ./mssql-bdc
```

Para habilitar esse perfil ajustado **mssql-bdc**, salve essas definições em um arquivo **tuned.conf** em uma pasta `/usr/lib/tuned/mssql-bdc` em todos os nós de trabalho do Kubernetes e habilite o perfil usando:

```bash
chmod +x /usr/lib/tuned/mssql-bdc/tuned.conf
tuned-adm profile mssql-bdc
```

Verifique se ele está habilitado usando este comando:

```bash
tuned-adm active
```

ou

```bash
tuned-adm list
```

Se o perfil for alterado dinamicamente, para que as novas alterações entrem em vigor, reinicie **tuned** em todos os nós de trabalho afetados:

```bash
systemctl restart tuned
```
 
Logs para o serviço **tuned** podem ser encontrados em */var/log/tuned/tuned.log*.

Opcionalmente, você pode configurar o perfil de ajuste em um nó no cluster do Kubernetes e usar o script abaixo para copiá-lo e configurá-lo nos nós restantes.

```bash
#!/bin/bash -e
# This script takes a list of servers (IPs like `cat ~administrator/workerhosts)) as input
# and update these servers with the local version of mssql-bdc tuned.conf.
 
is_root() {
    local is_root_set=0
    if [ "$EUID" -ne 0 ]; then
        echo "Please run as root"
    else
        is_root_set=1
    fi
    return "${is_root_set}"
}
 
# function main
if is_root -eq 0; then
    exit 0
fi
 
while [ $# -gt 0 ]
do
    # sometimes, people add non-breaking space characters to their *host* files.
    WORKER_IP=$(echo "$1" | sed -e 's/\xC2\xA0//g')
    echo -e "updating mssql-bdc tuned on \e[42m${WORKER_IP}\e[0m"
    # the following commands assume tuned was not set up and active...
    # TODO: add the tuned install and status checks
    ssh "${WORKER_IP}" mkdir -p /usr/lib/tuned/mssql-bdc
    scp ~administrator/tuned.conf "${WORKER_IP}":/usr/lib/tuned/mssql-bdc/tuned.conf
    ssh "${WORKER_IP}" tuned-adm profile mssql-bdc
    ssh "${WORKER_IP}" systemctl restart tuned
    ssh "${WORKER_IP}" tuned-adm active
    shift
done

```

## <a name="next-steps"></a>Próximas etapas

Para obter mais recursos, incluindo arquiteturas de referência para Clusters de Big Data do SQL Server, confira:

* [Estudo de caso: Cargas de trabalho do SQL em execução no Apache Spark no Cluster de Big Data do MS SQL Server 2019](https://aka.ms/sql-bdc-spark-perf/)

* [Arquitetura de referência do HPE para fornecer insights sobre todos os seus dados com Clusters de Big Data do Microsoft SQL Server 2019](https://h20195.www2.hpe.com/V2/GetDocument.aspx?docname=a50001963enw)

* [Dell EMC PowerStore: Clusters de Big Data do Microsoft SQL Server 2019](https://www.dellemc.com/resources/en-us/asset/white-papers/products/storage/h18231-dell-emc-powerstore-sql-server-big-data-clusters.pdf)

* [Clusters de Big Data do Microsoft SQL Server 2019: uma solução de Big Data usando a infraestrutura Dell EMC](https://infohub.delltechnologies.com/t/microsoft-sql-server-2019-big-data-clusters-a-big-data-solution-using-dell-emc-infrastructure/)

* [Arquitetura de referência dos Clusters de Big Data do Microsoft SQL Server 2019 no Cisco UCS](https://www.cisco.com/c/en/us/solutions/collateral/data-center-virtualization/unified-computing/sql-server-on-big-data-cluster-on-ucs.html)