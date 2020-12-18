---
title: Melhores práticas de desempenho para SQL Server em Linux
description: Este artigo fornece diretrizes e melhores práticas de desempenho para a execução do SQL Server em Linux.
author: tejasaks
ms.author: tejasaks
ms.reviewer: vanto
ms.date: 12/11/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 89b8a7c087fb87ed911be640126ec81021b045a7
ms.sourcegitcommit: 2991ad5324601c8618739915aec9b184a8a49c74
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2020
ms.locfileid: "97323253"
---
# <a name="performance-best-practices-and-configuration-guidelines-for-sql-server-on-linux"></a>Melhores práticas de desempenho e diretrizes de configuração para o SQL Server em Linux

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

Este artigo fornece práticas recomendadas e recomendações para maximizar o desempenho de aplicativos de banco de dados que se conectam ao SQL Server em Linux. Estas recomendações são específicas para a execução na plataforma Linux. Todas as recomendações normais para o SQL Server, tais como design de índice, ainda se aplicam.

As diretrizes a seguir contêm recomendações para configurar o SQL Server e o SO (sistema operacional) Linux.

## <a name="linux-os-configuration"></a>Configuração do sistema operacional Linux

Considere o uso das seguintes definições de configuração do SO Linux para experimentar o melhor desempenho para uma instalação do SQL Server.

### <a name="storage-configuration-recommendation"></a>Recomendação de configuração de armazenamento

#### <a name="use-storage-subsystem-with-appropriate-iops-throughput-and-redundancy"></a>Use o subsistema de armazenamento com IOPS, taxa de transferência e redundância apropriados

O subsistema de armazenamento que hospeda dados, logs de transações e outros arquivos associados (como arquivos de ponto de verificação para OLTP in-memory) deve ser capaz de gerenciar as cargas de trabalho média e de pico normalmente. Normalmente, em ambientes locais, o fornecedor de armazenamento dá suporte à configuração de RAID de hardware apropriada com distribuição para vários discos para garantir a IOPS, a taxa de transferência e a redundância apropriados. No entanto, isso pode variar de acordo com diferentes fornecedores de armazenamento e diferentes ofertas de armazenamento com arquiteturas variadas.

