---
title: "Partições de modelo tabular (SSAS Tabular) | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.asvs.ssms.partitions.partitionmgr.imbi.f1
ms.assetid: 041c269f-a229-4a41-8794-6ba4b014ef83
caps.latest.revision: "11"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 812d973da1d754ee8fcca06151b2068c180cfc5e
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="tabular-model-partitions-ssas-tabular"></a>Partições de modelo tabular (SSAS tabular)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]As partições dividem uma tabela em partes lógicas. Cada partição pode ser processada (Atualizada) independentemente de outras partições. As partições definidas para um modelo durante a criação de modelo são duplicadas em um modelo implantado. Uma vez implantado, você pode gerenciar essas partições e pode criar novas partições usando a caixa de diálogo **Partições** no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou usando um script. As informações fornecidas neste tópico descrevem partições em um banco de dados modelo tabular implantado. Para obter mais informações sobre como criar e gerenciar partições durante a criação de um modelo, consulte [Partições &#40;SSAS de Tabela&#41;](../../analysis-services/tabular-models/partitions-ssas-tabular.md).  
  
 Seções neste tópico:  
  
-   [Benefícios](#bkmk_benefits)  
  
-   [Permissões](#bkmk_permissions)  
  
-   [Processar partições](#bkmk_process_partitions)  
  
-   [Processamento paralelo](#bkmk_parallelProc)  
  
-   [Tarefas relacionadas](#bkmk_related_tasks)  
  
##  <a name="bkmk_benefits"></a> Benefícios  
 O design de modelo eficaz utiliza partições para eliminar processamento desnecessário e carga de processador subsequente em servidores do Analysis Services, enquanto, ao mesmo tempo, faz certos dados que são processados e atualizados com bastante frequência refletirem os dados mais recentes de fontes de dados.  
  
 Por exemplo, um modelo de tabela pode ter uma tabela de Vendas que inclui dados de vendas durante o ano fiscal de 2011 atual e cada um dos anos fiscais anteriores. A tabela de Vendas do modelo tem as três seguintes partições:  
  
|Partition|Dados de|  
|---------------|---------------|  
|Sales2011|Ano fiscal atual|  
|Sales2010-2001|Anos fiscais 2001, 2002, 2003, 2004, 2005, 2006. 2007, 2008, 2009, 2010|  
|SalesOld|Todos os anos fiscais antes dos últimos dez anos.|  
  
 Como novos dados de vendas são adicionados durante o ano fiscal de 2011 atual, esses dados devem ser processados diariamente para serem refletido com precisão na análise de dados de vendas do ano fiscal atual, de modo que a partição Sales2011 seja processada a cada noite.  
  
 Não há nenhuma necessidade de processar dados na partição Sales2010-2001 a cada noite; no entanto, como os dados de vendas durante os dez anos fiscais anteriores ainda podem ser alterados ocasionalmente por causa de devoluções de produtos e outros ajustes, eles ainda devem ser processados regularmente, assim, os dados na partição Sales2010-2001 são processados mensalmente. Os dados na partição SalesOld nunca são alterados; portanto só são processados anualmente.  
  
 Ao entrar no ano fiscal de 2012, uma nova partição Sales2012 é adicionada à tabela de Vendas do modo. A partição Sales2011 pode então ser mesclada com a partição Sales2010-2001 e renomeada como Sales2011-2002. Os dados do ano fiscal 2001 são eliminados da nova partição Sales2011-2002 e movidos para a partição SalesOld. Todas as partições são então processadas para refletir as alterações.  
  
 A maneira como você implementa uma estratégia de partição para os modelos tabulares de sua organização dependerá, em grande parte, de suas necessidades específicas de processamento de dados de modelo e dos recursos disponíveis.  
  
##  <a name="bkmk_permissions"></a> Permissões  
 Para criar, gerenciar e processar partições no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], você deverá ter as permissões do Analysis Services apropriadas definidas em uma função de segurança. Cada função de segurança tem uma das seguintes permissões:  
  
|Permissão|Ações|  
|----------------|-------------|  
|Administrador|Ler, processar, criar, copiar, mesclar, excluir|  
|Processar|Leitura e processo|  
|Somente Leitura|Leitura|  
  
 Para saber mais sobre como criar funções durante a criação do modelo usando o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], consulte [Funções &#40;SSAS de Tabela&#41;](../../analysis-services/tabular-models/roles-ssas-tabular.md). Para saber mais sobre como gerenciar os membros de função para funções de modelo de tabela implantadas usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], consulte [Funções de modelo de tabela &#40;SSAS de Tabela&#41;](../../analysis-services/tabular-models/tabular-model-roles-ssas-tabular.md).  
  
##  <a name="bkmk_parallelProc"></a> Processamento paralelo  
O Analysis Services inclui o processamento paralelo para tabelas com duas ou mais partições, aumentando o desempenho de processamento. Não há nenhuma configuração para o processamento paralelo (consulte as observações). O processamento paralelo ocorre por padrão quando você processa a tabela ou seleciona várias partições para a mesma tabela e processo. Você ainda pode optar por processar as partições de uma tabela de forma independente.  
  
> [!NOTE]  
>  Para especificar se as operações de atualização são executadas em sequência ou em paralelo, você pode usar a opção da propriedade **maxParallism** com o [comando Sequence (TMSL)](../../analysis-services/tabular-models-scripting-language-commands/sequence-command-tmsl.md).

> [!NOTE]  
>  Se a recodificação for detectada, o processamento paralelo pode causar aumento do uso de recursos do sistema. Isso ocorre porque várias operações de partição devem ser interrompidas e reiniciadas com a nova codificação em paralelo.  
  
##  <a name="bkmk_process_partitions"></a> Processar partições  
 As partições podem ser processadas (atualizadas) de forma independente de outras partições com a caixa de diálogo **Partições** no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] ou usando um script. O processamento tem as seguintes opções:  
  
|Modo|Description|  
|----------|-----------------|  
|Processar Padrão|Detecta o estado de processamento de um objeto de partição e realiza o processamento necessário para passar os objetos de partição não processados ou parcialmente processados para um estado completamente processado. Os dados para tabelas vazias e partições são carregados; hierarquias, colunas calculadas e relações são criadas ou recriadas.|  
|Processar Completo|Processa um objeto de partição e todos os objetos que ele contém. Quando o comando Processar Completo for executado para um objeto que já foi processado, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] removerá todos os dados do objeto e processará o objeto. Esse tipo de processamento é necessário quando uma alteração estrutural é feita em um objeto.|  
|Processar Dados|Carregue os dados em uma partição ou uma tabela sem recriar hierarquias ou relações ou recalcular colunas calculadas e medidas.|  
|Processar Limpeza|Remove todos os dados de uma partição.|  
|Processar adição|Atualize a partição incrementalmente com novos dados.|  
  
##  <a name="bkmk_related_tasks"></a> Tarefas relacionadas  
  
|Tarefa|Description|  
|----------|-----------------|  
|[Criar e gerenciar partições de modelos de tabela &#40;SSAS de Tabela&#41;](../../analysis-services/tabular-models/create-and-manage-tabular-model-partitions-ssas-tabular.md)|Descreve como criar e gerenciar partições em um modelo de tabela implantado usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].|  
|[Processar partições de modelo de tabela &#40;SSAS de Tabela&#41;](../../analysis-services/tabular-models/process-tabular-model-partitions-ssas-tabular.md)|Descreve como processar partições em um modelo tabular implantado usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].|  
  
  
