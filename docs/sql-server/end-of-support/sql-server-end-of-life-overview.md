---
title: Opções de fim do suporte
description: Conheça as diferentes opções disponíveis para os produtos do SQL Server que atingiram o fim do suporte, como SQL Server 2005, SQL Server 2008 e SQL Server 2008 R2.
ms.date: 12/18/2019
ms.prod: sql
ms.technology: install
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: pmasl
monikerRange: =sql-server-previousversions||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: d3143a586c54f0c908e80ca9e78041c9f1996931
ms.sourcegitcommit: 768f046107642f72693514f51bf2cbd00f58f58a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2020
ms.locfileid: "87112107"
---
# <a name="sql-server-end-of-support-options"></a>Opções de fim do suporte do SQL Server 
[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]

Este artigo explica as opções para lidar com produtos do SQL Server que atingiram o fim do suporte.

## <a name="understanding-the-sql-server-lifecycle"></a>Noções básicas sobre o ciclo de vida do SQL Server

Cada versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é apoiada por um mínimo de 10 anos de suporte, que inclui cinco anos de suporte base e cinco anos de suporte estendido:
-  O **suporte base** inclui atualizações funcionais, de desempenho, de escalabilidade e de segurança. 
-  O **suporte estendido** inclui apenas atualizações de segurança. 

O **fim do suporte** (às vezes conhecido como fim da vida útil) indica que um produto atingiu o final do respectivo ciclo de vida e que o serviço e o suporte não estão mais disponíveis para o produto. Para obter mais informações sobre o Ciclo de Vida da Microsoft, confira [Política do Ciclo de Vida da Microsoft](https://support.microsoft.com/hub/4095338/microsoft-lifecycle-policy).



## <a name="options"></a>Opções

Depois que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] atingir o fim do suporte, você poderá optar por:
- Fazer a atualização para uma versão atual do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
- Comprar uma [assinatura de Atualizações de Segurança Estendida](https://www.microsoft.com/cloud-platform/extended-security-updates). 
- Migrar sua carga de trabalho para uma Máquina Virtual do Azure no estado em que se encontra para [Atualizações de Segurança Estendidas gratuitas](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-2008-eos-extend-support).
- Migrar sua carga de trabalho para um [serviço do Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-paas-vs-sql-server-iaas). 

Para obter mais informações, diretrizes e ferramentas para planejar e automatizar a migração ou a atualização, confira [Fim do suporte do SQL Server 2005](https://www.microsoft.com/sql-server/sql-server-2005) e [Fim do suporte do SQL Server 2008](https://www.microsoft.com/cloud-platform/windows-sql-server-2008).  

![Opções de fim do suporte](media/sql-server-end-of-life-overview/sql-server-upgrade-paths.png)

Este artigo descreve os benefícios e as considerações de cada abordagem, bem como recursos adicionais que podem ajudar a orientar seu processo de tomada de decisão.

## <a name="upgrade-sql-server"></a>Atualizar o SQL Server

Depois que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] atingir o fim do suporte, você poderá optar por fazer a atualização para uma versão mais recente e com suporte do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Isso fornece consistência ambiental, permite que você use o conjunto de recursos mais recente e adote o ciclo de vida de suporte da nova versão.

### <a name="benefits"></a>Benefícios
- **Tecnologia mais recente**: As novas versões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] apresentam inovações que incluem recursos de desempenho, escalabilidade e alta disponibilidade, bem como segurança aprimorada. 
- **Controle**: você tem o máximo de controle sobre os recursos e a escalabilidade, porque você gerencia tanto o hardware quanto o software.
- **Ambiente conhecido**: se você estiver fazendo a atualização de uma versão antiga do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], esse será o ambiente mais semelhante.
- **Extensa aplicabilidade**: aplicável aos aplicativos de banco de dados de qualquer tipo, incluindo sistemas OLTP e data warehouse.
- **Baixo risco para aplicativos de banco de dados**: ao manter a compatibilidade do banco de dados com o mesmo nível do sistema herdado, os aplicativos de banco de dados existentes ficam protegidos contra alterações funcionais e de desempenho que podem ter efeitos prejudiciais. Um aplicativo só precisa ter uma nova certificação completa quando precisa usar recursos que são restritos por uma configuração de compatibilidade de banco de dados mais recente. Para saber mais, confira [Certificação de Compatibilidade](../../database-engine/install-windows/compatibility-certification.md).

