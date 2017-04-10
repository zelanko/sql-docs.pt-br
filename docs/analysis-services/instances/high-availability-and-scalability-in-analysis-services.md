---
title: "Alta disponibilidade e escalabilidade no Analysis Services | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d7040a55-1e4d-4c24-9333-689c1b9e2db8
caps.latest.revision: 14
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 14
---
# Alta disponibilidade e escalabilidade no Analysis Services
  Este artigo descreve as técnicas mais usadas para fazer com que os bancos de dados do Analysis Services sejam de alta disponibilidade e escalonáveis. Embora cada objetivo possa ser atingido separadamente, na realidade, eles muitas vezes ocorrem simultaneamente: uma implantação escalável para grandes cargas de trabalho de processamento ou consulta normalmente é acompanhada por expectativas de alta disponibilidade.  
  
 No entanto, o inverso nem sempre é verdadeiro. A alta disponibilidade, sem escala, pode ser o único objetivo em casos de contratos de nível de serviço rigorosos para cargas de trabalho de consulta de missão crítica, mas moderadas.  
  
 Técnicas para fazer com que o Analysis Services seja altamente disponível e escalonável tendem a ser iguais para todos os modos de servidor (Multidimensional, Tabular e modo integrado do SharePoint). A menos que especificamente observado de outra forma, você deve pressupor que as informações neste artigo se aplicam a todos os modos.  
  
## Pontos Principais  
 Como as técnicas para disponibilidade e escalabilidade diferem das do mecanismo de banco de dados relacional, um breve resumo dos pontos principais é uma introdução eficaz às técnicas usadas com o Analysis Services:  
  
-   O Analysis Services utiliza os mecanismos de escalabilidade e disponibilidade alta incorporados à plataforma Windows Server: balanceamento de carga de rede (NLB), Clustering de Failover do Windows Server (WSFC) ou ambos.  
  
    > [!NOTE]  
    >  O recurso Always On do mecanismo de banco de dados relacional não se estende ao Analysis Services.  Não é possível configurar uma instância do Analysis Services para execução em um grupo de disponibilidade Always On.  
    >   
    >  Embora o Analysis Services não seja executado em grupos de disponibilidade Always On, ele pode recuperar e processar dados de bancos de dados relacionais Always On. Para obter instruções sobre como configurar um banco de dados relacional altamente disponível para que ele pode ser usado pelo Analysis Services, veja [Analysis Services com grupos de disponibilidade AlwaysOn](../../database-engine/availability-groups/windows/analysis-services-with-always-on-availability-groups.md).  
  
-   A alta disponibilidade, como um único objetivo, pode ser obtida por meio de redundância do servidor em um cluster de failover. Presume-se que nós de substituição tenham configurações de hardware e software idênticas ao nó ativo.  Por si só, o WSFC fornece alta disponibilidade, mas sem escalabilidade.  
  
-   A escalabilidade, com ou sem a disponibilidade, é obtida por meio de NLB em bancos de dados somente leitura.  Escalabilidade geralmente é uma preocupação quando os volumes de consulta são grandes ou estão sujeitos a picos repentinos.  
  
     O balanceamento de carga, juntamente com vários bancos de dados somente leitura, oferecem escalabilidade e alta disponibilidade porque todos os nós estão ativos e, quando um servidor falha, solicitações são automaticamente redistribuídas entre os nós restantes. Quando você precisa de escalabilidade e disponibilidade, um cluster NLB é a escolha certa.  
  
 Para processamento, os objetivos de alta disponibilidade e escalabilidade são uma preocupação menor, pois você controla o tempo e o escopo das operações. O processamento pode ser parcial e incremental em partes de um modelo, mas, em algum momento, você precisará processar um modelo integralmente em um único servidor para garantir a consistência dos dados em todos os índices e agregações. Uma arquitetura escalonável robusta se depende de hardware que possa acomodar o processamento total em qualquer cadência necessária. Para grandes soluções, esse trabalho é estruturado como uma operação independente, com seus próprios recursos de hardware.  
  
