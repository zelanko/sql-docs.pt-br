---
title: Extensão do pool de buffers | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: 909ab7d2-2b29-46f5-aea1-280a5f8fedb4
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a48a5cb8b5fb317c40a2106b4ee433e49188d783
ms.sourcegitcommit: 04dd0620202287869b23cc2fde998a18d3200c66
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/30/2018
ms.locfileid: "52640647"
---
# <a name="buffer-pool-extension"></a>Buffer Pool Extension
  Introduzida no [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], a extensão do pool de buffers fornece a integração consistente de uma extensão de memória RAM não volátil (isto é, unidade de estado sólido) com o pool de buffers do [!INCLUDE[ssDE](../../includes/ssde-md.md)] para melhorar significativamente a taxa de transferência de E/S. A extensão do pool de buffers não está disponível em todas as edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obter mais informações, consulte [Features Supported by the Editions of SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
## <a name="benefits-of-the-buffer-pool-extension"></a>Benefícios da extensão do pool de buffers  
 A principal finalidade de um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é armazenar e recuperar dados, de modo que a intensa E/S de disco é uma característica importante do Mecanismo de Banco de Dados. Como as operações de E/S de disco podem consumir muitos recursos e levar um tempo relativamente longo para terminar, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se concentra em tornar a E/S altamente eficiente. O pool de buffers serve como fonte de alocação de memória primária do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O gerenciamento de buffer é um componente fundamental para alcançar essa eficiência. O componente de gerenciamento de buffer consiste em dois mecanismos: o gerenciador de buffer, para acessar e atualizar páginas de banco de dados, e o cache do pool de buffers, para reduzir a E/S do arquivo de banco de dados.  
  
 As páginas de índice e dados são lidas do disco no pool de buffers e as páginas modificadas (também conhecidas como páginas sujas) são gravadas novamente no disco. A demanda de memória nos pontos de verificação de servidor e banco de dados faz com que as páginas sujas dinâmicas (ativas) no cache do buffer sejam removidas do cache e gravadas nos discos mecânicos e, em seguida, lidas novamente no cache. Normalmente, essas operações de E/S são leituras e gravações aleatórias pequenas de 4 a 16 KB de dados. Os padrões de E/S aleatória pequena incorrem em buscas frequentes, competição por braço do disco mecânico, aumento de latência de E/S e redução da taxa de transferência de E/S agregada do sistema.  
  
 A abordagem comum para resolver esses gargalos de E/S é adicionar mais DRAM, ou como alternativa, a adição de eixos SAS de alto desempenho. Embora essas opções sejam úteis, elas apresentam desvantagens significativas: A DRAM é mais cara do que as unidades de armazenamento de dados, e a adição de eixos aumenta as despesas de capital na aquisição de hardware, bem como os custos operacionais com o aumento do consumo de energia e o aumento da probabilidade de falha do componente.  
  
 O recurso de extensão do pool de buffers estende o cache do pool de buffers com o armazenamento não volátil (geralmente, SSD). Graças a essa extensão, o pool de buffers pode acomodar um conjunto de trabalho de banco de dados maior, o que força a paginação de E/Ss entre a RAM e as SSDs. Isso descarrega eficazmente as E/Ss aleatórias pequenas dos discos mecânicos nas SSDs. Devido à latência mais baixa e ao melhor desempenho de E/S aleatória das SSDs, a extensão do pool de buffers melhora significativamente a taxa de transferência de E/S.  
  
 A lista a seguir descreve os benefícios do recurso de extensão do pool de buffers.  
  
-   Aumento da taxa de transferência de E/S aleatória  
  
-   Redução da latência de E/S  
  
-   Aumento da taxa de transferência da transação  
  
-   Melhoria do desempenho de leitura com um pool de buffers híbrido maior  
  
-   Uma arquitetura de cache que pode se beneficiar das unidades de memória de baixo custo presentes e futuras  
  
### <a name="concepts"></a>Conceitos  
 Os termos a seguir são aplicáveis ao recurso de extensão do pool de buffers.  
  
 SSD (unidade de estado sólido)  
 As unidades de estado sólido armazenam dados na memória (RAM) de maneira persistente. Para obter mais informações, consulte [esta definição](http://en.wikipedia.org/wiki/Solid-state_drive).  
  
 Buffer  
 No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], um buffer é uma página de 8 KB na memória, o mesmo tamanho de uma página de dados ou índice. Portanto, o cache do buffer é dividido em páginas de 8 KB. Uma página permanece no cache do buffer até que o gerenciador de buffer precise da área de buffer para ler mais dados. Os dados serão gravados no disco apenas se forem modificados. Essas páginas modificadas na memória são conhecidas como páginas sujas. Uma página está limpa quando equivale à sua imagem de banco de dados no disco. Os dados podem ser modificados no cache do buffer várias vezes antes de serem gravados no disco.  
  
 Pool de buffers  
 Também chamado de cache do buffer. O pool de buffers é um recurso global compartilhado por todos os bancos de dados para suas páginas de dados armazenadas em cache. O tamanho máximo e mínimo do cache do pool de buffers é determinado durante a inicialização ou quando a instância do SQL Server é reconfigurada dinamicamente usando sp_configure. Esse tamanho determina o número máximo de páginas que podem ser armazenadas em cache no pool de buffers a qualquer momento na instância em execução.  
  
 Ponto de verificação  
 Um ponto de verificação cria um bom ponto conhecido a partir do qual o [!INCLUDE[ssDE](../../includes/ssde-md.md)] pode começar a aplicar as alterações contidas no log de transações durante a recuperação após uma pane ou um desligamento inesperado. Um ponto de verificação grava as páginas sujas e as informações do log de transações da memória no disco e, além disso, registra informações sobre o log de transações. Para obter mais informações, consulte [Pontos de verificação de banco de dados &#40;SQL Server&#41;](../../relational-databases/logs/database-checkpoints-sql-server.md).  
  
## <a name="buffer-pool-extension-details"></a>Detalhes da extensão do pool de buffers  
 O armazenamento de SSD é usado como uma extensão para o subsistema de memória, e não para o subsistema de armazenamento de disco. Isto é, o arquivo de extensão do pool de buffers permite que o gerenciador do pool de buffers use a memória flash NAND e DRAM para manter um pool de buffers muito maior de páginas indiferentes na memória RAM não volátil apoiada por SSDs. Isso cria uma hierarquia de cache de vários níveis com o nível 1 (L1) como a DRAM e o nível 2 (L2) como o arquivo de extensão do pool de buffers na SSD. Somente páginas limpas são gravadas no cache L2, o que ajuda a manter a segurança dos dados. O gerenciador de buffer manipula a movimentação de páginas limpas entre os caches L1 e L2.  
  
 A ilustração a seguir fornece uma visão geral arquitetônica de alto nível do pool de buffers em relação a outros componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 ![Arquitetura da extensão do pool de buffers do SSD](../media/ssdbufferpoolextensionarchitecture.gif "Arquitetura da extensão do pool de buffers do SSD")  
  
 Quando habilitada, a extensão do pool de buffers especifica o tamanho e o caminho do arquivo de cache do pool de buffers na SSD. Esse arquivo é uma extensão contígua de armazenamento na SSD e é configurado estaticamente durante a inicialização da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. As alterações nos parâmetros da configuração do arquivo poderão ser realizadas somente quando o recurso de extensão do pool de buffers estiver desabilitado. Quando a extensão do pool de buffers é desabilitada, todas as definições da configuração relacionadas são removidas do Registro. O arquivo de extensão do pool de buffers é excluído durante o desligamento da instância do SQL Server.  
  
## <a name="best-practices"></a>Práticas recomendadas  
 É recomendável seguir estas práticas recomendadas.  
  
-   Depois de habilitar a extensão do Pool de buffers pela primeira vez, é recomendável reiniciar a instância do SQL Server para obter todos os benefícios de desempenho.  
  
-   O tamanho da extensão do pool de buffers pode ser até 32 vezes o valor de max_server_memory para edições Enterprise e até 4 vezes para edições Standard.  É recomendável uma taxa entre o tamanho da memória física (max_server_memory) e o tamanho da extensão do pool de buffers de 1:16 ou menos. Uma taxa mais baixa no intervalo de 1:4 a 1:8 pode ser ótima. Para obter informações sobre como definir a opção max_server_memory, veja [Opções Server Memory de configuração do servidor](server-memory-server-configuration-options.md).  
  
-   Teste toda a extensão do pool de buffers antes da implementação em um ambiente de produção. Uma vez na produção, evite fazer alterações de configuração no arquivo ou desative o recurso. Essas atividades podem ter um impacto negativo no desempenho do servidor, pois o pool de buffers é significativamente reduzido quando o recurso é desabilitado. Quando desabilitado, a memória usada para oferecer suporte ao recurso não é recuperada até que a instância do SQL Server seja reiniciada. No entanto, se o recurso for reabilitado, a memória será reutilizada sem precisar reiniciar a instância.  
  
## <a name="return-information-about-the-buffer-pool-extension"></a>Informações de retorno sobre a extensão do pool de buffers  
 Você pode usar as exibições de gerenciamento dinâmico a seguir para exibir a configuração da extensão do pool de buffers e informações de retorno sobre as páginas de dados na extensão.  
  
-   [sys.dm_os_buffer_pool_extension_configuration &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-buffer-pool-extension-configuration-transact-sql)  
  
-   [sys.dm_os_buffer_descriptors &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-buffer-descriptors-transact-sql)  
  
 Os contadores de desempenho estão disponíveis no SQL Server, objeto Buffer Manager, para rastrear as páginas de dados no arquivo de extensão do pool de buffers. Para obter mais informações, consulte [contadores de desempenho da extensão do pool de buffers](../../relational-databases/performance-monitor/sql-server-buffer-manager-object.md).  
  
 Os Xevents a seguir estão disponíveis.  
  
|XEvent|Descrição|Parâmetros|  
|------------|-----------------|----------------|  
|sqlserver.buffer_pool_extension_pages_written|É acionado quando uma página ou um grupo de páginas é removido do pool de buffers e gravado no arquivo de extensão do pool de buffers.|number_page<br /><br /> first_page_id<br /><br /> first_page_offset<br /><br /> initiator_numa_node_id|  
|sqlserver.buffer_pool_extension_pages_read|É acionado quando uma página é lida do arquivo de extensão do pool de buffers para o pool de buffers.|number_page<br /><br /> first_page_id<br /><br /> first_page_offset<br /><br /> initiator_numa_node_id|  
|sqlserver.buffer_pool_extension_pages_evicted|É acionado quando uma página é removida do arquivo de extensão do pool de buffers.|number_page<br /><br /> first_page_id<br /><br /> first_page_offset<br /><br /> initiator_numa_node_id|  
|sqlserver.buffer_pool_eviction_thresholds_recalculated|É acionado quando o limite de remoção é calculado.|warm_threshold<br /><br /> cold_threshold<br /><br /> pages_bypassed_eviction<br /><br /> eviction_bypass_reason<br /><br /> eviction_bypass_reason_description|  
  
## <a name="related-tasks"></a>Related Tasks  
  
|||  
|-|-|  
|**Descrição da tarefa**|**Tópico**|  
|Habilitar e configurar a extensão do pool de buffers|[ALTER SERVER CONFIGURATION &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-server-configuration-transact-sql)|  
|Modificar a configuração da extensão do pool de buffers|[ALTER SERVER CONFIGURATION &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-server-configuration-transact-sql)|  
|Exibir a configuração da extensão do pool de buffers|[sys.dm_os_buffer_pool_extension_configuration &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-buffer-pool-extension-configuration-transact-sql)|  
|Monitorar a extensão do pool de buffers|[sys.dm_os_buffer_descriptors &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-buffer-descriptors-transact-sql)<br /><br /> [Contadores de desempenho](../../relational-databases/performance-monitor/sql-server-buffer-manager-object.md)|  
  
  
