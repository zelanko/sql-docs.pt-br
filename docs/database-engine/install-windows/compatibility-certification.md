---
title: Certificação de compatibilidade | Microsoft Docs
description: A certificação de compatibilidade elimina os riscos de compatibilidade de aplicativos, o que permite que você atualize um banco de dados do SQL Server local e na nuvem.
ms.custom: ''
ms.date: 08/26/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- compatibility [SQL Server], databases
- compatibility levels [SQL Server], after upgrade
- Database Engine [SQL Server], upgrading
- Databases [SQL Server], upgrading
- Database Engine [SQL Server], upgrading
- compatibility [SQL Server], certification
- compatibility level [SQL Server], upgrades
ms.assetid: 3c036813-36cf-4415-a0c9-248d0a433856
author: pmasl
ms.author: pelopes
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 80fbe0c833f9b4ac7f3d0ec1f845dfd230f09e64
ms.sourcegitcommit: 2600a414c321cfd6dc6daf5b9bcbc9a99c049dc4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/30/2020
ms.locfileid: "91603456"
---
# <a name="compatibility-certification"></a>Certificação de compatibilidade

[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

A certificação de compatibilidade permite que as empresas atualizem e modernizem um banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] local, na nuvem e na borda, eliminando os riscos de compatibilidade do aplicativo. 

O mesmo [!INCLUDE[ssde_md](../../includes/ssde_md.md)] alimenta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] (incluindo a Instância Gerenciada). Esse [!INCLUDE[ssde_md](../../includes/ssde_md.md)] compartilhado significa que um banco de dados do usuário pode ser movido diretamente entre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] locais, enquanto o código do aplicativo executado no banco de dados como [!INCLUDE[tsql](../../includes/tsql-md.md)] continua funcionando como ele faria em seu sistema de origem.

Para cada nova versão de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o nível de compatibilidade padrão é definido como a versão do [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Mas o nível de compatibilidade de versões anteriores é preservado para garantir a compatibilidade contínua dos aplicativos existentes. Essa matriz de compatibilidade pode ser vista [aqui](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md#supported-dbcompats).
Portanto, um aplicativo que foi certificado para funcionar com uma determinada versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **estava, de fato, certificado para funcionar no nível de compatibilidade padrão dessa versão**.

Por exemplo, o nível de compatibilidade do banco de dados 130 era o padrão em [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]. Como os níveis de compatibilidade forçam comportamentos de otimização de consulta e funcionais do [!INCLUDE[tsql](../../includes/tsql-md.md)] específicos, **um banco de dados certificado para trabalhar no [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] foi certificado implicitamente no nível de compatibilidade do banco de dados 130**. Esse banco de dados pode funcionar no estado em que se encontra em uma versão mais recente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (como [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]) e [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)], desde que o nível de compatibilidade do banco de dados seja mantido como 130. 

Esse é um princípio fundamental do modelo de operação de integração contínua do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]. O [!INCLUDE[ssde_md](../../includes/ssde_md.md)] é continuamente aprimorado e atualizado no Azure, mas como os bancos de dados existentes mantêm seu nível de compatibilidade atual, eles continuam funcionando conforme projetado após as atualizações no [!INCLUDE[ssde_md](../../includes/ssde_md.md)] subjacente. 