##  <a name="bkmk_serverconfig"></a> Configurações de um versus vários servidores  
 Em uma implantação regular de um servidor, cargas de trabalho de processamento e consulta são executadas simultaneamente, presumindo que os recursos do sistema sejam suficientes para as duas atividades. O Analysis Services mantém as estruturas de dados existentes intactas para o suporte a consultas, enquanto uma versão atualizada é processada em segundo plano. Ter memória suficiente e espaço em disco para lidar com estruturas de dados temporárias é um requisito de hardware para todos os modos de servidor, embora cada modo tenha demandas de recursos do sistema diferentes e diferentes níveis de reconhecimento de NUMA.  
  
 **Escalabilidade e servidores individuais**  
  
 Um único servidor de alto nível de vários núcleos pode fornecer escalabilidade suficiente por conta própria. Em um sistema de alto nível com muitos núcleos, RAM e espaço em disco, a escalabilidade é possível em um só sistema.  
  
 Para bancos de dados multidimensionais, você pode ajustar as propriedades de configuração do servidor para criar afinidade entre processadores e processos. Consulte [Thread Pool Properties](../../analysis-services/server-properties/thread-pool-properties.md) para obter mais informações.  
  
 **Implantações de vários servidores**  
  
 Ocasionalmente, os requisitos operacionais exigem o uso de vários servidores. Por exemplo, os clusters de failover usam vários servidores por definição, com cada nó executado em configurações de software e hardware idênticas.  
  
 Da mesma forma, um requisito rígido de alta disponibilidade de cargas de trabalho de consulta normalmente exige vários servidores. Nesse cenário, a configuração recomendada para o Analysis Services é usar uma combinação de bancos de dados somente leitura e de leitura e gravação executados em instâncias separadas do Analysis Services, em hardware dedicado. Bancos de dados somente leitura lidam com solicitações de consulta. Bancos de dados de leitura e gravação são usados para processamento. Uma descrição mais extensa dessa técnica comum é fornecida na próxima seção.  
  
 **Alta disponibilidade e máquinas virtuais**  
  
 Outra estratégia para atender a um requisito de alta disponibilidade pode incluir o uso de máquinas virtuais. Se a disponibilidade puder ser atendida ao manter um servidor de substituição por horas em vez de minutos, você poderá usar máquinas virtuais que podem ser iniciadas sob demanda e carregadas com bancos de dados atualizados recuperados de um local central.  
  
