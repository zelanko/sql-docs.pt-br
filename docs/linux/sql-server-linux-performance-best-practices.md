---
title: "Práticas recomendadas de desempenho para o SQL Server no Linux | Microsoft Docs"
description: "Este tópico fornece diretrizes e práticas recomendadas de desempenho para a execução de 2017 do SQL Server no Linux."
author: rgward
ms.author: bobward
manager: jhubbard
ms.date: 09/14/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.workload: Inactive
ms.openlocfilehash: d6fb9839ee1ba7f583eca9445599422469212083
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="performance-best-practices-and-configuration-guidelines-for-sql-server-2017-on-linux"></a>Práticas recomendadas e diretrizes de configuração para 2017 do SQL Server no Linux

Este tópico fornece as práticas recomendadas e recomendações para maximizar o desempenho de aplicativos de banco de dados que se conectar ao SQL Server no Linux. Essas recomendações são específicas para execução na plataforma Linux. Todas as recomendações normais do SQL Server, como criação de índice, ainda se aplicam.

As diretrizes a seguir contém recomendações sobre como configurar o SQL Server e o sistema operacional Linux.

## <a name="sql-server-configuration"></a>Configuração do SQL Server

É recomendável executar as seguintes tarefas de configuração após a instalação do SQL Server no Linux para obter melhor desempenho de seu aplicativo.

### <a name="best-practices"></a>Práticas recomendadas

- **Usar a AFINIDADE de processo para o nó e/ou CPUs**

   É recomendável usar `ALTER SERVER CONFIGURATION` definir `PROCESS AFFINITY` para todos os **NUMANODEs** e/ou CPUs está usando para o SQL Server (que normalmente é para todos os nós e CPUs) em um sistema operacional Linux. Afinidade do processador ajuda a manter o comportamento eficiente do Linux e agendamento de SQL. Usando o **NUMANODE** opção é o método mais simples. Observe que você deve usar **a AFINIDADE do processo** mesmo se você tiver apenas um único nó em seu computador.  Consulte o [ALTER SERVER CONFIGURATION](../t-sql/statements/alter-server-configuration-transact-sql.md) documentação para obter mais detalhes sobre como definir **a AFINIDADE do processo**.

