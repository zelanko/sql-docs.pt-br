---
title: Partições em modelos multidimensionais | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 26e01dc7-fa49-4b1f-99eb-7799d1b4dcd2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 00d17af3ce46ee5b20a730e536321140bb69f4ae
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66073327"
---
# <a name="partitions-in-multidimensional-models"></a>Partições em modelos multidimensionais
  No [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], uma *partição* fornece o armazenamento físico de dados de fatos carregados em um grupo de medidas. Uma única partição é criada para cada grupo de medidas automaticamente, mas é comum criar partições adicionais que segmentam mais os dados, resultando em processamento mais eficiente e em desempenho mais rápido das consultas.  
  
 O processamento é mais eficiente porque as partições podem ser processados de forma independente e em paralelo, em um ou mais servidores. As consultas são executadas mais rápido porque cada partição pode ser configurada para ter os modos de armazenamento e as otimizações de agregação que resultam em tempos de resposta mais curtos. Por exemplo, o armazenamento MOLAP para partições contendo dados mais recentes costuma ser mais rápido do que o ROLAP. Da mesma forma, se você particionar por data, as partições contendo dados mais recentes poderão ter mais otimizações do que as partições contendo dados mais antigos que são acessados com menos frequência. Observe que a variação no design de armazenamento e agregação por partição terá um impacto negativo sobre operações futuras de mesclagem. Verifique se a mesclagem é de fato um componente essencial de sua estratégia de gerenciamento de partição antes de otimizar partições individuais.  
  
> [!NOTE]  
>  O suporte a várias partições está disponível nas edições business intelligence e enterprise. A edição standard não oferece suporte a várias partições. Para obter mais informações, consulte [Features Supported by the Editions of SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
## <a name="important-considerations-when-designing-a-partitioning-strategy"></a>Considerações importantes ao criar uma estratégia de particionamento  
 A integridade dos dados de um cubo depende de os dados serem distribuídos entre as partições do cubo de modo que nenhum dado seja duplicado entre as partições. Quando os dados são resumidos das partições, os elementos de dados que estão presentes em mais de uma partição serão resumidos como se fossem elementos de dados diferentes. Isto pode resultar em resumos incorretos e dados errôneos fornecidos para o usuário final. Por exemplo, se uma transação de vendas para o Produto X for duplicada nas tabelas de fato para duas partições, os resumos de vendas do Produto X poderão incluir uma contabilidade dupla da transação duplicada.  
  
 As partições podem ser mescladas; você pode usar este recurso na sua estratégia global de armazenamento e atualização de dados. As partições somente poderão ser mescladas se tiverem o mesmo modo de armazenamento e design de agregação. Para criar partições que são candidatos a mesclagem posterior, você poderá copiar o design de agregação de outra partição ao criar partições. Você também pode editar uma partição depois de ela ter sido criada para copiar o design de agregação de outra partição. Mesclar partições também deve ser realizado com cuidado para evitar duplicação de dados na partição resultante, o que pode causar inexatidão dos dados do cubo.  
  
## <a name="local-partitions"></a>Partições locais  
 Partições locais são partições definidas, processadas e armazenadas em um servidor. Se houver grandes grupos de medidas em um cubo, é possível particioná-los para que o processamento ocorra paralelamente entre as partições. A vantagem é que o processamento paralelo fornece uma execução mais rápida. Como um trabalho de processamento de partição não precisa terminar antes do início de outro, eles podem ser executados em paralelo. Para obter mais informações, consulte [Criar e gerenciar uma partição local &#40;Analysis Services&#41;](create-and-manage-a-local-partition-analysis-services.md).  
  
## <a name="remote-partitions"></a>Partições remotas  
 Partições remotas são partições definidas em um servidor, mas processadas e armazenadas em outro. Se desejar distribuir o armazenamento de dados e metadados entre vários servidores, use partições remotas. Normalmente, ao fazer a transição do desenvolvimento para a produção, o tamanho dos dados analisados aumenta várias vezes. Com grandes blocos de dados como esses, uma possível alternativa é distribuir tais dados entre vários computadores. Isso é feito não só porque um computador não pode armazenar todos os dados, mas também para processar os dados paralelamente em mais de um computador. Para obter mais informações, consulte [Create and Manage a Remote Partition &#40;Analysis Services&#41;](create-and-manage-a-remote-partition-analysis-services.md).  
  
## <a name="aggregations"></a>Agregações  
 As agregações são resumos pré-calculados de dados de cubo que ajudam a habilitar o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para fornecer rápidas respostas de consultas. Você pode controlar o número de agregações criadas para um grupo de medidas definindo limites de armazenamento, ganhos de desempenho, ou arbitrariamente interrompendo o processo de criação de agregação após sua execução por algum tempo. Mais agregações não são necessariamente melhores. Cada nova agregação tem a custo, em termos de espaço em disco e de tempo de processamento. Recomendamos criar agregações para um ganho de 30% em desempenho e, depois, aumentar o número apenas se o teste ou a experiência o justificar. Para obter mais informações, consulte [Projetando agregações &#40;Analysis Services – Multidimensional&#41;](designing-aggregations-analysis-services-multidimensional.md).  
  
## <a name="partition-merging-and-editing"></a>Mesclando e editando partições  
 Se duas partições usarem o mesmo design de agregação, é possível mesclar essas duas partições em uma. Por exemplo, se você tiver uma dimensão de inventário particionada por mês, no final de cada mês do calendário, será possível mesclar a partição desse mês com a partição existente dos meses acumulados no ano. Desse modo, a partição do mês atual pode ser processada e analisada rapidamente, enquanto o resto do ano em meses só será reprocessado quando for mesclado. O reprocessamento requer um tempo maior e pode ser executado com menos frequência. Para obter mais informações sobre como gerenciar a processo de mesclagem de partições, consulte [Mesclar partições no Analysis Services &#40;SSAS – Multidimensional&#41;](merge-partitions-in-analysis-services-ssas-multidimensional.md). Para editar as partições do cubo usando o **partições** no Designer de cubo, consulte [editar ou excluir partições &#40;Analysis Services - Multidimensional&#41;](edit-or-delete-partitions-analyisis-services-multidimensional.md).  
  
## <a name="related-topics"></a>Tópicos relacionados  
  
|Tópico|Descrição|  
|-----------|-----------------|  
|[Criar e gerenciar uma partição local &#40;Analysis Services&#41;](create-and-manage-a-local-partition-analysis-services.md)|Contém informações sobre como particionar dados usando filtros ou tabelas de fato diferentes sem duplicar dados.|  
|[Definir armazenamento de partição &#40;Analysis Services – Multidimensional&#41;](set-partition-storage-analysis-services-multidimensional.md)|Descreve como configurar o armazenamento para partições.|  
|[Editar ou excluir partições &#40;do Analysis Services - Multidimensional&#41;](edit-or-delete-partitions-analyisis-services-multidimensional.md)|Descreve como exibir e editar partições.|  
|[Mesclar partições no Analysis Services &#40;SSAS – Multidimensional&#41;](merge-partitions-in-analysis-services-ssas-multidimensional.md)|Contém informações sobre como mesclar partições que têm tabelas de fato diferentes ou fatias de dados diferentes sem duplicar dados.|  
|[Definir o write-back de partições](set-partition-writeback.md)|Fornece instruções sobre como habilitar uma partição para gravação.|  
|[Criar e gerenciar uma partição remota &#40;Analysis Services&#41;](create-and-manage-a-remote-partition-analysis-services.md)|Descreve como criar e gerenciar uma partição remota.|  
  
  
