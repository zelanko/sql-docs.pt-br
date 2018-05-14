---
title: Pool de recursos do Resource Governor | Microsoft Docs
ms.custom: ''
ms.date: 10/20/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: resource-governor
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Resource Governor, resource pool
- resource pool [SQL Server], overview
- resource pool [SQL Server]
ms.assetid: 306b6278-e54f-42e6-b746-95a9315e0cbe
caps.latest.revision: 17
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 0c9ca3616b2e5d6c4f417feca2318598adb1ae3b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="resource-governor-resource-pool"></a>Pool de recursos do Administrador de Recursos
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  No Administrador de Recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , um pool de recursos representa um subconjunto dos recursos físicos de uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)]. O Administrador de Recursos permite que você especifique os limites de quantidade de CPU, E/S física e memória que as solicitações recebidas de aplicativos podem usar dentro do pool de recursos. Cada pool de recursos pode conter um ou mais grupos de cargas de trabalho. Quando uma sessão é iniciada, o classificador do Administrador de Recursos atribui a sessão a um grupo de cargas de trabalho específico e a sessão deve ser executada, usando os recursos atribuídos ao grupo de cargas de trabalho.  
  
## <a name="resource-pool-concepts"></a>Conceitos do pool de recursos  
 O pool de recursos ou pool representa os recursos físicos do servidor. É possível pensar no pool como uma instância virtual do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dentro de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Um pool tem duas partes. Uma parte não sobrepõe outros pools, o que permite reserva mínima de recursos. A outra parte é compartilhada com outros pools, fornecendo suporte ao consumo máximo possível de recursos. Os recursos do pool são definidos especificando-se uma ou mais das seguintes configurações para cada recurso (CPU, memória e E/S física):  
  
-   **MIN_CPU_PERCENT e MAX_CPU_PERCENT**  
  
     Essas são as configurações mínima e máxima de largura de banda de CPU garantida para todas as solicitações no pool de recursos quando houver contenção de CPU. Você pode usar essas configurações para estabelecer o uso de recursos previsível de CPU para várias cargas de trabalho com base nas necessidades de cada carga de trabalho. Por exemplo, suponha que os departamentos de Vendas e Marketing em uma empresa compartilhem o mesmo banco de dados. O departamento de Vendas tem uma carga de trabalho com uso intensivo de CPU com consultas de alta prioridade. O departamento de Marketing também tem uma carga de trabalho com uso intensivo de CPU, mas tem consultas de prioridade inferior. Ao criar um pool de recursos separado para cada departamento, você poderá atribuir um percentual *mínimo* de CPU de 70 para o pool de recursos de Vendas e um percentual *máximo* de CPU de 30 para o pool de recursos de Marketing. Isso garante que a carga de trabalho de Vendas receba os recursos de CPU necessários e a carga de trabalho de Marketing seja isolada das demandas de CPU da carga de trabalho de Vendas. Observe que o percentual máximo de CPU é um máximo oportunista. Se houver uma capacidade de CPU disponível, a carga de trabalho a usará até 100 por cento. O valor máximo será aplicado apenas quando houver contenção para recursos da CPU. Nesse exemplo, se a carga de trabalho de Vendas for desativada, a carga de trabalho de Marketing poderá usar 100 por cento da CPU se for necessário.  
  
-   **CAP_CPU_PERCENT**  
  
     Essas configurações são um limite rígido na largura de banda de CPU para todas as solicitações no pool de recursos. As cargas de trabalho associadas com o pool podem usar a capacidade da CPU acima do valor de MAX_CPU_PERCENT quando ela está disponível, mas não acima do valor de CAP_CPU_PERCENT. Usando o exemplo anterior, suponha que o departamento de Marketing esteja sendo cobrado pelo uso do recurso. Eles querem uma cobrança previsível e não querem pagar por mais de 30 por cento da CPU. Isso pode ser feito definindo o CAP_CPU_PERCENT para 30 para o pool de recursos de Marketing.  
  
-   **MIN_MEMORY_PERCENT e MAX_MEMORY_PERCENT**  
  
     Essas configurações são a quantidade mínima e máxima de memória reservada para o pool de recursos que não pode ser compartilhada com outros pools de recursos. A memória referenciada aqui é memória de concessão de execução da consulta, não memória do pool de buffers (por exemplo, páginas de índice e de dados). Ao definir um valor mínimo de memória para um pool, você garante que o percentual de memória especificada esteja disponível para todas as solicitações que possam ser executadas nesse pool de recursos. Este é um diferenciador importante comparado com MIN_CPU_PERCENT, porque, nesse caso, a memória poderá permanecer no pool de recursos determinado mesmo quando o pool não tiver nenhuma solicitação nos grupos de cargas de trabalho que pertencem a este pool. Portanto, é crucial que você seja muito cuidadoso ao usar essa configuração, pois essa memória não estará disponível para uso por nenhum outro pool, mesmo quando não houver solicitações ativas. Definir um valor máximo de memória para um pool significa que, quando as solicitações estiverem em execução nesse pool, elas nunca obterão mais do que essa porcentagem de memória total.  
  
