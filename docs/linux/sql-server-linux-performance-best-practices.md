---
title: Melhores práticas de desempenho para SQL Server em Linux
description: Este artigo fornece diretrizes e melhores práticas de desempenho para a execução do SQL Server em Linux.
author: tejasaks
ms.author: tejasaks
ms.reviewer: vanto
ms.date: 09/14/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 548ab73e97b9bccb6a64a95b7294d3d5ca63493d
ms.sourcegitcommit: 867b7c61ecfa5616e553410ba0eac06dbce1fed3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/22/2020
ms.locfileid: "77558340"
---
# <a name="performance-best-practices-and-configuration-guidelines-for-sql-server-on-linux"></a>Melhores práticas de desempenho e diretrizes de configuração para o SQL Server em Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este artigo fornece práticas recomendadas e recomendações para maximizar o desempenho de aplicativos de banco de dados que se conectam ao SQL Server em Linux. Estas recomendações são específicas para a execução na plataforma Linux. Todas as recomendações normais para o SQL Server, tais como design de índice, ainda se aplicam.

As diretrizes a seguir contêm recomendações para configurar o SQL Server e o sistema operacional Linux.

## <a name="sql-server-configuration"></a>Configuração do SQL Server

É recomendável executar as tarefas de configuração a seguir depois de instalar o SQL Server em Linux para obter o melhor desempenho para o aplicativo.

### <a name="best-practices"></a>Práticas recomendadas

- **Usar afinidade do processador para nó e/ou CPUs**

   É recomendável usar `ALTER SERVER CONFIGURATION` para definir `PROCESS AFFINITY` para todos os **NUMANODEs** e/ou CPUs que você está usando para o SQL Server (que normalmente é para todos os nós e CPUs) em um sistema operacional Linux. A afinidade do processador ajuda a manter eficiente o comportamento do agendamento do Linux e do SQL. O uso da opção **NUMANODE** é o método mais simples. Observe que você deve usar a **afinidade de processo** mesmo que você tenha apenas um único nó NUMA no computador.  Consulte a documentação [Alterar a configuração do servidor](../t-sql/statements/alter-server-configuration-transact-sql.md) para obter mais informações sobre como definir a **afinidade de processo**.