### <a name="considerations"></a>Considerações

- **Custo**: essa abordagem exige o maior investimento inicial e o gerenciamento mais contínuo. Você precisa comprar, manter e gerenciar o próprio hardware e software.
- **Tempo de inatividade**: pode haver algum tempo de inatividade, dependendo da sua estratégia de atualização. Também há um risco inerente de enfrentar problemas durante um processo de atualização in-loco.
- **Complexidade**: se você estiver usando o Windows Server 2008 ou o [!INCLUDE[winserver2008r2-md](../../includes/winserver2008r2-md.md)], também precisará atualizar o sistema operacional, pois as versões mais recentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podem não ter suporte nessas versões do Windows. Há um risco adicional durante o processo de atualização do sistema operacional e, portanto, fazer uma migração lado a lado pode ser a abordagem mais prudente, porém, a mais cara. Não há suporte para atualizações do sistema operacional in-loco em instâncias de cluster de failover do Windows Server 2008 ou [!INCLUDE[winserver2008r2-md](../../includes/winserver2008r2-md.md)]. 

  > [!NOTE]
  > As atualizações sem interrupção do sistema operacional do cluster estão disponíveis no Windows Server 2016 em diante.

### <a name="resources"></a>Recursos

[Mídia de instalação](https://www.microsoft.com/evalcenter/evaluate-sql-server-2017-rtm)   
[Atualizar o SQL Server usando o Assistente de Instalação](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)

Novidades do:
- [SQL Server 2016](../what-s-new-in-sql-server-2016.md)
- [SQL Server 2017](../what-s-new-in-sql-server-2017.md) 
- [SQL Server 2019](../what-s-new-in-sql-server-ver15.md)   

Requisitos de hardware:
- [SQL Server 2017 e anterior](../install/hardware-and-software-requirements-for-installing-sql-server.md)  
- [SQL Server 2019](../install/hardware-and-software-requirements-for-installing-sql-server-ver15.md)    

Atualizações de versão e edição compatíveis:
- [SQL Server 2016](../../database-engine/install-windows/supported-version-and-edition-upgrades.md?view=sql-server-2016) 
- [SQL Server 2017](../../database-engine/install-windows/supported-version-and-edition-upgrades-2017.md)
- [SQL Server 2019](../../database-engine/install-windows/supported-version-and-edition-upgrades-version-15.md)

Ferramentas:
-  O [Assistente para Experimentos de Banco de Dados](../../dea/database-experimentation-assistant-overview.md) pode ajudar a avaliar a versão de destino do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para uma carga de trabalho específica. 
-  O [Assistente de Migração de Dados](../../dma/dma-overview.md) pode ajudar a detectar problemas de compatibilidade que possam afetar a funcionalidade do banco de dados na nova versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 
-  O [Assistente de Ajuste de Consulta](../../relational-databases/performance/upgrade-dbcompat-using-qta.md) pode ajudar a ajustar cargas de trabalho que possam ter efeitos adversos ao atualizar a compatibilidade do banco de dados.

A seguinte imagem fornece um exemplo de inovação nas várias versões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao longo dos anos: 

![25 anos de inovação do SQL Server](media/sql-server-end-of-life-overview/sql-server-version-improvements.png)

## <a name="extend-support"></a>Estender o suporte 

Caso não esteja pronto para a atualização e a migração para a nuvem, você terá a capacidade de comprar uma assinatura de Atualizações de Segurança Estendida para receber atualizações de segurança **Críticas** por até três anos após o fim da data de suporte.  

### <a name="benefits"></a>Benefícios 

- **Suporte a aplicativos**: essa será a melhor opção se o aplicativo exigir uma nova certificação em uma versão mais recente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Isso é comum para os aplicativos que não estão usando a [Certificação de Compatibilidade](../../database-engine/install-windows/compatibility-certification.md). 
- **Infraestrutura consistente**: você não precisa alterar sua infraestrutura de nenhuma forma. 
- **Suporte técnico**: se você tiver o Software Assurance ou outro plano de suporte, poderá continuar recebendo suporte técnico do [!INCLUDE[msCoName](../../includes/msconame-md.md)] no produto do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de fim do suporte. Essa é a única maneira de obter suporte para o [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)] e o [!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)]. 
- **Time**: essa opção está disponível por três anos, proporcionando a você um tempo extra para certificar seus aplicativos. 