Essa também é a maneira como o SharePoint Server 2016 e o SharePoint Server 2019 certificam [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e [!INCLUDE[ssSDSMIfull](../../includes/sssdsmifull-md.md)], permitindo que você implante qualquer [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que possa usar os níveis de compatibilidade de banco de dados com suporte nessas versões do SharePoint Server. Para obter mais informações, confira [Requisitos de hardware e software para o SharePoint Server 2016](https://docs.microsoft.com/sharepoint/install/hardware-and-software-requirements#minimum-requirements-for-a-database-server-in-a-farm) e [Requisitos de hardware e software para o SharePoint Server 2019](https://docs.microsoft.com/sharepoint/install/hardware-and-software-requirements-2019#minimum-requirements-for-a-database-server-in-a-farm).

## <a name="managing-upgrade-risk-with-compatibility-certification"></a>Gerenciar risco de atualização com a Certificação de Compatibilidade
Usar a Certificação de Compatibilidade é uma abordagem valiosa à modernização do banco de dados. Ao certificar com base no nível de compatibilidade, os desenvolvedores definem os requisitos técnicos de um aplicativo com suporte no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e no [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)], mas desacoplam o ciclo de vida do aplicativo do ciclo de via da plataforma do banco de dados. Isso permite que as empresas mantenham o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] atualizado conforme necessário pelas políticas de ciclo de vida, além de aproveitar novos aprimoramentos de escalabilidade e desempenho que não dependem de código, e os aplicativos em conexão **mantêm seu status funcional** por meio de atualizações.

A possibilidade de afetar negativamente a funcionalidade e o desempenho é o principal fator de risco de qualquer atualização. A Certificação de Compatibilidade representa a tranquilidade em termos de gerenciamento destes riscos de atualização:

-  No que se refere ao comportamento do [!INCLUDE[tsql](../../includes/tsql-md.md)], qualquer alteração significa que um aplicativo precisa ser recertificado quanto à exatidão. No entanto, a configuração de [nível de compatibilidade do banco de dados](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md) oferece compatibilidade com versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] apenas para o banco de dados especificado, não para todo o servidor. Manter o nível de compatibilidade do banco de dados no estado em que se encontra faz as consultas de aplicativo existentes continuarem exibindo o mesmo comportamento antes e depois de uma atualização [!INCLUDE[ssde_md](../../includes/ssde_md.md)]. Para saber mais sobre o comportamento [!INCLUDE[tsql](../../includes/tsql-md.md)] e níveis de compatibilidade, confira [Usar níveis de compatibilidade para compatibilidade com versões anteriores](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md#backwardCompat).

-  Em relação ao desempenho, como as melhorias no Otimizador de Consulta são introduzidas com cada versão, poderia ser esperado encontrar diferenças de plano de consulta entre diferentes versões do [!INCLUDE[ssde_md](../../includes/ssde_md.md)]. As diferenças de plano de consulta no escopo de uma atualização geralmente representam risco quando há potencial de que algumas alterações possam ser prejudiciais para uma determinada consulta ou carga de trabalho. Por sua vez, esse risco é uma motivação para a recertificação, que pode atrasar atualizações e gerar desafios de ciclo de vida e de suporte. 
   A mitigação de riscos de atualização é o motivo pelo qual os aprimoramentos do Otimizador de Consulta estão restritos ao nível de compatibilidade padrão de uma nova versão (ou seja, o nível de compatibilidade mais alto disponível para qualquer nova versão). A Certificação de Compatibilidade inclui a **proteção de forma do plano de consulta**: a noção de que manter um nível de compatibilidade do banco de dados no estado em que se encontra imediatamente após uma atualização do [!INCLUDE[ssde_md](../../includes/ssde_md.md)] significa usar o mesmo modelo de otimização de consulta da nova versão que era usado antes da atualização e que a forma do plano de consulta não deve ser alterada. 
   Para obter mais informações, confira a seção [Por que usar a forma do plano de consulta?](#queryplan_shape) neste artigo.
   
Para saber mais sobre os níveis de compatibilidade, confira [Usar níveis de compatibilidade para compatibilidade com versões anteriores](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md#backwardCompat).
   
> [!IMPORTANT]
> Para um aplicativo existente que já foi certificado para um determinado nível de compatibilidade, atualize o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] e **mantenha** o nível de compatibilidade do banco de dados anterior. Não é necessário certificar novamente um aplicativo nesse cenário. Para saber mais, confira [Níveis de compatibilidade e Atualizações do Mecanismo de Banco de Dados](#compatibility-levels-and-database-engine-upgrades) mais adiante neste artigo.
>
> Para um novo trabalho de desenvolvimento ou quando um aplicativo existente exige o uso de novos recursos, como o [Processamento de Consulta Inteligente](../../relational-databases/performance/intelligent-query-processing.md), bem como um novo [!INCLUDE[tsql](../../includes/tsql-md.md)], planeje atualizar o nível de compatibilidade do banco de dados para a versão mais recente disponível em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e certifique novamente o aplicativo para que ele funcione com esse nível de compatibilidade. Para obter mais informações sobre como atualizar o nível de compatibilidade do banco de dados, confira [Melhores práticas para atualizar o nível de compatibilidade do banco de dados](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md#best-practices-for-upgrading-database-compatibility-level).
   
### <a name="why-query-plan-shape"></a><a name="queryplan_shape"></a> Por que usar a forma do plano de consulta?      
Forma do plano de consulta refere-se à representação visual dos vários operadores que compõem um plano de consulta. Isso inclui operadores como buscas, verificações, junções e classificações, bem como as conexões entre eles que indicam o fluxo de dados e a ordem das operações que precisam ser executadas e o conjunto de resultados pretendidos. A forma do plano de consulta é determinada pelo otimizador de consulta.

Para manter o desempenho de consultas previsível durante uma atualização, uma das metas fundamentais é garantir que a mesma forma de plano de consulta seja usada. Isso pode ser feito ao não alterar o nível de compatibilidade do banco de dados imediatamente após uma atualização, mesmo que o [!INCLUDE[ssde_md](../../includes/ssde_md.md)] subjacente tenha versões diferentes. Se nada mais for alterado no ecossistema de execução de consultas, como alterações significativas em recursos disponíveis ou na distribuição de dos dados subjacentes, o desempenho de uma consulta deverá permanecer inalterado. 

No entanto, manter a forma de um plano de consulta não é o único fator que pode ter implicações de desempenho após uma atualização. Se mover o banco de dados para um [!INCLUDE[ssde_md](../../includes/ssde_md.md)] mais recente e também fizer alterações ambientais, você poderá estar introduzindo fatores que terão impacto imediato no desempenho de uma consulta, mesmo se o plano de consulta mantiver a mesma forma entre as versões. Essas alterações ambientais podem incluir o novo [!INCLUDE[ssde_md](../../includes/ssde_md.md)] ter mais ou menos recursos de memória e CPU disponíveis, alterações nas opções de configuração do servidor ou do banco de dados ou alterações na distribuição de dados que afetam o modo como um plano de consulta é criado. Por isso, é importante entender que manter o nível de compatibilidade do banco de dados protege contra alterações na **forma** do plano de consulta, mas não oferece proteção contra outros aspectos ambientais que influenciam o desempenho da consulta, alguns dos quais são alterações iniciadas pelo usuário.

Para obter mais informações, confira o [Guia da Arquitetura de Processamento de Consultas](../../relational-databases/query-processing-architecture-guide.md#optimizing-select-statements).
   
## <a name="compatibility-certification-benefits"></a>Benefícios da Certificação de Compatibilidade
Há vários benefícios imediatos para a certificação do banco de dados como uma abordagem baseada em compatibilidade, em vez de uma abordagem de versão nomeada:

-  **Dissociar a certificação do aplicativo da plataforma**. Por causa de seu [!INCLUDE[ssde_md](../../includes/ssde_md.md)], para aplicativos que só precisam executar consultas [!INCLUDE[tsql](../../includes/tsql-md.md)], não há necessidade de manter processos de certificação separados para o Azure e o local.
-  **Reduza os riscos de atualização** porque, durante a modernização da plataforma de banco de dados, os ciclos de atualização da camada de plataforma do banco de dados e do aplicativo podem ser separados para que haja menos interrupções e melhor gerenciamento de alterações.
-  **Atualizar sem alterações no código**. A atualização para uma nova versão de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou de [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] pode ser feita sem alterações no código por meio da manutenção do mesmo nível de compatibilidade que o sistema de origem e sem a necessidade imediata de recertificação até o momento em que o aplicativo precisa aproveitar as melhorias que só estão disponíveis em um nível de compatibilidade do banco de dados mais alto.
- **Melhore a capacidade de gerenciamento e a escalabilidade** sem exigir alterações no aplicativo, usando aprimoramentos que não estão restringidos pelo nível de compatibilidade do banco de dados. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], eles incluem, por exemplo: 
  - Melhorias avançadas de monitoramento e solução de problemas, com novas [Exibições de Gerenciamento Dinâmico do Sistema](../../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md), [Eventos Estendidos](../../relational-databases/extended-events/extended-events.md) e [Ajuste Automático](../../relational-databases/automatic-tuning/automatic-tuning.md). 
  - Escalabilidade aprimorada, por exemplo, com [Soft-NUMA automático](../../database-engine/configure-windows/soft-numa-sql-server.md#automatic-soft-numa), [Recuperação Acelerada de Banco de Dados](../../relational-databases/accelerated-database-recovery-concepts.md) ou [Metadados de tempdb com otimização de memória](../../relational-databases/in-memory-database.md#memory-optimized-tempdb-metadata).

Novos bancos de dados ainda são definidos como o nível de compatibilidade padrão da versão [!INCLUDE[ssde_md](../../includes/ssde_md.md)]. Mas, quando um banco de dados é movido de qualquer versão anterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para uma nova versão de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)], o banco de dados mantém seu nível de compatibilidade existente. 

> [!IMPORTANT]
> Antes de mover um banco de dados para uma nova versão de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)], verifique se ainda há suporte para o nível de compatibilidade do banco de dados. A matriz de suporte do nível de compatibilidade do banco de dados pode ser vista [aqui](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md#arguments). 
>
> A atualização de um banco de dados com um nível de compatibilidade menor do que o permitido (por exemplo, 90 que era o padrão em [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]), define o banco de dados como o menor nível de compatibilidade permitido (100).
>
> Para determinar o nível de compatibilidade atual, consulte a coluna **compatibility_level** de [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md).

## <a name="compatibility-levels-and-database-engine-upgrades"></a>Níveis de compatibilidade e atualizações do Mecanismo de Banco de Dados
Para atualizar o [!INCLUDE[ssde_md](../../includes/ssde_md.md)] para a versão mais recente, mantendo o nível de compatibilidade do banco de dados que existia antes da atualização e o status de capacidade de suporte, é recomendável executar a **validação de área de superfície funcional estática** do código do aplicativo **no banco de dados** (objetos de capacidade de programação como procedimentos armazenados, funções, gatilhos e outros) e **no aplicativo** (usando um rastreamento de carga de trabalho que captura o código dinâmico enviado pelo aplicativo).

Isso pode ser feito facilmente usando a ferramenta [DMA (Assistente de Migração de Dados da Microsoft)](https://www.microsoft.com/download/details.aspx?id=53595). A ausência de erros na saída da ferramenta AMD, sobre a funcionalidade ausente ou incompatível, protege o aplicativo de qualquer regressão funcional na nova versão de destino. Se for necessário realizar alterações para garantir que o seu banco de dados funcione na nova versão, o DMA permitirá que você identifique quando as alterações são necessárias e quais soluções alternativas estão disponíveis. Para obter mais informações, confira [Visão geral do Assistente de Migração de Dados](../../dma/dma-overview.md).   

> [!TIP]
> Essa validação funcional é especialmente importante ao mover um banco de dados de uma versão herdada (como [!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)] ou [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]) para uma nova versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou do [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)], porque o código do aplicativo pode estar usando um [!INCLUDE[tsql](../../includes/tsql-md.md)] descontinuado que não está protegido pelo nível de compatibilidade do banco de dados. Mas, quando estiver migrando de uma versão mais recente (como [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]) para [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] ou [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], não precisará se preocupar com nenhum [!INCLUDE[tsql](../../includes/tsql-md.md)] descontinuado. Para saber mais sobre o [!INCLUDE[tsql](../../includes/tsql-md.md)] descontinuado, confira [Usar níveis de compatibilidade para compatibilidade com versões anteriores](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md#backwardCompat).

> [!NOTE]
> O AMD é compatível com o nível de compatibilidade do banco de dados de 100 ou mais. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] como a versão de origem é excluído.   

> [!IMPORTANT]
> A [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomenda que alguns testes mínimos sejam realizados para validar o sucesso de uma atualização, mantendo o nível de compatibilidade do banco de dados anterior. Você deve determinar quais testes mínimos são importantes para seu próprio aplicativo e cenário.   

> [!IMPORTANT]
> A [!INCLUDE[msCoName](../../includes/msconame-md.md)] fornece proteção de forma do plano de consulta quando:
>
> - A nova versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (destino) é executada no hardware que é comparável ao hardware em que a versão anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (origem) estava em execução.
> - O mesmo [nível de compatibilidade do banco de dados compatível](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md#supported-dbcompats) é usado no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de destino e no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de origem.
> - Os **mesmos** banco de dados e carga de trabalho são usados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de destino e no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de origem. 
>
> Qualquer regressão de forma do plano de consulta (em comparação com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de origem) que ocorre nas condições acima será tratada. Entre em contato com o atendimento ao cliente da Microsoft se esse for o caso.
  
## <a name="see-also"></a>Consulte Também 
[ALTERAR NÍVEL DE COMPATIBILIDADE DO BANCO DE DADOS](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)       
[Exibir ou alterar o nível de compatibilidade de um banco de dados](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md)       
[Melhores práticas para atualizar o Nível de Compatibilidade do Banco de Dados](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md#best-practices-for-upgrading-database-compatibility-level)      
