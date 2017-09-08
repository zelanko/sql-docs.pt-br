---
title: "Requisitos e considerações para Analysis Services implantação | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- memory [Analysis Services]
- scalability [Analysis Services]
- space [Analysis Services]
- Analysis Services deployments, requirements
- deploying [Analysis Services], requirements
- disk space [Analysis Services]
- requirements [Analysis Services]
- processors [Analysis Services]
- system requirements [Analysis Services]
- availability [Analysis Services]
ms.assetid: ef1387a5-5137-4ef4-b731-fec347e5f5ed
caps.latest.revision: 27
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c698473d796548f3ed9d7d17dfb19206804f634f
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="requirements-and-considerations-for-analysis-services-deployment"></a>Requisitos e considerações sobre a implantação do Analysis Services
  O desempenho e disponibilidade de uma solução dependem de muitos fatores, inclusive os recursos do hardware subjacente, a topologia de sua implantação de servidor, as características de sua solução (por exemplo, tendo partições distribuídas por vários servidores ou usando armazenamento de ROLAP que requer acesso direto ao mecanismo relacional), acordos de nível de serviço e a complexidade de seu modelo de dados.  
  
## <a name="memory-and-processor-requirements"></a>Requisitos de memória e processador  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] precisa de mais recursos de memória e processador nos seguintes casos:  
  
-   Ao processar cubos grandes ou complexos. Esse processamento requer mais recursos de memória e processador do que cubos pequenos ou simples.  
  
-   Quando o número de cubos aumenta em um único banco de dados.  
  
-   Quando o número de bancos de dados aumenta em uma única instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
-   Quando o número de instâncias do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] aumenta em um único computador.  
  
-   Quando o número de usuários que estão acessando recursos do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] simultaneamente aumenta.  
  
 A quantidade de memória e os recursos do processador que estão disponíveis para o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] variam, dependendo da edição do SQL Server, sistema operacional, capacidade de hardware e se você está usando processadores virtuais ou físicos. Para obter mais informações, siga estes links:  
  
 [Requisitos de hardware e software para a instalação do SQL Server 2016](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)  
  
 [Computar limites de capacidade por edição do SQL Server](../../sql-server/compute-capacity-limits-by-edition-of-sql-server.md)  
  
 [Recursos com suporte nas edições do SQL Server 2016](../../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md)  
  
 [Especificações de capacidade máxima &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/olap-physical/maximum-capacity-specifications-analysis-services.md)  
  
## <a name="disk-space-requirements"></a>Requisitos de espaço em disco  
 Aspectos diferentes da instalação do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e as tarefas relacionadas ao processamento de objetos requerem diferentes quantidades de espaço em disco. A lista a seguir descreve esses requisitos.  
  
 Cubes  
 Os cubos que têm tabelas de fatos grandes requerem mais espaço em disco do que os cubos com tabelas de fatos pequenas. Do mesmo modo, embora em extensão menor, os cubos com dimensões muito grandes requerem mais espaço em disco do que os cubos com membros de dimensão menores. Geralmente, um banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] requer aproximadamente 20% da quantidade de espaço necessário para os mesmos dados armazenados no banco de dados relacional subjacente.  
  
 Agregações  
 As agregações requerem um espaço adicional proporcional às agregações adicionadas: quanto mais agregações, mais espaço é necessário. Se a criação de agregações desnecessárias for evitada, o espaço em disco adicional necessário para as agregações normalmente não será maior do que cerca de 10% do tamanho dos dados armazenados no banco de dados relacional subjacente.  
  
 Mineração de dados  
 Por padrão, as estruturas de mineração armazenam em cache no disco o conjunto de dados com os quais foram instruídas. Para remover esses dados em cache do disco, use a opção de processamento **Processar Limpeza de Estrutura** no objeto de estrutura de mineração. Para obter mais informações, consulte [Requisitos e considerações sobre processamento &#40;Mineração de dados&#41;](../../analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md).  
  
 Processamento de objetos  
 Durante o processamento, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] armazena cópias dos objetos que estão sendo processados no disco até o final desse procedimento. Quando o processamento termina, as cópias processadas dos objetos substituem os objetos originais. Portanto, é necessário fornecer espaço em disco adicional suficiente para uma segunda cópia de cada objeto a ser processado. Por exemplo, se desejar processar um cubo inteiro em uma única transação, é necessário espaço em disco suficiente para armazenar uma segunda cópia do cubo inteiro.  
  
##  <a name="BKMK_Availability"></a> Considerações sobre disponibilidade  
 Em um ambiente do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , um cubo ou modelo de mineração pode não estar disponível para consulta devido a uma falha de hardware ou software. Um cubo também pode estar indisponível porque precisa ser processado.  
  
