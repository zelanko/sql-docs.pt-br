---
title: "Governan&#231;a de recursos para servi&#231;os de R | Microsoft Docs"
ms.custom: ""
ms.date: "05/31/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 18c9978a-aa55-42bd-9ab3-8097030888c9
caps.latest.revision: 11
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 11
---
# Governan&#231;a de recursos para servi&#231;os de R
  Um ponto problemático com R é que a análise de grandes quantidades de dados de produção requer hardware adicional e dados geralmente são movidos fora do banco de dados para computadores não controlados pelo IT.  Para executar operações de análise avançada, os clientes desejam aproveitar os recursos do servidor de banco de dados e para proteger seus dados, eles exigem que essas operações atendam aos requisitos de conformidade de nível empresarial, como segurança e desempenho.  
  
 Esta seção fornece informações sobre como você pode gerenciar os recursos usados pelo tempo de execução R e por trabalhos de R em execução usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância como o contexto de computação.  
  
## O que é o controle de recursos?  
 Governança de recursos foi projetada para identificar e evitar problemas comuns em um ambiente de servidor de banco de dados, onde geralmente há vários aplicativos dependentes e vários serviços para oferecer suporte e saldo. Para [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], governança de recursos envolve as seguintes tarefas:  
  
-   Identificando os scripts que usam recursos excessivos de servidor.  
  
     O administrador precisa ser capaz de cancelar ou limitar os trabalhos que estão consumindo muitos recursos.  
  
-   Redução de cargas de trabalho imprevisíveis.  
  
     Por exemplo, se vários trabalhos em R são executados simultaneamente no servidor e os trabalhos não são isolados uns dos outros usando pools de recursos, a contenção de recursos resultante pode resultar em desempenho imprevisível ou ameaçam a conclusão da carga de trabalho.  
  
-   Priorizar as cargas de trabalho.  
  
     O administrador ou o arquiteto precisa ser capazes de especificar cargas de trabalho que devem precedência ou garantia de determinadas cargas de trabalho para ser concluída se houver contenção de recursos.  
  
 Em [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], você pode usar [Resource Governor](../../relational-databases/resource-governor/resource-governor.md) para gerenciar os recursos usados pelo tempo de execução R e pelos trabalhos de R remotos.  
  
## Para usar o administrador de recursos como trabalhos em R gerenciar  
 Em geral, você pode gerenciar os recursos alocados para trabalhos em R, criando *pools de recursos externos* e atribuindo as cargas de trabalho para o pool ou pools. Um pool de recursos externo é um novo tipo de pool de recursos introduzido no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], para ajudar a gerenciar o tempo de execução de R e outros processos externos para o mecanismo de banco de dados.  
  
 Em [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], agora há três tipos de grupos de recursos padrão.  
  
-   O *pool interno* representa os recursos usados pelo próprio SQL Server e não podem ser alterados ou restrito.  
  
-   O *padrão pool* é um conjunto de usuários predefinidos que você pode usar para modificar o uso de recursos para o servidor como um todo. Você também pode definir grupos de usuários que pertencem a esse pool, para gerenciar o acesso aos recursos.  
  
-   O *padrão pool externo* é um pool de usuário predefinido para recursos externos. Além disso, você pode criar novos pools de recursos externos e definir grupos de usuários pertencentes a esse pool.  
  
 Além disso, você pode criar *pools de recursos definidos pelo usuário* para alocar recursos para o mecanismo de banco de dados ou outros aplicativos e criar *pools de recursos externos definidos pelo usuário* para gerenciar R e outros processos externos.  
  
 Para obter uma boa introdução a terminologia e conceitos gerais, consulte [Pool de recursos Resource Governor](../../relational-databases/resource-governor/resource-governor-resource-pool.md).  
  
> [!NOTE]  
>  Atualmente as novas propriedades do administrador de recursos estão disponíveis apenas por meio de instruções DDL ou scripts. não não possível criar grupos de recursos externos por meio da interface do usuário em [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
## Gerenciamento de recursos usando o administrador de recursos 

   Se você for novo para o administrador de recursos, consulte este tópico para uma rápida explicação passo a passo de como modificar os recursos de instância padrão e criar um novo pool de recursos externos:  [como: criar um Pool de recursos para R](../../advanced-analytics/r-services/how-to-create-a-resource-pool-for-r.md)   
  
 Você pode usar o *pool de recursos externos* mecanismo para gerenciar os recursos usados pelos executáveis de R a seguir:  
  
-   Processos Rterm.exe e satélite  
  
-   Processos BxlServer.exe e satélite  
  
-   Processos de satélite iniciados por barra inicial  
  
 No entanto, não há suporte para gerenciamento direto do serviço Launchpad usando o Resource Governor. Isso ocorre porque o [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] é um serviço confiável que pode por design hospedar somente os iniciadores que são fornecidos pela Microsoft. Iniciadores confiáveis também são configuradas para evitar o consumo excessivo de recursos.  
  
 É recomendável que você gerencie processos de satélite usando o Resource Governor e ajustá-los para atender às necessidades da configuração do banco de dados individual e carga de trabalho.  Por exemplo, qualquer processo de satélite individual pode ser criado ou destruído sob demanda durante a execução.  
  
## Desabilitar a execução de Script externo  
 Suporte para scripts externos é opcional em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a instalação. Mesmo depois da instalação [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)], a capacidade de executar scripts externos é desativado por padrão, e você deve reconfigurar a propriedade manualmente e reiniciar a instância para permitir a execução de script.  
  
 Portanto, se houver um problema de recurso que precisa ser atenuados imediatamente, ou um problema de segurança, um administrador pode desabilitar imediatamente qualquer execução de script externo usando [sp_configure & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) e definindo a propriedade `external scripts enabled` como FALSE ou 0.  
  
## Consulte também  
 [Gerenciando e monitorando soluções R](../../advanced-analytics/r-services/managing-and-monitoring-r-solutions.md)  
 [Como: Criar um Pool de recursos para R](../../advanced-analytics/r-services/how-to-create-a-resource-pool-for-r.md)  
 [Pool de recursos do Administrador de Recursos](../../relational-databases/resource-governor/resource-governor-resource-pool.md)
  