### <a name="considerations"></a>Considerações 

- **Disponibilidade limitada**: essa opção só está disponível para os clientes com licenças de assinatura ou do Software Assurance. 
- **Custo**: essa opção pode ser cara, pois as Atualizações de Segurança Estendida são aproximadamente 75% do custo de licença local anualmente.
- **Período limitado**: essa opção só está disponível por três anos e, portanto, você ainda precisará fazer a atualização ou a migração no final do período de três anos se quiser garantir a segurança e a conformidade.
- **Sem correções de bug**: se você encontrar um bug não relacionado à segurança no produto, a [!INCLUDE[msCoName](../../includes/msconame-md.md)] não lançará uma correção para ele. 
- **Suporte limitado**: as Atualizações de Segurança Estendida não incluem novos recursos, aprimoramentos funcionais nem correções solicitadas pelo cliente. As correções de segurança são limitadas àquelas classificadas como Críticas pelo [MSRC (Microsoft Security Response Center)](https://portal.msrc.microsoft.com/).

### <a name="resources"></a>Recursos

[Visão geral do ESU (Atualizações de Segurança Estendida)](sql-server-extended-security-updates.md)       
[Perguntas frequentes detalhadas sobre o ESU](https://www.microsoft.com/cloud-platform/extended-security-updates)       
[Estender o suporte gratuitamente com a migração no estado em que se encontram para uma VM do Azure](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-2008-eos-extend-support)       
[Software Assurance](https://www.microsoft.com/licensing/licensing-programs/software-assurance-default)       

## <a name="azure-virtual-machine"></a>Máquina Virtual do Azure

Outra opção é migrar a sua carga de trabalho para uma [Máquina Virtual do Azure que executa o SQL Server](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview). Você pode migrar o sistema no estado em que se encontra e manter o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de fim do suporte ou fazer a atualização para uma versão mais recente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Isso é melhor para migrações e aplicativos que exigem acesso no nível do sistema operacional. As máquinas virtuais do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estão prontas para lift-and-shift em aplicativos existentes que exigem migração rápida para a nuvem com pouca ou nenhuma alteração. 

### <a name="benefits"></a>Benefícios

- **Atualizações de Segurança Estendida gratuitas**: se você optar por manter o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no estado em que se encontra usando o [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)] ou o [!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)], poderá obter Atualizações de Segurança Estendida gratuitas por três anos após o fim da data de suporte, mesmo sem ter o Software Assurance. 
- **Redução de custos**: você economiza o custo do hardware e do software para servidores, pagando apenas pelo uso por hora. 
- **Lift-and-shift**: você pode migrar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e a infraestrutura de aplicativo por lift-and-shift para a nuvem com pouca ou nenhuma alteração. 
- **Ambiente hospedado**: você terá os benefícios de um ambiente hospedado, como descarregamento de hardware e manutenção de software. 
- **Automação**: se você estiver usando o [!INCLUDE[winserver2008r2-md](../../includes/winserver2008r2-md.md)] e superior, obterá o benefício da aplicação automatizada de patch e backups automatizados. 
- **Controle do sistema operacional**: você tem controle sobre o ambiente do sistema operacional, mas com o conjunto de recursos conhecido do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 
- **Implantação rápida**: você pode fazer a implantação rapidamente usando uma biblioteca de imagens de máquinas virtuais. 
- **Mobilidade de Licenças**: você pode levar sua licença, permitindo uma diminuição do custo operacional. 
- **Alta disponibilidade**: você não só se beneficia da disponibilidade da máquina virtual interna pela infraestrutura do Azure que apresenta até 99,99% de disponibilidade, mas também pode aproveitar as opções de alta disponibilidade do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], como instâncias de cluster de failover e grupos de disponibilidade Always On. 
- **Baixo risco para aplicativos de banco de dados**: ao manter a compatibilidade do banco de dados com o mesmo nível dos bancos de dados herdados, os aplicativos de banco de dados existentes ficam protegidos contra alterações funcionais e de desempenho que podem ter efeitos prejudiciais. Um aplicativo só precisa ter uma nova certificação completa quando precisa usar recursos que são restritos por uma configuração de compatibilidade de banco de dados mais recente. Para saber mais, confira [Certificação de Compatibilidade](../../database-engine/install-windows/compatibility-certification.md).