-   **AFFINITY**  
  
     Essa configuração permite relacionar um pool de recursos a um ou mais agendadores ou nós NUMA a fim de obter um maior isolamento de recursos de CPU. Usando o cenário de Vendas e Marketing acima, vamos supor que o departamento de Vendas precise de um ambiente mais isolado e queira 100 por cento do núcleo de uma CPU constantemente. Usando a opção AFFINITY, as cargas de trabalho de Vendas e Marketing podem ser agendadas em CPUs diferentes. Supondo que o CAP_CPU_PERCENT no pool de Marketing ainda esteja ativo, a carga de trabalho de Marketing continuará a usar um máximo de 30 por cento de um núcleo, enquanto que a carga de trabalho de Vendas usará 100 por cento do outro núcleo. Do ponto de vista das cargas de trabalho de Vendas e Marketing, elas estão sendo executadas em dois computadores isolados.  
  
-   **MIN_IOPS_PER_VOLUME e MAX_IOPS_PER_VOLUME**  
  
     Essas configurações são as operações de E/S mínima e máxima por segundo (IOPS) por volume de disco para um pool de recursos. Você pode usar essas configurações para controlar as E/S físicas emitidas para threads de usuário para um determinado pool de recursos. Por exemplo, o departamento de Vendas produz vários relatórios de fim de mês em lotes grandes. As consultas nesses lotes podem gerar E/Ss que podem saturar o volume de disco e afetar o desempenho de outras cargas de trabalho de prioridade mais alta no banco de dados. Para isolar essa carga de trabalho, o MIN_IOPS_PER_VOLUME é definido como 20 e o MAX_IOPS_PER_VOLUME é definido como 100 para o pool de recursos do departamento de Vendas, que controla o nível de E/S que pode emitido para a carga de trabalho.  
  
Ao configurar CPU ou Memória, a soma dos valores MIN de todos os pools não pode ultrapassar 100% dos recursos do servidor. Além disso, ao configurar CPU ou memória, os valores MAX e CAP podem ser definidos em qualquer lugar no intervalo entre MIN e 100 por cento inclusive.  
  
Se um pool tiver um MIN diferente de zero definido, o valor MAX efetivo de outros pools será reajustado. O mínimo do valor MAX configurado de um pool e a soma dos valores MIN de outros pools é subtraído de 100%.  
  
A tabela a seguir ilustra alguns dos conceitos anteriores. A tabela mostra as configurações para o pool interno, para o pool padrão e para dois pools definidos pelo usuário. 
  
|Nome do pool|Configuração de % MIN|Configuração de % MAX|% MAX efetivo calculado|% compartilhado calculado|Comentário|  
|---------------|-------------------|-------------------|--------------------------------|-------------------------|-------------|  
|internal|0|100|100|0|O % MAX efetivo e o % compartilhado não são aplicáveis ao pool interno.|  
|padrão|0|100|30|30|O valor MAX efetivo é calculado como: min(100,100-(20+50)) = 30. O % compartilhado calculado é o MAX efetivo - MIN = 30.|  
|Pool 1|20|100|50|30|O valor MAX efetivo é calculado como: min(100,100-50) = 50. O % compartilhado calculado é o MAX efetivo - MIN = 30.|  
|Pool 2|50|70|70|20|O valor MAX efetivo é calculado como: min(70,100-20) = 70. O % compartilhado calculado é o MAX efetivo - MIN = 20.|  
As fórmulas a seguir são usadas para calcular o MAX% efetivo e o percentual compartilhado na tabela acima:  
  
-   Min(X,Y) significa o menor valor de X e Y.  
  
-   Sum(X) significa a soma do valor X de todos os pools.  
  
-   % compartilhado total = 100 - sum(% MIN).  
  
-   % MAX efetivo = min(X,Y).  
  
-   % compartilhado = % MAX efetivo - % MIN.  

Usando a tabela anterior como exemplo, podemos ilustrar mais tarde os ajustes que são feitos quando outro pool é criado. Esse é o Pool 3 e tem o valor 5 de configuração de % MIN.  
  