## Escalabilidade usando bancos de dados somente leitura e de leitura e gravação  
 O balanceamento de carga de rede é recomendado para cargas de trabalho de consulta e processamento grandes ou crescentes. Os bancos de dados do Analysis Services em uma solução NLB são definidos como bancos de dados somente leitura para assegurar consistência entre as consultas.  
  
 Embora as orientações em [Consulta com escalabilidade para o Analysis Services usando bancos de dados somente leitura](https://technet.microsoft.com/library/ff795582\(v=sql.100\).aspx) (publicado em 2008) estejam desatualizadas, elas, de modo geral, ainda são válidas. Embora os sistemas operacionais e hardware de computador tenham evoluído e as referências a plataformas específicas e limites de CPU estejam obsoletas, a técnica básica do uso de bancos de dados somente leitura e de leitura e gravação para grandes volumes de consulta não mudou.  
  
 Essa abordagem pode ser resumida da seguinte maneira:  
  
-   Use hardware dedicado e instâncias do Analysis Services para processar o banco de dados. Configure o banco de dados para somente leitura após a conclusão do processamento. Consulte [Switch an Analysis Services database between ReadOnly and ReadWrite modes](../../analysis-services/multidimensional-models/switch-an-analysis-services-database-between-readonly-and-readwrite-modes.md) para obter instruções.  
  
-   Use vários servidores de consulta idênticos para executar cópias do mesmo banco de dados somente leitura do Analysis Services. Os servidores são implantados em um cluster NLB, acessados por meio de um nome de servidor virtual que funciona como um único ponto de entrada para o cluster.  
  
-   Use o robocopy para copiar um diretório inteiro de dados do servidor de processamento para cada servidor de consulta e anexe o mesmo banco de dados no modo somente leitura para todos os servidores de consulta. Você também pode usar instantâneos de SAN, sincronizações ou qualquer outra ferramenta ou método para mover bancos de dados de produção.  
  
## Demandas de recursos para cargas de trabalho de tabela e multidimensionais  
 A tabela a seguir é um resumo de alto nível como o Analysis Services usa recursos do sistema para consultas e processamento, separados por modo de servidor e armazenamento. Este resumo pode ajudar você a entender o que enfatizar em uma implantação de vários servidores que lida com uma carga de trabalho distribuída.  
  
|||  
|-|-|  
|**Modo de servidor e armazenamento**|**Impacto nos recursos do sistema**|  
|Tabela na memória (padrão), onde consultas são executadas como verificações de tabela de estruturas de dados na memória.|Enfatize RAM e CPUs com altas velocidades de relógio.|  
|Tabela no modo DirectQuery, onde consultas são descarregadas em servidores de banco de dados relacionais de back-end e o processamento é limitado à construção de metadados no modelo.|Foque no desempenho do banco de dados relacional, reduzindo a latência de rede e maximizando a taxa de transferência. CPUs mais rápidas também podem melhorar o desempenho do processador de consulta do Analysis Services.|  
|Modelos multidimensionais usando o armazenamento MOLAP|Escolha uma configuração equilibrada que comporte E/S de disco para carregar os dados rapidamente e RAM suficiente para dados armazenados em cache.|  
|Modelos multidimensionais usando o armazenamento ROLAP|Maximizar a E/S de disco e minimizar a latência de rede.|  
  
## Alta disponibilidade e redundância por meio do WSFC  
 O Analysis Services pode ser instalado em um existente Cluster de Failover do Windows Server (WSFC) para obter alta disponibilidade que restaura o serviço no menor tempo possível.  
  
 Clusters de failover fornecem acesso total (leitura e gravação) ao banco de dados, mas somente um nó por vez. Bancos de dados secundários são executados em nós adicionais do cluster como servidores de substituição se o primeiro nó falhar.  
  
 A principal vantagem do clustering de failover é a rápida recuperação de uma falha de serviço. Essa vantagem tem certas limitações. Por exemplo, se o failover nunca for necessário, os recursos dedicados no cluster ficarão ociosos. Além disso, no caso de um failover, todas as conexões serão perdidas, com a perda correspondente do trabalho não confirmado. A maioria dos aplicativos cliente deve ser capaz de lidar com essa situação; frequentemente, pressionar o botão Atualizar no aplicativo traz os resultados de volta. 
 
 Ao considerar um WSFC, tenha os seguintes pontos em mente:

- Ativo/Ativo não tem suporte no momento. Ativo/Passivo (failover) é a única configuração WSFC com suporte para o Analysis Services.
- Ao realizar clustering do Analysis Services, verifique se todos os nós que participam do cluster são executado em hardware idêntico ou muito semelhante e se o contexto operacional de cada nó é o mesmo quanto à versão do sistema operacional e service packs, versão do Analysis Services e service packs (ou atualizações cumulativas) e o modo de servidor.
- Evite readaptar um nó Passivo como o nó Ativo de outra carga de trabalho. Os ganhos de curto prazo na utilização de computador serão perdidos em caso de uma situação de failover real se o nó não puder lidar com ambas as cargas de trabalho.
 
 Instruções e informações detalhadas sobre a implantação do Analysis Services em um cluster de failover são fornecidas neste white paper: [Como Clusterizar o SQL Server Analysis Services](https://msdn.microsoft.com/library/dn736073.aspx). Embora elas tenham sido escritas para o SQL Server 2012, essas diretrizes ainda se aplicam às versões mais recentes do Analysis Services.  
  
## Consulte também  
 [Sincronizar bancos de dados do Analysis Services](../../analysis-services/multidimensional-models/synchronize-analysis-services-databases.md)   
 [Forçar a afinidade a NUMA para Bancos de Dados Tabulares do Analysis Services](https://blogs.msdn.microsoft.com/sqlcat/2013/11/05/forcing-numa-node-affinity-for-analysis-services-tabular-databases/)   
 [Um Estudo de Caso do Analysis Services: Usar Modelos de Tabela em uma Solução Comercial em Larga Escala](https://msdn.microsoft.com/library/dn751533.aspx)  
  
  