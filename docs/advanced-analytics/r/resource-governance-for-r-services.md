---
title: "Governança de recursos para o aprendizado de máquina no SQL Server | Microsoft Docs"
ms.custom: 
ms.date: 11/16/2017
ms.prod:
- sql-server-2016
- sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 18c9978a-aa55-42bd-9ab3-8097030888c9
caps.latest.revision: "11"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: e5f334edf065d691a78469c01bf2cd3352a71544
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="resource-governance-for-machine-learning-in-sql-server"></a>Governança de recursos para o aprendizado de máquina no SQL Server

Este artigo fornece uma visão geral do controle de recursos de recursos do SQL Server que ajudam a alocar e equilibrar os recursos usados pelos scripts de R e Python.

**Aplica-se a:** [!INCLUDE[sscurrent-md](../../includes/sscurrent-md.md)] 
 [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)] e [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)][!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)]

## <a name="goals-of-resource-governance-for-machine-learning"></a>Objetivos de controle de recursos de aprendizado de máquina

Um ponto de problemas conhecidos com linguagens de aprendizado de máquina, como R e Python é dados geralmente são movidos fora do banco de dados para computadores não controlados por IT. Outra vantagem é que R é de thread único, que significa que você só pode trabalhar com os dados disponíveis na memória. 

Serviços de aprendizado de máquina do SQL Server elimina esses dois problemas e ajuda a atender os requisitos de conformidade da empresa. Ele mantém análises avançadas no banco de dados e dá suporte ao aumento de desempenho em grandes conjuntos de dados por meio de recursos como fluxo e operações de divisão. No entanto, mover o R e Python cálculos dentro dos bancos de dados pode afetar o desempenho de outros serviços que usam o banco de dados, incluindo consultas de usuário regular, aplicativos externos e trabalhos agendados do banco de dados.

Esta seção fornece informações sobre como você pode gerenciar os recursos usados por tempos de execução externos, como R e Python, para reduzir o impacto em outros serviços de banco de dados principal. Normalmente, um ambiente de servidor de banco de dados é o hub para vários serviços e aplicativos dependentes.

Você pode usar [Resource Governor](../../relational-databases/resource-governor/resource-governor.md) para gerenciar os recursos usados pelos tempos de execução externos para R e Python.  Para o aprendizado de máquina, governança de recursos envolve as seguintes tarefas:

+ Identificar os scripts que usam recursos de servidor em excesso.
  
     O administrador precisa ser capaz de cancelar ou limitar os trabalhos que estão consumindo recursos demais.
  
+ Reduzir cargas de trabalho imprevisíveis.
  
     Por exemplo, se vários trabalhos de aprendizado de máquina são executados simultaneamente no servidor, a contenção de recursos resultante pode resultar em desempenho imprevisível ou ameaçam a conclusão da carga de trabalho. No entanto, se os pools de recursos forem usados, os trabalhos podem ser isolados uma da outra.
  
-   Priorizar as cargas de trabalho.
  
     O administrador ou um arquiteto precisa ser capaz de especificar cargas de trabalho devem têm precedência ou garantir determinadas cargas de trabalho para concluir quando houver contenção de recursos.

## <a name="how-to-use-resource-governor-to-manage-machine-learning"></a>Como usar o administrador de recursos para gerenciar o aprendizado de máquina
 
Gerenciar recursos alocados para sessões de R ou Python, criando um *pool de recursos externos*e a atribuição de cargas de trabalho para o pool ou os pools. Um pool de recursos externos é um novo tipo de pool de recursos introduzido no [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] para ajudar a gerenciar o tempo de execução de R e outros processos externos para o mecanismo de banco de dados.

SQL Server dá suporte a três tipos de pools de recursos padrão: 
  
-   O *pool interno* representa os recursos usados pelo próprio SQL Server e não pode ser alterado nem restrito.
  
-   O *pool padrão* é um conjunto de usuários predefinidos que você pode usar para modificar o uso de recursos para o servidor como um todo. Você também pode definir grupos de usuários que pertencem a esse pool, para gerenciar o acesso aos recursos.
  
-   O *pool externo padrão* é um pool de usuários predefinido para recursos externos. Adicionalmente, você pode criar novos pools de recursos externos e definir grupos de usuários como pertencentes a um desses pools.
  
 Além disso, você pode criar *pools de recursos definidos pelo usuário* para alocar recursos para o mecanismo de banco de dados ou outros aplicativos e criar *pools de recursos externos definidos pelo usuário* para gerenciar o R e outros processos externos.
  
 Para obter uma boa introdução à terminologia e a conceitos gerais, consulte [Pool de recursos do Resource Governor](../../relational-databases/resource-governor/resource-governor-resource-pool.md).

  
## <a name="resource-management-walkthrough-with-resource-governor"></a>Passo a passo o gerenciamento de recursos com o administrador de recursos

Se você for novo para o administrador de recursos, consulte este tópico para uma rápida explicação passo a passo de como modificar os recursos de instância padrão e criar um novo pool de recursos externos: [criar um pool de recursos para scripts externos](../../advanced-analytics/r/how-to-create-a-resource-pool-for-r.md)
  
 Você pode usar o *pool de recursos externos* mecanismo para gerenciar os recursos usados pelos executáveis abaixo que são usados no aprendizado de máquina:

+ Rterm.exe e processos satélite
+ Processos Python.exe e satélite
+ BxlServer.exe e processos satélite
+ Processos de satélite iniciados por barra inicial
  
> [!NOTE]
> 
> Não há suporte para o gerenciamento direto do serviço barra inicial usando o administrador de recursos. Isso ocorre porque o [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] é um serviço confiável que, por design, pode hospedar somente os inicializadores fornecidos pela Microsoft. Iniciadores confiáveis são configuradas para evitar o consumo excessivo de recursos.
>   
> É recomendável que você gerencie os processos satélite usando o Resource Governor e ajuste-os para atender às necessidades da configuração do banco de dados individual e da carga de trabalho.  Por exemplo, qualquer processo satélite individual pode ser criado ou destruído sob demanda durante a execução.
  
## <a name="disable-external-script-execution"></a>Desabilitar a execução do script externo

O suporte para scripts externos é opcional na instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Mesmo depois de instalar a recursos de aprendizado de máquina, a capacidade de executar scripts externos é desativado por padrão, e você deve reconfigurar a propriedade manualmente e reinicie a instância para habilitar a execução do script.

Portanto, se houver um problema de recurso que precisa ser reduzidos imediatamente, ou um problema de segurança, um administrador pode desabilitar imediatamente qualquer execução de script externo usando [sp_configure &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) e definir a propriedade `external scripts enabled` como FALSE ou 0.
  
## <a name="see-also"></a>Consulte também

[Gerenciando e monitorando soluções de aprendizado de máquina](../../advanced-analytics/r/managing-and-monitoring-r-solutions.md)

[Criar um pool de recursos para o aprendizado de máquina](../../advanced-analytics/r/how-to-create-a-resource-pool-for-r.md)

[Pools de recursos do administrador de recursos](../../relational-databases/resource-governor/resource-governor-resource-pool.md)
