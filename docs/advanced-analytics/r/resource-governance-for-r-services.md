---
title: "Governança de recursos para o R Services | Microsoft Docs"
ms.custom: 
ms.date: 05/31/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 18c9978a-aa55-42bd-9ab3-8097030888c9
caps.latest.revision: 11
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5475c2258971c48c2e19bba69d9ec962ae48be87
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="resource-governance-for-r-services"></a>Governança de recursos para o R Services
  Um ponto problemático com o R é que a análise de grandes quantidades de dados em produção requer hardware adicional e os dados geralmente são movidos para fora do banco de dados, para computadores não controlados pelo TI.  Para executar operações de análise avançada, os clientes desejam aproveitar os recursos do servidor de banco de dados e, para proteger seus dados, eles exigem que essas operações atendam aos requisitos de conformidade de nível empresarial, tais como segurança e desempenho.  
  
 Esta seção fornece informações sobre como você pode gerenciar os recursos usados pelo tempo de execução do R e por trabalhos do R em execução usando a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como o contexto de computação.  
  
## <a name="what-is-resource-governance"></a>O que é a governança de recursos?  
 A governança de recursos foi projetada para identificar e evitar problemas comuns em um ambiente de servidor de banco de dados, em que geralmente há vários aplicativos dependentes e vários serviços aos quais dar suporte e balancear. Para o [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], a governança de recursos envolve as seguintes tarefas:  
  
-   Identificar os scripts que usam recursos de servidor em excesso.  
  
     O administrador precisa ser capaz de cancelar ou limitar os trabalhos que estão consumindo recursos demais.  
  
-   Reduzir cargas de trabalho imprevisíveis.  
  
     Por exemplo, se vários trabalhos do R são executados simultaneamente no servidor e os trabalhos não são isolados uns dos outros usando pools de recursos, a contenção de recursos resultante poderia resultar em desempenho imprevisível ou ameaçar a conclusão da carga de trabalho.  
  
-   Priorizar as cargas de trabalho.  
  
     O administrador ou o arquiteto precisa ser capaz de especificar cargas de trabalho que deverão ter precedência ou, se houver contenção de recursos, assegurar que determinadas cargas de trabalho sejam concluídas.  
  
 Em [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], você pode usar o [Resource Governor](../../relational-databases/resource-governor/resource-governor.md) para gerenciar os recursos usados pelo tempo de execução do R e pelos trabalhos do R remotos.  
  
## <a name="how-to-use-resource-governor-to-manage-r-jobs"></a>Como usar o Resource Governor para gerenciar trabalhos do R  
 Em geral, você pode gerenciar os recursos alocados para trabalhos do R criando *pools de recursos externo* e atribuindo as cargas de trabalho para um ou mais pools. Um pool de recursos externo é um novo tipo de pool de recursos introduzido no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], para ajudar a gerenciar o tempo de execução do R e outros processos externos ao mecanismo de banco de dados.  
  
 Em [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], agora há três tipos de grupos de recursos padrão.  
  
-   O *pool interno* representa os recursos usados pelo próprio SQL Server e não pode ser alterado nem restrito.  
  
-   O *pool padrão* é um conjunto de usuários predefinidos que você pode usar para modificar o uso de recursos para o servidor como um todo. Você também pode definir grupos de usuários que pertencem a esse pool, para gerenciar o acesso aos recursos.  
  
-   O *pool externo padrão* é um pool de usuários predefinido para recursos externos. Adicionalmente, você pode criar novos pools de recursos externos e definir grupos de usuários como pertencentes a um desses pools.  
  
 Além disso, você pode criar *pools de recursos definidos pelo usuário* para alocar recursos para o mecanismo de banco de dados ou outros aplicativos e criar *pools de recursos externos definidos pelo usuário* para gerenciar o R e outros processos externos.  
  
 Para obter uma boa introdução à terminologia e a conceitos gerais, consulte [Pool de recursos do Resource Governor](../../relational-databases/resource-governor/resource-governor-resource-pool.md).  

  
## <a name="resource-management-using-resource-governor"></a>Gerenciamento de recursos usando o Resource Governor 

   Se você for novato no uso do Resource Governor, consulte este tópico para uma rápida explicação passo a passo de como modificar os recursos padrão da instância e criar um novo pool de recursos externo: [Como criar um pool de recursos para o R](../../advanced-analytics/r-services/how-to-create-a-resource-pool-for-r.md)   
  
 Você pode usar o mecanismo do *pool de recursos externo* para gerenciar os recursos usados pelos executáveis de R a seguir:  
  
-   Rterm.exe e processos satélite  
  
-   BxlServer.exe e processos satélite  
  
-   Processos satélite iniciados pelo LaunchPad  
  
 No entanto, não há suporte para gerenciamento direto do serviço Launchpad pelo uso do Resource Governor. Isso ocorre porque o [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] é um serviço confiável que, por design, pode hospedar somente os inicializadores fornecidos pela Microsoft. Inicializadores confiáveis também são configurados para evitar o consumo excessivo de recursos.  
  
 É recomendável que você gerencie os processos satélite usando o Resource Governor e ajuste-os para atender às necessidades da configuração do banco de dados individual e da carga de trabalho.  Por exemplo, qualquer processo satélite individual pode ser criado ou destruído sob demanda durante a execução.  
  
## <a name="disable-external-script-execution"></a>Desabilitar a execução de script externo  
 O suporte para scripts externos é opcional na instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Mesmo depois da instalação do [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)], a capacidade de executar scripts externos fica DESATIVADA por padrão e você deve reconfigurar a propriedade e reiniciar a instância manualmente para habilitar a execução de scripts.  
  
 Portanto, se houver um problema de recurso que precise ser atenuados imediatamente ou um problema de segurança, um administrador poderá desabilitar imediatamente qualquer execução de script externo usando [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) e definindo a propriedade `external scripts enabled` como FALSE ou 0.  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciando e monitorando soluções de R](../../advanced-analytics/r-services/managing-and-monitoring-r-solutions.md)  
 [Como criar um pool de recursos para o R](../../advanced-analytics/r-services/how-to-create-a-resource-pool-for-r.md)  
 [Pool de recursos do Resource Governor](../../relational-databases/resource-governor/resource-governor-resource-pool.md)
  