- **Configurar vários arquivos de dados tempdb**

   Já que uma instalação do SQL Server em Linux não oferece uma opção para configurar vários arquivos tempdb, recomendamos que você considere criar vários arquivos de dados tempdb após a instalação. Para obter mais informações, confira as diretrizes no artigo [Recomendações para reduzir a contenção de alocação no banco de dados tempdb do SQL Server](https://support.microsoft.com/help/2154845/recommendations-to-reduce-allocation-contention-in-sql-server-tempdb-d).

### <a name="advanced-configuration"></a>Configuração avançada

As recomendações a seguir são definições de configuração opcionais que você pode optar por executar após a instalação do SQL Server em Linux. Essas opções se baseiam nos requisitos de carga de trabalho e na configuração do sistema operacional Linux.

- **Definir um limite de memória com mssql-conf**

   Para garantir que haja memória física livre suficiente para o sistema operacional Linux, o processo de SQL Server usa apenas 80% da RAM física por padrão. Para alguns sistemas que têm grande quantidade de RAM física, 20% pode ser um número significativo. Por exemplo, em um sistema com 1 TB de RAM, a configuração padrão deixaria cerca de 200 GB de RAM não usada. Nessa situação, talvez você queira configurar o limite de memória para um valor mais alto. Consulte a documentação sobre a ferramenta **mssql-conf** e a configuração [memory.memorylimitmb](sql-server-linux-configure-mssql-conf.md#memorylimit) que controla a memória visível para o SQL Server (em unidades de MB).

   Ao alterar essa configuração, tenha cuidado para não definir esse valor muito alto. Se você não deixar memória suficiente, poderá ter problemas com o sistema operacional Linux e outros aplicativos do Linux.

## <a name="linux-os-configuration"></a>Configuração do sistema operacional Linux

Considere o uso das seguintes definições de configuração do sistema operacional Linux para experimentar o melhor desempenho para uma instalação do SQL Server.

### <a name="kernel-settings-for-high-performance"></a>Configurações de kernel para alto desempenho
Essas são as configurações recomendadas do sistema operacional Linux relacionadas ao alto desempenho e à taxa de transferência para uma instalação do SQL Server. Confira a documentação do sistema operacional Linux para obter o processo de definição dessas configurações.



> [!Note]
> Para usuários do RHEL (Red Hat Enterprise Linux), o perfil de desempenho de taxa de transferência [tuned](https://tuned-project.org) define essas configurações automaticamente (exceto para C-States). Do RHEL 8.0 em diante, um perfil mssql interno /usr/lib/tuned era codesenvolvido com a Red Hat e oferece ajustes mais refinados relacionados a desempenho do Linux para cargas de trabalho do SQL Server. Esse perfil inclui o perfil de desempenho de taxa de transferência do RHEL e apresentamos as definições dele abaixo para sua análise com outras distribuições do Linux e versões do RHEL sem esse perfil.

A tabela a seguir fornece recomendações para as configurações de CPU:

| Configuração | Valor | Mais informações |
|---|---|---|
| Administrador de frequência de CPU | desempenho | Confira o comando **cpupower** |
| ENERGY_PERF_BIAS | desempenho | Confira o comando **x86_energy_perf_policy** |
| min_perf_pct | 100 | Confira a documentação sobre o Intel p-state |
| C-States | Somente C1 | Confira a documentação do Linux ou do sistema sobre como garantir que os C-States sejam definidos apenas como C1 |

A tabela a seguir fornece recomendações para as configurações de disco:

| Configuração | Valor | Mais informações |
|---|---|---|
| leitura antecipada de disco | 4096 | Confira o comando **blockdev** |
| configurações de sysctl | kernel.sched_min_granularity_ns = 10000000<br/>kernel.sched_wakeup_granularity_ns = 15000000<br/>vm.dirty_ratio = 40<br/>vm.dirty_background_ratio = 10<br/>vm.swappiness = 10 | Confira o comando **sysctl** |

### <a name="kernel-setting-auto-numa-balancing-for-multi-node-numa-systems"></a>Configuração do kernel para balanceamento automático NUMA de vários nós para sistemas NUMA

Se você instalar o SQL Server em um sistema **NUMA** de vários nós, a configuração de kernel **kernel.numa_balancing** a seguir será habilitada por padrão. Para permitir que o SQL Server opere com eficiência máxima em um sistema **NUMA**, desabilite o balanceamento automático NUMA em um sistema NUMA de vários nós:

```bash
sysctl -w kernel.numa_balancing=0
```

### <a name="kernel-settings-for-virtual-address-space"></a>Configurações de kernel para espaço de endereço virtual

A configuração padrão de **vm.max_map_count** (que é 65536) pode não ser alta o suficiente para uma instalação do SQL Server. Altere esse valor (que é um limite superior) para 256K.

```bash
sysctl -w vm.max_map_count=262144
```

### <a name="proposed-linux-settings-using-a-tuned-mssql-profile"></a>Configurações do Linux propostas usando um perfil mssql ajustado

```bash
#
# A tuned configuration for SQL Server on Linux
#
    
[main]
summary=Optimize for Microsoft SQL Server
include=throughput-performance
    
[cpu]
force_latency=5

[sysctl]
vm.swappiness = 1
vm.dirty_background_ratio = 3
vm.dirty_ratio = 80
vm.dirty_expire_centisecs = 500
vm.dirty_writeback_centisecs = 100
vm.transparent_hugepages=always
# For , use
# vm.transparent_hugepages=madvice
vm.max_map_count=1600000
net.core.rmem_default = 262144
net.core.rmem_max = 4194304
net.core.wmem_default = 262144
net.core.wmem_max = 1048576
kernel.numa_balancing=0
kernel.sched_latency_ns = 60000000
kernel.sched_migration_cost_ns = 500000
kernel.sched_min_granularity_ns = 15000000
kernel.sched_wakeup_granularity_ns = 2000000
```

Para habilitar esse perfil ajustado, salve essas definições em um arquivo **tuned.conf** em uma pasta/usr/lib/tuned/MSSQL e habilite o perfil usando

```bash
chmod +x /usr/lib/tuned/mssql/tuned.conf
tuned-adm profile mssql
```

Verifique a habilitação dele com

```bash
tuned-adm active
```
ou
```bash
tuned-adm list
```

### <a name="disable-last-accessed-datetime-on-file-systems-for-sql-server-data-and-log-files"></a>Desabilitar data/hora do último acesso em sistemas de arquivos para arquivos de log e dados do SQL Server

Use o atributo **noatime** com qualquer sistema de arquivos usado para armazenar arquivos de log e dados do SQL Server. Confira a documentação do Linux sobre como definir esse atributo.

### <a name="leave-transparent-huge-pages-thp-enabled"></a>Deixar THP (páginas enormes transparentes) habilitadas

A maioria das instalações do Linux deve ter essa opção ativada por padrão. Para a experiência de desempenho mais consistente, recomendamos deixar essa opção de configuração habilitada. No entanto, em caso de atividade de paginação de alta memória em implantações do SQL Server com várias instâncias, por exemplo, ou de execução do SQL Server com outros aplicativos que demandam memória no servidor, sugerimos que você teste o desempenho dos aplicativos após executar o comando a seguir 

```bash
echo madvice > /sys/kernel/mm/transparent_hugepage/enabled
```
ou modificar o perfil tuned mssql com a linha

```bash
vm.transparent_hugepages=madvice
```
e torne o perfil mssql ativo após a modificação
```bash
tuned-adm off
tuned-amd profile mssql
```

### <a name="swapfile"></a>swapfile

Verifique se você tem um swapfile configurado corretamente para evitar quaisquer problemas de memória insuficiente. Consulte a documentação do Linux para saber como criar e dimensionar corretamente um swapfile.

### <a name="virtual-machines-and-dynamic-memory"></a>Máquinas virtuais e memória dinâmica

Se você está executando o SQL Server em Linux em uma máquina virtual, verifique se você selecionou as opções para corrigir a quantidade de memória reservada para a máquina virtual. Não use recursos como a Memória Dinâmica Hyper-V.

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre recursos do SQL Server que melhoram o desempenho, confira [Introdução aos recursos de desempenho](sql-server-linux-performance-get-started.md).

Para saber mais sobre o SQL Server em Linux, confira [Visão geral do SQL Server em Linux](sql-server-linux-overview.md).
