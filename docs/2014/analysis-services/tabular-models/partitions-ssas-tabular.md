---
title: Partições (SSAS tabular) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 708b9bdf-8c0b-4476-809a-8f616be23a58
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f5dd80a1f6645e7d1c766e88de653fa1e8f1f4cc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66066897"
---
# <a name="partitions-ssas-tabular"></a>Partições (SSAS tabular)
  As partições dividem uma tabela em partes lógicas. Cada partição pode ser processada (Atualizada) independentemente de outras partições. As partições criadas usando a caixa de diálogo Partições no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] durante a criação do modelo aplicam-se ao banco de dados de workspace modelo. Quando o modelo é implantado, as partições definidas para o banco de dados de workspace modelo são duplicadas no banco de dados modelo implantado. Você ainda pode criar e gerenciar partições para um banco de dados modelo implantado usando a caixa de diálogo Partições no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  As informações fornecidas neste tópico descrevem partições criadas durante a criação modelo usando a caixa de diálogo Gerenciador de Partições no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Para obter informações sobre como criar e gerenciar partições para um modelo implantado, consulte [Criar e gerenciar partições de modelos tabulares &#40;SSAS de Tabela&#41;](create-and-manage-tabular-model-partitions-ssas-tabular.md).  
  
 Seções neste tópico:  
  
-   [Benefícios](#bkmk_benefits)  
  
-   [Tarefas relacionadas](#bkmk_related_tasks)  
  
##  <a name="bkmk_benefits"></a> Benefícios  
 Partições, em modelos tabulares, dividem uma tabela em objetos de partição lógicos. Cada partição pode ser processada independentemente de outras partições. Por exemplo, uma tabela pode incluir determinados conjuntos de linha que contêm dados que raramente são alterados, mas outros conjuntos de linha têm dados que são alterados frequentemente. Nestes casos, não há necessidade de processar todos os dados quando você realmente só deseja processar uma parte deles. As partições permitem que você divida porções de dados que você deseja processar com frequência dos dados que podem ser processados com menos frequência.  
  
 O design de modelo eficaz utiliza partições para eliminar processamento desnecessário e carga de processador subsequente em servidores do Analysis Services, enquanto, ao mesmo tempo, faz certos dados que são processados e atualizados com bastante frequência refletirem os dados mais recentes de fontes de dados. O modo como você implementa e utiliza partições durante a criação de modelo pode ser muito diferente de como partições são implementadas e utilizadas para modelos implantados. Mantenha em mente que, durante a fase de criação modelo, você pode estar trabalhando com somente um subconjunto dos dados que estarão, no final das contas, em seu modelo implantado.  
  
### <a name="processing-partitions"></a>Processando partições  
 Para modelos implantados, o processamento ocorre usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], ou executando um script que inclui o comando de processo e especifica opções e configurações de processamento. Ao criar modelos usando o [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], você pode executar operações de processo usando um comando de Processo do menu ou barra de ferramentas do Modelo. Uma operação de Processo pode ser especificada para uma partição, uma tabela ou tudo.  
  
 Quando uma operação de processo é executada, uma conexão para a fonte de dados é feita usando a conexão de dados. Novos dados são importados nas tabelas modelo, relações e hierarquias são recriadas para cada tabela, e cálculos em colunas calculadas e medidas são recalculados.  
  
 Ao dividir a tabela mais ainda em partições lógicas, você poderá determinar seletivamente o que, quando e como os dados em cada partição são processados. Quando você implanta um modelo, o processamento de partições pode ser concluído manualmente usando a caixa de diálogo Partições no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], ou usando um script que executa um comando de processo.  
  
### <a name="partitions-in-the-model-workspace-database"></a>Partições no banco de dados de workspace modelo  
 Você pode criar novas partições, editar, mesclar ou excluir partições usando o Gerenciador de Partições no [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. O Gerenciador de Partições fornece dois modos para selecionar tabelas, linhas e colunas para uma partição: modo de visualização de tabela e modo de consulta SQL. Todas as partições são definidas usando uma consulta SQL; porém, usando o modo de visualização de tabela, você pode visualizar e selecionar os dados que deseja incluir na partição. A consulta SQL é automaticamente criada e validada para você. Como o modo de visualização de Tabela é a mesma visualização de tabela que está na caixa de diálogo Editar Propriedades de Tabela e na página Visualização de Tabela do Assistente de Importação de Tabela, o número máximo de linhas na visualização é 50.  
  
### <a name="partitions-in-a-deployed-model-database"></a>As partições em um banco de dados modelo implantado  
 Quando você implanta um modelo, as partições para o banco de dados modelo implantado são exibidas como objetos de banco de dados no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Você pode criar, editar, mesclar e excluir partições para um modelo implantado usando a caixa de diálogo Partições no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Gerenciar partições para um modelo implantado no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] está fora do escopo deste tópico. Para saber sobre gerenciamento de partições no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], consulte [Criar e gerenciar partições de modelos tabulares &#40;SSAS de Tabela&#41;](create-and-manage-tabular-model-partitions-ssas-tabular.md).  
  
##  <a name="bkmk_related_tasks"></a> Tarefas relacionadas  
  
|Tópico|DESCRIÇÃO|  
|-----------|-----------------|  
|[Criar e gerenciar partições no banco de dados de espaço de trabalho &#40;SSAS tabular&#41;](workspace-database-ssas-tabular.md)|Descreve como criar e gerenciar partições no banco de dados de workspace modelo usando o Gerenciador de Partições no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].|  
|[Processar partições no banco de dados de espaço de trabalho &#40;SSAS tabular&#41;](process-partitions-in-the-workspace-database-ssas-tabular.md)|Descreve como processar (atualizar) partições no banco de dados de workspace modelo.|  
  
## <a name="see-also"></a>Consulte Também  
 [Modo DirectQuery &#40;SSAS de tabela&#41;](directquery-mode-ssas-tabular.md)   
 [Processar dados &#40;SSAS de tabela&#41;](../process-data-ssas-tabular.md)  
  
  