Para o SQL Server em Linux implantado nas Máquinas Virtuais do Azure, considere o uso de RAID de software para garantir que os requisitos de taxa de transferência e IOPS apropriados sejam atingidos. Consulte o seguinte artigo ao configurar o SQL Server em máquinas virtuais do Azure para ver considerações de armazenamento semelhantes: [Configuração de armazenamento para VMs do SQL Server](https://docs.microsoft.com/azure/azure-sql/virtual-machines/windows/storage-configuration)

Veja a seguir um exemplo de como criar um RAID de software no Linux nas Máquinas Virtuais do Azure. Um exemplo é fornecido abaixo, mas use o número apropriado de discos de dados para a taxa de transferência e a IOPS necessários para volumes com base nos requisitos de dados, log de transações e E/S de tempdb. Neste exemplo, oito discos de dados foram anexados à Máquina Virtual do Azure; 4 para hospedar arquivos de dados, 2 para logs de transações e 2 para cargas de trabalho de tempdb.

```bash
# To locate the devices (for example /dev/sdc) for RAID creation, use the lsblk command
# For Data volume, using 4 devices, in RAID 5 configuration with 8KB stripes
mdadm --create --verbose /dev/md0 --level=raid5 --chunk=8K --raid-devices=4 /dev/sdc /dev/sdd /dev/sde /dev/sdf

# For Log volume, using 2 devices in RAID 10 configuration with 64KB stripes
mdadm --create --verbose /dev/md1 --level=raid10 --chunk=64K --raid-devices=2 /dev/sdg /dev/sdh

# For tempdb volume, using 2 devices in RAID 0 configuration with 64KB stripes
mdadm --create --verbose /dev/md2 --level=raid0 --chunk=64K --raid-devices=2 /dev/sdi /dev/sdj
```

#### <a name="file-system-configuration-recommendation"></a>Recomendação de configuração de sistema de arquivos

O SQL Server dá suporte a sistemas de arquivos EXT4 e XFS para hospedar o banco de dados, os logs de transações e arquivos adicionais, como arquivos de ponto de verificação para OLTP in-memory no SQL Server. A Microsoft recomenda usar o sistema de arquivos XFS para hospedar os dados de SQL Server e os arquivos de log de transações.

```bash
# Formatting the volume with XFS filesystem
mkfs.xfs /dev/md0 -f -L datavolume
mkfs.xfs /dev/md1 -f -L logvolume
mkfs.xfs /dev/md2 -f -L tempdb
```

> [!NOTE]
> É possível configurar o sistema de arquivos XFS para não diferenciar maiúsculas de minúsculas ao criar e formatar o volume XFS. Essa não é a configuração frequentemente usada no ecossistema de Linux, mas pode ser usada para fins de compatibilidade.
>
> Exemplo: mkfs.xfs /dev/md0 -f -n version=ci -L datavolume
>
> No exemplo, os parâmetros `-n version=ci` são usados para configurar o sistema de arquivos XFS de maneira a não diferenciar maiúsculas de minúsculas.

##### <a name="persistent-memory-filesystem-recommendation"></a>Recomendação de sistema de arquivos de memória persistente

Para a configuração do sistema de arquivos em dispositivos de memória persistente, a alocação de bloco para o sistema de arquivos subjacente deve ser de 2 MB. Para saber mais sobre este tópico, confira o artigo [Considerações técnicas](sql-server-linux-configure-pmem.md#technical-considerations).

#### <a name="disable-last-accessed-datetime-on-file-systems-for-sql-server-data-and-log-files"></a>Desabilitar data/hora do último acesso em sistemas de arquivos para arquivos de log e dados do SQL Server

Para garantir que a unidade anexada ao sistema seja remontada automaticamente após uma reinicialização, ela deve ser adicionada ao arquivo `/etc/fstab`. Além disso, é altamente recomendável que o UUID (Identificador Universal Exclusivo) seja usado no `/etc/fstab` para fazer referência à unidade e não apenas ao nome do dispositivo (por exemplo, `/dev/sdc1`).

É altamente recomendável usar o atributo **noatime** com qualquer sistema de arquivos usado para armazenar arquivos de log e dados do SQL Server. Confira a documentação do Linux sobre como definir esse atributo. Veja abaixo um exemplo de como habilitar a opção **noatime** para um volume montado na Máquina Virtual do Azure.

A entrada do ponto de montagem em **_/etc/fstab_* _

```bash
UUID="xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx" /data1 xfs,rw,attr2,noatime 0 0
```

No exemplo acima, a UUID representa o dispositivo que você pode encontrar usando o comando _*_blkid_*_.

#### <a name="sql-server-and-forced-unit-access-fua-io-subsystem-capability"></a>Recurso de subsistema de E/S de FUA (Acesso forçado à unidade) e SQL Server

Há certas versões de distribuições do Linux com suporte que dão suporte ao recurso de subsistema de E/S de FUA para fornecer durabilidade de dados. O SQL Server usa a funcionalidade FUA para fornecer E/S altamente eficiente e confiável para cargas de trabalho do SQL Server. Para saber mais sobre o suporte do FUA pela distribuição de Linux e seu impacto para o SQL Server, leia o seguinte blog: [SQL Server em Linux: Elementos internos de FUA (Acesso forçado à unidade)](https://bobsql.com/sql-server-on-linux-forced-unit-access-fua-internals/)

O SUSE Linux Enterprise Server 12 SP5 e o Red Hat Enterprise Linux 8.0 em diante dão suporte ao recurso de FUA no subsistema de E/S. Se você estiver usando o SQL Server 2017 CU6 e superior ou o SQL Server 2019, use a configuração a seguir para uma implementação de E/S eficiente e de alto desempenho com FUA pelo SQL Server.

Use a configuração recomendada listada abaixo se as condições a seguir forem atendidas.

- Usando SQL Server 2017 CU6 ou mais recente ou o SQL Server 2019
- Usando uma distribuição e uma versão do Linux que dão suporte ao recurso de FUA (Red Hat Enterprise Linux 8.0 ou superior ou o SUSE Linux Enterprise Server 12 SP5)
- Hardware e/ou subsistema de armazenamento que dá suporte e está configurado para o recurso de FUA

Configuração recomendada:

1. Habilitar o sinalizador de rastreamento 3979 como um parâmetro de inicialização
2. Use _ *MSSQL-conf** para configurar `control.writethrough = 1` e `control.alternatewritethrough = 0`

Para quase todas as outras configurações que não atendem às condições anteriores, a configuração recomendada é a seguinte:

1. Habilite o sinalizador de rastreamento 3982 como um parâmetro de inicialização (que é o padrão para o SQL Server no ecossistema do Linux), enquanto garante que o sinalizador de rastreamento 3979 não está habilitado como um parâmetro de inicialização
2. Use **mssql-conf** para configurar `control.writethrough = 1` e `control.alternatewritethrough = 1`

### <a name="kernel-and-cpu-settings-for-high-performance"></a>Configurações de kernel e CPU para alto desempenho

A seção a seguir descreve as configurações recomendadas do SO Linux relacionadas ao alto desempenho e à taxa de transferência para uma instalação do SQL Server. Confira a documentação do SO Linux para ver o processo de definição dessas configurações. O uso de [**_Tuned_* _](https://tuned-project.org) conforme descrito ajuda a configurar várias CPUs e configurações de kernel descritas abaixo.

#### <a name="using-__tuned__-to-configure-kernel-settings"></a>Usando _*_Tuned_*_ para definir as configurações do kernel

Para usuários do RHEL (Red Hat Enterprise Linux), o perfil de desempenho de taxa de transferência [Tuned](https://tuned-project.org) define algumas configurações de kernel e CPU automaticamente (exceto para C-States). Do RHEL 8.0 em diante, um perfil _*_Tuned_*_ chamado _ *mssql* foi codesenvolvido com a Red Hat e oferece ajustes mais refinados relacionados a desempenho do Linux para cargas de trabalho do SQL Server. Esse perfil inclui o perfil de desempenho de taxa de transferência do RHEL e apresentamos as definições dele abaixo para sua análise com outras distribuições do Linux e versões do RHEL sem esse perfil.

Para o SUSE Linux Enterprise Server 12 SP5, o Ubuntu 18.04 e o Red Hat Enterprise Linux 7.x, o pacote **_Tuned_ *_ pode ser instalado manualmente. Ele pode ser usado para criar e configurar o perfil _* mssql** conforme descrito abaixo.

##### <a name="proposed-linux-settings-using-a-tuned-mssql-profile"></a>Configurações do Linux propostas usando o perfil mssql Tuned

```bash
#
# A Tuned configuration for SQL Server on Linux
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
# For multi-instance SQL deployments, use
# vm.transparent_hugepages=madvise
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

Para habilitar esse perfil Tuned, salve essas definições em um arquivo **tuned.conf** em uma `/usr/lib/tuned/mssql` e habilite o perfil usando os seguintes comandos:

```bash
chmod +x /usr/lib/tuned/mssql/tuned.conf
tuned-adm profile mssql
```

Verifique se ele está habilitado com o seguinte comando:

```bash
tuned-adm active
```

ou

```bash
tuned-adm list
```

#### <a name="cpu-settings-recommendation"></a>Recomendação de configurações de CPU

A tabela a seguir fornece recomendações para as configurações de CPU:

| Configuração | Valor | Mais informações |
|---|---|---|
| Administrador de frequência de CPU | desempenho | Confira o comando **cpupower** |
| ENERGY_PERF_BIAS | desempenho | Confira o comando **x86_energy_perf_policy** |
| min_perf_pct | 100 | Confira a documentação sobre o Intel p-state |
| C-States | Somente C1 | Confira a documentação do Linux ou do sistema sobre como garantir que os C-States sejam definidos apenas como C1 |

Usando **_Tuned_ *_ conforme descrito anteriormente configura automaticamente as configurações do administrador de frequência da CPU, de ENERGY_PERF_BIAS e de min_perf_pct adequadamente porque o perfil de desempenho de produtividade é usado como base para o perfil _* mssql**. O parâmetro C-States deve ser configurado manualmente de acordo com a documentação fornecida pelo Linux ou pelo distribuidor do sistema.

#### <a name="disk-settings-recommendations"></a>Recomendações de configurações de disco

A tabela a seguir fornece recomendações para as configurações de disco:

| Configuração | Valor | Mais informações |
|---|---|---|
| disco `readahead` | 4096 | Confira o comando `blockdev` |
| configurações de sysctl | kernel.sched_min_granularity_ns = 10000000<br/>kernel.sched_wakeup_granularity_ns = 15000000<br/>vm.dirty_ratio = 40<br/>vm.dirty_background_ratio = 10<br/>vm.swappiness = 1 | Confira o comando **sysctl** |

**Descrição:**

- **vm.swappiness**: Esse parâmetro controla o peso relativo fornecido para alternar a memória de runtime limitando o kernel para alternar páginas de memória do processo do SQL Server.

- **vm.dirty_\** _: Os acessos de gravação de arquivo do SQL Server não são armazenados em cache, atendendo aos seus requisitos de integridade de dados. Esses parâmetros permitem um desempenho de gravação assíncrona eficiente e reduzem o impacto de E/S de armazenamento das gravações de cache do Linux, permitindo um cache grande o suficiente enquanto limita a liberação.

- _*kernel.sched_\**_: Esses valores de parâmetro representam a recomendação atual para ajustar o algoritmo de CFS (Completely Fair Scheduling) no Kernel do Linux para melhorar a taxa de transferência de chamadas de E/S de rede e armazenamento com relação à preempção e à retomada de threads entre processos.

O uso do perfil de _*mssql** **_Tuned_*_ define as configurações _*vm.swappiness**, **vm.dirty_\* *_ e _* kernel.sched_\**_. A configuração `readahead` do disco usando o comando `blockdev` é feita por dispositivo e deve ser executada manualmente.

#### <a name="kernel-setting-auto-numa-balancing-for-multi-node-numa-systems"></a>Configuração do kernel para balanceamento automático NUMA de vários nós para sistemas NUMA

Se você instalar o SQL Server em um sistema _ *NUMA** de vários nós, a configuração de kernel **kernel.numa_balancing** a seguir será habilitada por padrão. Para permitir que o SQL Server opere com eficiência máxima em um sistema **NUMA**, desabilite o balanceamento automático NUMA em um sistema NUMA de vários nós:

```bash
sysctl -w kernel.numa_balancing=0
```

O uso do perfil do **mssql** **_Tuned_ *_ configura a opção _* kernel.numa_balancing**.

#### <a name="kernel-settings-for-virtual-address-space"></a>Configurações de kernel para espaço de endereço virtual

A configuração padrão de **vm.max_map_count** (que é 65536) pode não ser alta o suficiente para uma instalação do SQL Server. Por esse motivo, altere o valor de **vm.max_map_count** para, no mínimo, 262144 em uma implantação do SQL Server e confira a seção [Configurações propostas do Linux usando um perfil MSSQL Tuned](#proposed-linux-settings-using-a-tuned-mssql-profile) para obter ajustes adicionais para esses parâmetros de kernel. O valor máximo para vm.max_map_count é 2147483647.

```bash
sysctl -w vm.max_map_count=1600000
```

O uso do perfil do **mssql** **_Tuned_ *_ configura a opção _* vm.max_map_count**.

#### <a name="leave-transparent-huge-pages-thp-enabled"></a>Deixar THP (páginas enormes transparentes) habilitadas

A maioria das instalações do Linux deve ter essa opção ativada por padrão. Para a experiência de desempenho mais consistente, recomendamos deixar essa opção de configuração habilitada. No entanto, se houver atividade de paginação de alta memória em implantações do SQL Server com várias instâncias, por exemplo, ou de execução do SQL Server com outros aplicativos que demandam memória no servidor, sugerimos que você teste o desempenho dos aplicativos após executar o comando a seguir:

```bash
echo madvise > /sys/kernel/mm/transparent_hugepage/enabled
```

Ou modifique o perfil do **mssql** **_Tuned_* _ com a linha:

```bash
vm.transparent_hugepages=madvise
```

E torne o perfil _ *mssql** ativo após a modificação:

```bash
tuned-adm off
tuned-adm profile mssql
```

O uso do perfil do **mssql** **_Tuned_ *_ configura a opção _* transparent_hugepage**.

#### <a name="additional-advanced-kernelos-configuration"></a>Configuração avançada adicional de kernel/SO

1. Para obter o melhor desempenho de E/S de armazenamento, recomenda-se o uso do agendamento de multifila do Linux para dispositivos de bloco. Isso permite que o desempenho da camada de bloco seja bem dimensionado com SSDs (unidades de estado sólido) rápidas e sistemas de vários núcleos. Confira na documentação se ela estiver habilitada por padrão em suas distribuições do Linux. Na maioria dos outros casos, inicializar o kernel com **scsi_mod.use_blk_mq=y** a habilita, embora a documentação da distribuição do Linux em uso possa ter orientações adicionais. Isso é consistente com o kernel do Linux upstream.

1. Como a E/S de vários caminhos geralmente é usada para implantações do SQL Server, o destino de vários caminhos do DM (mapeador de dispositivos) também deve ser configurado para usar a infraestrutura `blk-mq` habilitando a opção de inicialização de kernel **dm_mod.use_blk_mq=y**. O valor padrão é `n` (desabilitado). Essa configuração, quando dispositivos SCSI subjacentes estão usando `blk-mq`, reduz a sobrecarga de bloqueio na camada de DM. Consulte a documentação da distribuição Linux em uso para ver diretrizes adicionais sobre como configurá-la.

#### <a name="configure-swapfile"></a>Configurar o arquivo de permuta

Verifique se você tem um swapfile configurado corretamente para evitar quaisquer problemas de memória insuficiente. Consulte a documentação do Linux para saber como criar e dimensionar corretamente um swapfile.

#### <a name="virtual-machines-and-dynamic-memory"></a>Máquinas virtuais e memória dinâmica

Se você está executando o SQL Server em Linux em uma máquina virtual, verifique se você selecionou as opções para corrigir a quantidade de memória reservada para a máquina virtual. Não use recursos como a Memória Dinâmica Hyper-V.

## <a name="sql-server-configuration"></a>Configuração do SQL Server

É recomendável executar as tarefas de configuração a seguir depois de instalar o SQL Server em Linux para obter o melhor desempenho para o aplicativo.

### <a name="best-practices"></a>Práticas recomendadas

- **Usar afinidade do processador para nó e/ou CPUs**

   É recomendável usar `ALTER SERVER CONFIGURATION` para definir `PROCESS AFFINITY` para todos os **NUMANODEs** e/ou CPUs que você está usando para o SQL Server (que normalmente é para todos os nós e CPUs) em um SO Linux. A afinidade do processador ajuda a manter eficiente o comportamento do agendamento do Linux e do SQL. O uso da opção **NUMANODE** é o método mais simples. Use **PROCESS AFFINITY** mesmo que você tenha apenas um único nó NUMA no computador. Para obter mais informações sobre como definir **PROCESS AFFINITY**, confira o artigo [ALTER SERVER CONFIGURATION](../t-sql/statements/alter-server-configuration-transact-sql.md).

- **Configurar vários arquivos de dados tempdb**

   Já que uma instalação do SQL Server em Linux não oferece uma opção para configurar vários arquivos tempdb, recomendamos que você considere criar vários arquivos de dados tempdb após a instalação. Para obter mais informações, confira as diretrizes no artigo [Recomendações para reduzir a contenção de alocação no banco de dados tempdb do SQL Server](https://support.microsoft.com/help/2154845/recommendations-to-reduce-allocation-contention-in-sql-server-tempdb-d).

### <a name="advanced-configuration"></a>Configuração avançada

As recomendações a seguir são definições de configuração opcionais que você pode optar por executar após a instalação do SQL Server em Linux. Essas opções se baseiam nos requisitos de carga de trabalho e na configuração do SO Linux.

- **Definir um limite de memória com mssql-conf**

   Para garantir que haja memória física livre suficiente para o SO Linux, o processo de SQL Server usa apenas 80% da RAM física por padrão. Para alguns sistemas que têm grande quantidade de RAM física, 20% pode ser um número significativo. Por exemplo, em um sistema com 1 TB de RAM, a configuração padrão deixaria cerca de 200 GB de RAM não usada. Nessa situação, talvez você queira configurar o limite de memória para um valor mais alto. Consulte a documentação sobre a ferramenta **mssql-conf** e a configuração [memory.memorylimitmb](sql-server-linux-configure-mssql-conf.md#memorylimit) que controla a memória visível para o SQL Server (em unidades de MB).

   Ao alterar essa configuração, tenha cuidado para não definir esse valor muito alto. Se você não tiver memória suficiente, poderá ter problemas com o SO Linux e outros aplicativos do Linux.

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre recursos do SQL Server que melhoram o desempenho, confira [Introdução aos recursos de desempenho](sql-server-linux-performance-get-started.md).

Para saber mais sobre o SQL Server em Linux, confira [Visão geral do SQL Server em Linux](sql-server-linux-overview.md).