- **Configurar vários arquivos de dados tempdb**

   Como um SQL Server na instalação do Linux não oferece uma opção para configurar vários arquivos de tempdb, é recomendável que você considere criar tempdb vários arquivos de dados após a instalação. Para obter mais informações, consulte o guia do artigo, [recomendações para reduzir a contenção de alocação no banco de dados do SQL Server tempdb](https://support.microsoft.com/en-us/help/2154845/recommendations-to-reduce-allocation-contention-in-sql-server-tempdb-d).

### <a name="advanced-configuration"></a>Configuração avançada

As recomendações a seguir são parâmetros de configuração opcionais que você pode optar por executar após a instalação do SQL Server no Linux. Essas opções são com base nos requisitos da sua carga de trabalho e a configuração do seu sistema operacional Linux.

- **Definir um limite de memória com conf mssql**

   Para garantir que não há suficiente memória física livre para o sistema operacional Linux, o processo do SQL Server usa somente 80% da RAM física por padrão. Para alguns sistemas quais grande quantidade de RAM física, 20% pode ser um número significativo. Por exemplo, em um sistema com 1 TB de RAM, a configuração padrão deixaria cerca de 200 GB de RAM não utilizados. Nessa situação, você poderá configurar o limite de memória para um valor mais alto. Consulte a documentação sobre o **mssql conf** ferramenta e o [memory.memorylimitmb](sql-server-linux-configure-mssql-conf.md#memorylimit) definir que controla a memória visível para o SQL Server (em unidades de MB).

   Ao alterar essa configuração, tenha cuidado para não definir esse valor muito alto. Se você não deixar memória suficiente, você poderá experimentar problemas com o sistema operacional Linux e outros aplicativos do Linux.

## <a name="linux-os-configuration"></a>Configuração do sistema operacional do Linux

Considere usar as seguintes configurações do sistema operacional Linux com o melhor desempenho para uma instalação do SQL Server.

### <a name="kernel-settings-for-high-performance"></a>Configurações de kernel de alto desempenho

Esses são o desempenho relacionado ao alto de configurações de sistema operacional Linux recomendada e a taxa de transferência para uma instalação do SQL Server. Consulte a documentação do sistema operacional Linux para o processo definir essas configurações.



> [!Note]
> Para usuários do Red Hat Enterprise Linux (RHEL), o perfil de desempenho de taxa de transferência irá configurar essas configurações automaticamente (exceto estados C).

A tabela a seguir fornece recomendações para configurações de CPU:

| Configuração | Valor | Mais informações |
|---|---|---|
| Administrador de frequência de CPU | desempenho | Consulte o **cpupower** comando |
| ENERGY_PERF_BIAS | desempenho | Consulte o **x86_energy_perf_policy** comando |
| min_perf_pct | 100 | Consulte a documentação sobre intel p-estado |
| Estados de C | C1 somente | Consulte a documentação do Linux ou do sistema sobre como garantir estados C está definido como C1 somente |

A tabela a seguir fornece recomendações para configurações de disco:

| Configuração | Valor | Mais informações |
|---|---|---|
| leitura antecipada de disco | 4096 | Consulte o **blockdev** comando |
| configurações de sysctl | kernel.sched_min_granularity_ns = 10000000<br/>kernel.sched_wakeup_granularity_ns = 15000000<br/>VM.dirty_ratio = 40<br/>VM.dirty_background_ratio = 10<br/>VM.swappiness=10 | Consulte o **sysctl** comando |

### <a name="kernel-setting-auto-numa-balancing-for-multi-node-numa-systems"></a>Kernel configuração automática numa balanceamento para sistemas com vários nós NUMA

Se você instalar o SQL Server em um nó de vários **NUMA** sistemas, o seguinte **kernel.numa_balancing** kernel configuração é habilitada por padrão. Para permitir que o SQL Server para funcionar com eficiência máxima em uma **NUMA** sistema, desabilitar auto numa balanceamento em um sistema com vários nós NUMA:

```bash
sysctl -w kernel.numa_balancing=0
```

### <a name="kernel-settings-for-virtual-address-space"></a>Configurações de kernel para o espaço de endereço Virtual

A configuração padrão de **vm.max_map_count** (que é 65536) não pode ser alto o suficiente para uma instalação do SQL Server. Altere esse valor (que é um limite superior) para 256K.

```bash
sysctl -w vm.max_map_count 262144
```

### <a name="disable-last-accessed-datetime-on-file-systems-for-sql-server-data-and-log-files"></a>Desabilitar acessado pela última vez data/hora em sistemas de arquivos para arquivos de log e de dados do SQL Server

Use o **noatime** atributo com qualquer sistema de arquivos que é usado para armazenar dados do SQL Server e os arquivos de log. Consulte a documentação do Linux sobre como definir esse atributo.

### <a name="leave-transparent-huge-pages-thp-enabled"></a>Deixe transparente páginas (THP enorme) habilitada

A maioria das instalações do Linux deve ter essa opção em por padrão. É recomendável para a experiência de desempenho mais consistente deixar essa opção de configuração habilitada.

### <a name="swapfile"></a>arquivo de permuta

Certifique-se de que você tem um arquivo de permuta configurado corretamente para evitar quaisquer problemas de memória insuficiente. Consulte a documentação do Linux para criar e dimensionar corretamente um arquivo de permuta.

### <a name="virtual-machines-and-dynamic-memory"></a>Máquinas virtuais e a memória dinâmica

Se você estiver executando o SQL Server no Linux em uma máquina virtual, certifique-se de que selecionar opções para corrigir a quantidade de memória reservada para a máquina virtual. Não use recursos como memória dinâmica do Hyper-V.

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre os recursos do SQL Server que melhoram o desempenho, consulte [começar com recursos de desempenho](sql-server-linux-performance-get-started.md).

Para obter mais informações sobre o SQL Server no Linux, consulte [visão geral do SQL Server no Linux](sql-server-linux-overview.md).