### <a name="considerations"></a>Considerações

- **Capacidade de gerenciamento**: você ainda precisa gerenciar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e software do sistema operacional. 
- **Rede**: você precisa configurar a máquina virtual para se integrar à sua rede e à infraestrutura do Active Directory, que é uma camada adicional de complexidade. 
- **FCI de armazenamento compartilhado**: as máquinas virtuais do Azure só dão suporte a instâncias de cluster de failover que usam os Espaços de Armazenamento Diretos ou os compartilhamentos de arquivo Premium e não dão suporte a uma instância de cluster de failover que usa o armazenamento compartilhado. Assim, as máquinas virtuais do Azure só dão suporte a instâncias de cluster de failover ao usar o Windows Server 2012 ou superior.
- **Tempo de inatividade de escalabilidade**: há um tempo de inatividade ao alterar os recursos de CPU e de armazenamento. 
- **Limitação de tamanho**: embora a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] possa dar suporte a tantos bancos de dados quantos forem necessários, o total cumulativo de todos os bancos de dados para uma instância individual do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é de 256 TB, em comparação com 524 PB para um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]local. 

### <a name="resources"></a>Recursos

[Visão geral da VM do SQL Server](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview)       
[Como escolher uma opção do SQL do Azure](/azure/sql-database/sql-database-paas-vs-sql-server-iaas)       
[Migrar o SQL Server para uma VM do Azure](/azure/virtual-machines/windows/sql/virtual-machines-windows-migrate-sql)       
[ESUs (Atualizações de Segurança Estendida) gratuitas para migração para o Azure no estado em que se encontram](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-2008-eos-extend-support)       
[Visão geral do ESU (Atualizações de Segurança Estendida)](sql-server-extended-security-updates.md)       
[Perguntas frequentes detalhadas sobre o ESU](https://www.microsoft.com/cloud-platform/extended-security-updates)       
[Aplicação automatizada de patch da máquina virtual do SQL](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-automated-patching)       
[Backup automatizado da máquina virtual do SQL](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-automated-backup-v2)       
[Alta disponibilidade de máquina virtual do SQL](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-high-availability-dr)       
[Perguntas frequentes sobre a máquina virtual do SQL](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-faq)       

## <a name="azure-sql-database-single-database"></a>Banco de dados individual do Banco de Dados SQL do Azure

Caso deseje descarregar a manutenção, reduzir os custos e eliminar a necessidade de atualização no futuro, migre a sua carga de trabalho para o [banco de dados individual do Banco de Dados SQL do Azure](/azure/sql-database/sql-database-single-database). Essa opção é melhor para os aplicativos de nuvem modernos que desejam usar os recursos estáveis e mais recentes do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] e têm restrições de tempo em desenvolvimento e marketing. 

### <a name="benefits"></a>Benefícios

- **Custo**: o banco de dados individual pode ser econômico, pois o hardware, o software e a manutenção são descarregados e você pode pagar pelo uso por segundo ou por hora. 
- **Flexibilidade**: o banco de dados individual é particularmente adequado a aplicativos projetados para a nuvem quando a produtividade do desenvolvedor e o rápido tempo para comercialização das soluções são críticos ou que precisam fornecer acesso externo.  
- **Recursos comuns**: os recursos do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] usados com mais frequência estão disponíveis, mas não são tantos como para uma Instância Gerenciada do Banco de Dados SQL do Azure.  
- **Implantação rápida**: você pode implantar rapidamente um banco de dados individual. 
- **Escalabilidade**: você pode escalar ou reduzir verticalmente de maneira rápida e fácil conforme necessário para a sua empresa, fornecendo benefícios adicionais de economia. 
- **Disponibilidade**: o custo do serviço inclui armazenamento e alta disponibilidade, com 99,995% de disponibilidade garantida.  
- **Automação**: a aplicação de patch e os backups ocorrem automaticamente, proporcionando uma economia valiosa de tempo de manutenção.  
- **Intelligent Insights**: obtenha insights sobre o desempenho do seu banco de dados com a análise de inteligência interna.  
- **Sem versão**: o [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] sem versão, o que significa que você está sempre usando a última versão e nunca precisa se preocupar com atualização ou tempo de inatividade. Além disso, você está sempre usando o mais recente e o melhor, com nossos recursos estáveis e mais recentes sendo lançados na nuvem primeiro.
- **Baixo risco para aplicativos de banco de dados**: ao manter a compatibilidade do banco de dados com o mesmo nível do banco de dados local, os aplicativos existentes ficam protegidos contra alterações funcionais e de desempenho que podem ter efeitos prejudiciais. Um aplicativo só precisa ter uma nova certificação completa quando precisa usar recursos que são restritos por uma configuração de compatibilidade de banco de dados mais recente. Para saber mais, confira [Certificação de Compatibilidade](../../database-engine/install-windows/compatibility-certification.md).