|Nome do pool|Configuração de % MIN|Configuração de % MAX|% MAX efetivo calculado|% compartilhado calculado|Comentário|  
|---------------|-------------------|-------------------|--------------------------------|-------------------------|-------------|  
|internal|0|100|100|0|O % MAX efetivo e o % compartilhado não são aplicáveis ao pool interno.|  
|padrão|0|100|25|25|O valor MAX efetivo é calculado como: min(100,100-(20+50+5)) = 25. O % compartilhado calculado é o MAX efetivo - MIN = 25.|  
|Pool 1|20|100|45|25|O valor MAX efetivo é calculado como: min(100,100-55) = 45. O % compartilhado calculado é o MAX efetivo - MIN = 25.|  
|Pool 2|50|70|70|20|O valor MAX efetivo é calculado como: min(70,100-25) = 70. O % compartilhado calculado é o MAX efetivo - MIN = 20.|  
|Pool 3|5|100|30|25|O valor MAX efetivo é calculado como: min(100,100-70) = 30. O % compartilhado calculado é o MAX efetivo - MIN = 25.|  
  
 A parte compartilhada do pool é usada para indicar aonde os recursos disponíveis podem ir se os recursos estão disponíveis. Porém, quando os recursos são consumidos, eles vão para o pool especificado e não são compartilhados. Isso pode melhorar a utilização dos recursos nos casos em que não há solicitações em um determinado pool, e os recursos configurados para o pool podem ser liberados para outros pools.  
  
 Estes são alguns casos extremos de configuração de pool:  
  
-   Todos os pools definem mínimos que, totalizados, representam 100% dos recursos do servidor. Nesse caso, os máximos efetivos são iguais aos mínimos. Isso equivale a dividir os recursos do servidor em partes que não se sobrepõem, independentemente de os recursos serem consumidos em cada pool específico.  
  
-   Todos os pools têm mínimo com valor zero. Todos os pools disputam os recursos disponíveis e seus tamanhos finais baseiam-se no consumo de recurso em cada pool. Outros fatores, como políticas, desempenham uma função na formação do tamanho final do pool.  
  
O Administrador de Recursos define previamente dois pools de recursos, o interno e o padrão. Você pode adicionar outros pools.  
  
**Pool interno**  
  
O pool interno representa os recursos consumidos pelo próprio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Esse pool sempre contém apenas o grupo interno, e o pool não pode ser alterado de forma nenhuma. O consumo de recursos pelo pool interno não é restrito. Todas as cargas de trabalho no pool são consideradas críticas para a função do servidor e o Administrador de Recursos permite que o pool interno pressione os outros pools, mesmo se isso significar violação dos limites definidos para os outros pools.  
  
> [!NOTE]  
>  O uso de recursos do pool interno e do grupo interno não é subtraído do uso de recursos total. As porcentagens são calculadas com base nos recursos totais disponíveis.  
  
**Pool padrão**  
  
O pool padrão é o primeiro pool definido previamente pelo usuário. Antes de qualquer configuração, o pool padrão só contém o grupo padrão. O pool padrão não pode ser criado ou descartado, mas pode ser alterado. O pool padrão pode conter grupos definidos pelo usuário além do grupo padrão. A partir do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] , há um pool de recursos padrão para operações de rotina do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e um pool de recursos externos padrão para processos externos, como a execução de scripts R.  
  
> [!NOTE]  
>  O grupo padrão pode ser alterado, mas não pode ser se movido do pool padrão.  
  
**Pool externo**  
  
Os usuários podem definir um pool externo para definir recursos para os processos externos. Para Serviços de R, isso controla especificamente o `rterm.exe`, `BxlServer.exe` e outros processos gerados por eles.  
  
**Pools de recursos definidos pelo usuário**  
  
Os pools de recursos definidos pelo usuário são aqueles que você cria para cargas de trabalho específicas em seu ambiente. O Administrador de Recursos fornece instruções DDL para criar, alterar e descartar pools de recursos.  
  
## <a name="resource-pool-tasks"></a>Tarefas do pool de recursos  
  
|Descrição da tarefa|Tópico|  
|----------------------|-----------|  
|Descreve como criar um pool de recursos.|[Criar um pool de recursos](../../relational-databases/resource-governor/create-a-resource-pool.md)|  
|Descreve como alterar as configurações do pool de recursos.|[Alterar configurações do pool de recursos](../../relational-databases/resource-governor/change-resource-pool-settings.md)|  
|Descreve como excluir um pool de recursos.|[Excluir um pool de recursos](../../relational-databases/resource-governor/delete-a-resource-pool.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Administrador de Recursos](../../relational-databases/resource-governor/resource-governor.md)   
 [Grupos de carga de trabalho do Administrador de Recursos](../../relational-databases/resource-governor/resource-governor-workload-group.md)   
 [Função de classificação do Administrador de Recursos](../../relational-databases/resource-governor/resource-governor-classifier-function.md)   
 [Configurar o administrador de recursos usando um modelo](../../relational-databases/resource-governor/configure-resource-governor-using-a-template.md)   
 [Exibir Propriedades do Administrador de Recursos](../../relational-databases/resource-governor/view-resource-governor-properties.md)  
  
  