### <a name="providing-availability-in-the-event-of-hardware-or-software-failures"></a>Mantendo a disponibilidade caso ocorram falhas de hardware ou software  
 Falhas de hardware ou software podem ocorrer por várias razões. No entanto, manter a disponibilidade da instalação do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] não se trata apenas de solucionar o problema da origem dessas falhas, mas também de fornecer recursos alternativos que permitem ao usuário continuar usando o sistema em caso de falha. Servidores de clustering e de balanceamento de carga normalmente são usados para fornecer recursos alternativos necessários para manter a disponibilidade quando ocorrer falhas de hardware ou software.  
  
 Para manter a disponibilidade caso ocorra uma falha de hardware ou software, implante o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] em um cluster de failover. Em um cluster de failover, se o nó primário falhar por qualquer motivo ou se for necessário reinicializá-lo, o clustering do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows falha em um nó secundário. Após o failover, que ocorre rapidamente, quando executarem a consulta, os usuários estarão acessando a instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] em execução no nó secundário. Para obter mais informações sobre clusters de failover, consulte [Tecnologias do Windows Server: clusters de failover](http://technet.microsoft.com/library/cc732488\(v=WS.10\).aspx).  
  
 Outra solução para problemas de disponibilidade é implantar o projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] em dois ou mais servidores de produção. Em seguida, é possível usar o recurso Balanceamento de Carga de Rede (NLB) dos servidores Windows para combinar os servidores de produção em um único cluster. Em um cluster NLB, se um servidor do cluster ficar indisponível devido a problemas de hardware ou software, o serviço NLB direciona as consultas de usuário para os servidores que ainda estão disponíveis.  
  
### <a name="providing-availability-while-processing-structural-changes"></a>Mantendo a disponibilidade durante o processamento de alterações estruturais  
 Algumas alterações feitas em um cubo podem fazer o cubo ficar indisponível até ser processado. Por exemplo, se forem feitas alterações estruturais em uma dimensão de um cubo, mesmo que a dimensão seja reprocessada, cada cubo que usa a dimensão modificada também deverá ser processado. Até serem processados, esses cubos não podem ser consultados pelos usuários, que também não podem consultar nenhum modelo de mineração baseado em um cubo que tem a dimensão modificada.  
  
 Para manter a disponibilidade durante o processamento de alterações estruturais que podem afetar um ou mais cubos de um projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , incorpore um servidor de preparo e use o Assistente para Sincronizar Bancos de Dados. Esse recurso permite atualizar os dados e metadados de um servidor de preparo e, em seguida, executar uma sincronização online do servidor de produção e do servidor de preparo. Para obter mais informações, consulte [Sincronizar bancos de dados do Analysis Services](../../analysis-services/multidimensional-models/synchronize-analysis-services-databases.md).  
  
 Para processar as atualizações incrementais de modo transparente em dados de origem, habilite o cache pró-ativo. O cache pró-ativo atualiza cubos com novos dados de origem sem exigir o processamento manual e sem afetar a disponibilidade dos cubos. Para obter mais informações, consulte [Cache pró-ativo &#40;Partições&#41;](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md).  
  
##  <a name="BKMK_Scalability"></a> Considerações sobre escalabilidade  
 Várias instâncias do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no mesmo computador podem causar problemas de desempenho. Para solucionar esses problemas, uma opção pode ser aumentar os recursos de processador, memória e disco no servidor. No entanto, talvez também seja necessário dimensionar as instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] em vários computadores.  
  
### <a name="scaling-analysis-services-across-multiple-computers"></a>Dimensionando o Analysis Services em vários computadores  
 Há vários modos para dimensionar uma instalação do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] em vários computadores. Essas opções são descritas na lista a seguir.  
  
-   Se houver várias instâncias no [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] em um único computador, será possível mover uma ou mais instâncias para outro computador.  
  
-   Se houver vários bancos de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] em um único computador, é possível mover um ou mais banco de dados para sua própria instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] em um computador separado.  
  
-   Se um ou mais bancos de dados relacionais fornecem dados para um banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , será possível mover esses bancos de dados para um computador separado. Antes de mover os bancos de dados, verifique a velocidade e a largura de banda da rede que existe entre o banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e os bancos de dados subjacentes. Se a rede estiver lenta ou congestionada, mover os bancos de dados subjacentes para um computador separado poderá degradar o desempenho do processamento.  
  
-   Se o processamento afeta o desempenho da consulta, mas não é possível processar durante os momentos em que há uma menor carga de consulta, mova as tarefas de processamento para um servidor de preparo e, em seguida, execute uma sincronização online do servidor de produção e do servidor de preparo. Para obter mais informações, consulte [Sincronizar bancos de dados do Analysis Services](../../analysis-services/multidimensional-models/synchronize-analysis-services-databases.md). Você também pode distribuir o processamento entre várias instâncias do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usando partições remotas. O processamento de partições remotas usa os recursos de processador e memória no servidor remoto, em vez dos recursos do computador local. Para obter informações sobre o gerenciamento de partições remotas, consulte [Criar e gerenciar uma partição remota &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/create-and-manage-a-remote-partition-analysis-services.md).  
  
-   Se o desempenho da consulta é ruim, mas não é possível aumentar os recursos de processador e memória no servidor local, implante um projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] em dois ou mais servidores de produção. Em seguida, use o Balanceamento de Carga de Rede (NLB) para combinar os servidores em um único cluster. Em um cluster NLB, as consultas são distribuídas automaticamente entre todos os servidores do cluster NLB.  
  
  