### <a name="considerations"></a>Considerações

- **Opções de migração limitadas**:  você só pode migrar um banco de dados individual por vez, em vez de uma instância inteira.   
- **Limitação de recursos**:  embora os recursos do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] usados com mais frequência estejam disponíveis, o conjunto de recursos para um banco de dados individual não é tão completo quanto para uma instância gerenciada do [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] ou o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 
- **Diferenças do Transact-SQL**:  há algumas diferenças do T-SQL ([!INCLUDE[tsql](../../includes/tsql-md.md)]) entre um banco de dados individual e um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] local. 
- **Limitações de tamanho**:  Um banco de dados individual tem um tamanho máximo de banco de dados de 100 TB, em comparação com um tamanho de 524 PB para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 
- **Tempo de manutenção**: não há nenhuma garantia do tempo de manutenção exato, embora ele seja quase transparente. 

### <a name="resources"></a>Recursos

[Visão geral do Banco de Dados SQL do Azure](/azure/sql-database/sql-database-technical-overview)       
[Como escolher uma opção do SQL do Azure](/azure/sql-database/sql-database-paas-vs-sql-server-iaas)       
[Comparação de recursos do Banco de Dados SQL](/azure/sql-database/sql-database-features)       
[Migrar o SQL Server para um banco de dados individual](/azure/sql-database/sql-database-single-database-migrate)       
[Processo de migração mais amplo](/azure/cloud-adoption-framework/migrate/expanded-scope/sql-migration)       
[Diferenças do T-SQL em um banco de dados individual](/azure/sql-database/sql-database-transact-sql-information)       
Limites de recursos entre [vCore](/azure/sql-database/sql-database-vcore-resource-limits-single-databases) e [DTU](/azure/sql-database/sql-database-dtu-resource-limits-single-databases)       
[Intelligent Insights](/azure/sql-database/sql-database-intelligent-insights)       

Ferramentas:
- [Assistente de migração de dados](../../dma/dma-overview.md)
- [Serviço de Migração do Banco de Dados](/azure/dms/dms-overview)

## <a name="azure-sql-database-managed-instance"></a>Instância gerenciada do Banco de Dados SQL do Azure

Caso deseje aproveitar o descarregamento da manutenção e do custo, mas acha o conjunto de recursos de um banco de dados individual do [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] muito limitado, faça a migração para a [Instância Gerenciada do Banco de Dados SQL do Azure](/azure/sql-database/sql-database-managed-instance). Uma instância gerenciada é parecida com um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] local, sem a necessidade de se preocupar com aspectos como falha de hardware ou aplicação de patch. A instância gerenciada é uma coleção de bancos de dados do sistema e de usuário com um conjunto compartilhado de recursos prontos para lift-and-shift e que podem ser usados para a maioria das migrações para a nuvem. Essa opção é melhor para novos aplicativos ou aplicativos locais existentes que desejam usar os recursos estáveis e mais recentes do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] e que são migrados para a nuvem com o mínimo de alterações. 

### <a name="benefits"></a>Benefícios

- **Custo**: você pode economizar descarregando a manutenção de hardware e software.  
- **Lift-and-shift**: você pode migrar por lift-and-shift toda a sua instância local do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para uma instância gerenciada, incluindo todos os bancos de dados com pouca ou nenhuma alteração no banco de dados. 
- **Recursos**: o conjunto de recursos de uma instância gerenciada é muito semelhante ao de uma instância local do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], como consultas entre bancos de dados, publicação e distribuição de replicação transacional, agendamento de trabalhos SQL e suporte a CLR. 
- **Escalabilidade**: todos os bancos de dados em uma instância gerenciada compartilham recursos e é possível escalá-la ou reduzi-la verticalmente a qualquer momento sem tempo de inatividade.   
- **Automação**: a aplicação de patch e os backups ocorrem automaticamente, proporcionando uma economia valiosa de tempo de manutenção.  
- **Disponibilidade**: o custo do serviço inclui armazenamento e alta disponibilidade, com 99,99% de disponibilidade garantida.  
- **Intelligent Insights**: obtenha insights sobre o desempenho dos seus bancos de dados com a análise de inteligência interna.  
- **Sem versão**: o [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] sem versão, o que significa que você está sempre usando a última versão e nunca precisa se preocupar com atualização ou tempo de inatividade. Além disso, você está sempre usando o mais recente e o melhor, com nossos recursos estáveis e mais recentes sendo lançados na nuvem primeiro.
- **Baixo risco para aplicativos de banco de dados**: ao manter a compatibilidade do banco de dados com o mesmo nível dos bancos de dados locais, os aplicativos de banco de dados existentes ficam protegidos contra alterações funcionais e de desempenho que podem ter efeitos prejudiciais. Um aplicativo só precisa ter uma nova certificação completa quando precisa usar recursos que são restritos por uma configuração de compatibilidade de banco de dados mais recente. Para saber mais, confira [Certificação de Compatibilidade](../../database-engine/install-windows/compatibility-certification.md).

### <a name="considerations"></a>Considerações

- **Custo**: a opção de instância gerenciada pode ser mais cara do que a opção de banco de dados individual.  
- **Diferenças do Transact-SQL**: há algumas diferenças do T-SQL ([!INCLUDE[tsql](../../includes/tsql-md.md)]) entre um banco de dados individual e um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] local.  
- **Implantação**:  a implantação de uma instância gerenciada pode levar mais tempo do que a implantação de um banco de dados individual.  
- **Limitação de recursos**: embora uma instância gerenciada compartilhe a maioria dos recursos com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ainda há alguns recursos que não têm suporte. 
- **Limitação de tamanho**: o tamanho de armazenamento combinado de todos os bancos de dados em uma instância gerenciada é limitado a 8 TB, em comparação com 524 PB para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] local.  
- **Rede**: os requisitos de rede para uma instância gerenciada adicionam uma camada extra de complexidade à infraestrutura e exigem um Gateway de VPN ou o Azure ExpressRoute.
- **Tempo de manutenção**: não há nenhuma garantia do tempo de manutenção exato, embora ele seja quase transparente. 

### <a name="resources"></a>Recursos

[Visão geral da Instância Gerenciada do Banco de Dados SQL do Azure](/azure/sql-database/sql-database-managed-instance)       
[Como escolher uma opção do SQL do Azure](/azure/sql-database/sql-database-paas-vs-sql-server-iaas)       
[Comparação de recursos do Banco de Dados SQL](/azure/sql-database/sql-database-features)       
[Migrar o SQL Server para uma instância gerenciada](/azure/sql-database/sql-database-managed-instance-migrate)       
[Processo de migração mais amplo](/azure/cloud-adoption-framework/migrate/expanded-scope/sql-migration)       

Ferramentas:
- [Assistente de migração de dados](../../dma/dma-overview.md)
- [Serviço de Migração do Banco de Dados](/azure/dms/dms-overview)

## <a name="non-sql-options"></a>Opções não SQL

Para determinados tipos de aplicativos, o ideal é considerar uma solução não relacional ou NoSQL, como o Azure Cosmos DB ou o Armazenamento de Tabelas do Azure.

### <a name="azure-cosmos-db"></a>Azure Cosmos DB

Considere o uso do Azure Cosmos DB para aplicativos Web modernos, escalonáveis e móveis que usam dados JSON e exigem uma combinação de consultas robustas e processamento de dados transacionais. Para obter mais informações, consulte [Cosmos DB](https://azure.microsoft.com/services/cosmos-db/). Para obter informações sobre como importar dados, consulte [Importar dados para o Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/import-data/).

O Azure Cosmos DB oferece os seguintes benefícios:
- Os documentos são indexados e você pode usar uma sintaxe SQL familiar para consultá-los.
- O banco de dados é livre de esquemas.
- Você pode adicionar propriedades aos documentos sem precisar recompilar índices.
- Você obtém suporte ao JSON e ao JavaScript dentro do mecanismo de banco de dados.
- Você obtém suporte nativo para dados geoespaciais e integração com outros serviços do Azure, incluindo Pesquisa do Azure, HDInsight e Data Factory.
- Obtenha armazenamento de baixa latência e alto desempenho com níveis de produtividade reservados.

### <a name="azure-table-storage"></a>Armazenamento de tabelas do Azure

Considere o uso do Armazenamento de Tabelas do Azure para armazenar petabytes de dados semiestruturados em uma solução econômica. Para obter mais informações, consulte o [Armazenamento de Tabela](https://azure.microsoft.com/services/storage/tables/).

O Armazenamento de Tabelas do Azure oferece os seguintes benefícios:
- Você pode evoluir seus aplicativos e seu esquema de tabela sem colocar os dados offline.
- Você pode escalar verticalmente sem fragmentar seu conjunto de dados.
- Você obtém armazenamento com redundância geográfica que replica os dados por várias regiões.

## <a name="lifecycle-dates"></a>Datas do ciclo de vida

A tabela a seguir fornece uma estimativa das datas do ciclo de vida para produtos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais detalhes e informações mais precisas, confira a página [Política do Ciclo de Vida da Microsoft](https://support.microsoft.com/hub/4095338/microsoft-lifecycle-policy). 

| **Versão**     | **Ano de lançamento** | **Ano do fim do suporte base** | **Ano do fim do suporte estendido** |
| :---------------| :--------------- | :------------------------------ | :---------------------------- |
| [SQL Server 2019](https://support.microsoft.com/lifecycle/search?alpha=SQL%20Server%202019) | 2019 | 2025 | 2030 |
| [SQL Server 2017](https://support.microsoft.com/lifecycle/search?alpha=SQL%20Server%202017) | 2017 | 2022 | 2027 |
| [SQL Server 2016](https://support.microsoft.com/lifecycle/search?alpha=SQL%20Server%202016) | 2016 | 2021 | 2026 |
| [SQL Server 2014](https://support.microsoft.com/lifecycle/search?alpha=SQL%20Server%202014) | 2014 | 2019 | 2024 |
| [SQL Server 2012](https://support.microsoft.com/lifecycle/search?alpha=SQL%20Server%202012) | 2012 | 2017 | 2022 |
| [SQL Server 2008 R2](https://support.microsoft.com/lifecycle/search?alpha=SQL%20Server%202008%20R2) | 2010 | 2012 | [2019](https://www.microsoft.com/sql-server/sql-server-2008) |
| [SQL Server 2008](https://support.microsoft.com/lifecycle/search?alpha=SQL%20Server%202008) | 2008 | 2012 | [2019](https://www.microsoft.com/sql-server/sql-server-2008) |
| [SQL Server 2005](https://support.microsoft.com/lifecycle/search?alpha=SQL%20Server%202005) | 2006 | 2011 | [2016](https://www.microsoft.com/sql-server/sql-server-2005) |
| [SQL Server 2000](https://support.microsoft.com/lifecycle/search?alpha=SQL%20Server%202000) | 2000 | 2005 | [2013](https://blogs.technet.microsoft.com/cdnitmanagers/2012/12/06/sql-server-2000-end-of-support-april-2013/) |

> [!IMPORTANT]
> Em caso de discrepância entre esta tabela e a página do Ciclo de Vida da [!INCLUDE[msCoName](../../includes/msconame-md.md)], o Ciclo de Vida da [!INCLUDE[msCoName](../../includes/msconame-md.md)] substituirá essa tabela, pois essa tabela deve ser usada como uma referência aproximada.  

## <a name="next-steps"></a>Próximas etapas  
[SQL Server 2019](https://www.microsoft.com/sql-server/sql-server-2019)   
[Fim do suporte do SQL Server 2005](https://www.microsoft.com/sql-server/sql-server-2005)   
[Fim do suporte do SQL Server 2008](https://www.microsoft.com/cloud-platform/windows-sql-server-2008)   
[Visão geral do ESU (Atualizações de Segurança Estendida)](sql-server-extended-security-updates.md)   
[ESUs (Atualizações de Segurança Estendida) gratuitas para migração para o Azure no estado em que se encontram](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-2008-eos-extend-support)   
[Visão geral da VM do SQL Server](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview)   
[Visão geral do Banco de Dados SQL do Azure](/azure/sql-database/sql-database-technical-overview)    

