---
title: Tabelas e colunas | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8a172a4916197c39c58774675d39d275724fc619
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="tables-and-columns"></a>Tabelas e colunas 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Depois de ter adicionado tabelas e os dados em um modelo usando o Assistente de Importação de Tabela, você pode começar a trabalhar com as tabelas adicionando novas colunas de dados, criando relacionamentos entre tabelas, definindo cálculos que estendem os dados e filtrando e classificando dados nas tabelas para facilitar a exibição.  
  
 Seções neste tópico:  
  
-   [Benefícios](#bkmk_benefits)  
  
-   [Trabalhando com tabelas e colunas](#bkmk_working)  
  
-   [Tarefas relacionadas](#bkmk_related_tasks)  
  
##  <a name="bkmk_benefits"></a> Benefícios  
 Tabelas, em modelos tabulares, fornecem a estrutura na qual colunas e outros metadados são definidos. As tabelas incluem:  
  
 **Definição da tabela**  
 A definição de tabela inclui o conjunto de colunas. As colunas podem ser importadas de uma fonte de dados ou adicionadas manualmente, como colunas calculadas.  
  
 **Metadados de tabela**  
 Relações, medidas, funções, perspectivas e dados colados são todos os metadados que definem objetos dentro do contexto de uma tabela.  
  
 **Dados**  
 Os dados são populados em colunas de tabela quando você primeiro importa as tabelas usando o Assistente de Importação de Tabela ou criando novos dados em colunas calculadas. Quando os dados são alterados na origem, ou quando um modelo é removido de memória, você deve executar uma operação de processo para repopular os dados nas tabelas.  
  
##  <a name="bkmk_working"></a> Trabalhando com tabelas e colunas  
 No designer de modelo, você não cria novas tabelas modelo diretamente. Uma nova guia será criada automaticamente para você sempre que os dados forem importados ou copiados de outra fonte de dados. Cada guia (no designer de modelo) contém uma tabela de dados que pode incluir o seguinte:  
  
-   Uma única tabela ou exibição de um banco de dados relacional ou de outras origens não relacionais, como um cubo do Analysis Services.  
  
-   Um conjunto de dados tabulares importado de um feed ou arquivo de texto.  
  
-   Uma combinação de dados relacionais e dados tabulares (HTML) copiados e colados na tabela.  
  
 Quando você importa dados, cada tabela ou exibição, planilha ou arquivo de dados é adicionado como uma tabela no designer de modelo. Geralmente você adiciona dados de várias fontes em guias separadas, mas é possível combinar dados em uma única tabela usando **Colar** e **Colar Acréscimo**. Para obter mais informações, consulte [copiar e colar dados](../../analysis-services/tabular-models/ssas-import-data-copy-and-paste-data.md).  
  
 Depois que você adicionar os dados necessários, poderá criar relacionamentos adicionais entre as tabelas, procurar ou referenciar valores relacionados em outras tabelas ou criar valores derivados adicionando novas colunas calculadas.  
  
 Se você estiver trabalhando com conjuntos de dados muito grandes, poderá desejar não filtrar determinados dados para que não sejam visíveis. Você também pode querer classificar dados em uma ordem diferente. Usando o designer de modelo, você pode usar o filtro, classificar e ocultar recursos, colunas inteiras ou determinados dados.  
  
##  <a name="bkmk_related_tasks"></a> Tarefas relacionadas  
  
|Tópico|Description|  
|-----------|-----------------|  
|[Adicionar colunas a uma tabela](../../analysis-services/tabular-models/add-columns-to-a-table-ssas-tabular.md)|Descreve como adicionar uma coluna de origem a uma definição de tabela.|  
|[Excluir uma coluna](../../analysis-services/tabular-models/delete-a-column-ssas-tabular.md)|Descreve como excluir uma coluna de tabela modelo usando o designer de modelos ou usando a caixa de diálogo de Propriedades de Tabela.|  
|[Alterar os mapeamentos de tabela, de coluna ou de filtro de linha](../../analysis-services/tabular-models/change-table-column-or-row-filter-mappings-ssas-tabular.md)|Descreve como alterar tabela, coluna ou mapeamentos de filtro de linha usando a visualização de tabela ou editor de consulta SQL na caixa de diálogo Editar Propriedades de Tabela.|  
|[Especifique Marcar como Tabela de Data para uso com inteligência de dados temporais](../../analysis-services/tabular-models/specify-mark-as-date-table-for-use-with-time-intelligence-ssas-tabular.md)|Descreve como usar a caixa de diálogo Marcar como Tabela de Data para especificar uma tabela de data e coluna de identificador exclusivo. A especificação de uma tabela de data e identificador exclusivo é necessária durante o uso das funções de inteligência de tempo nas fórmulas DAX.|  
|[Adicionar uma tabela](../../analysis-services/tabular-models/add-a-table-ssas-tabular.md)|Descreve como adicionar uma tabela de uma fonte de dados usando uma conexão de fonte de dados existente.|  
|[Excluir uma tabela](../../analysis-services/tabular-models/delete-a-table-ssas-tabular.md)|Descreve como excluir tabelas em seu banco de dados de espaço de trabalho modelo que você não precisa mais.|  
|[Renomear uma tabela ou coluna](../../analysis-services/tabular-models/rename-a-table-or-column-ssas-tabular.md)|Descreve como renomear uma tabela ou coluna para torná-la mais identificável em seu modelo.|  
|[Definir o tipo de dados de uma coluna](../../analysis-services/tabular-models/set-the-data-type-of-a-column-ssas-tabular.md)|Descreve como alterar o tipo de dados de uma coluna. O tipo de dados define como dados na coluna são armazenados e apresentados.|  
|[Ocultar ou congelar colunas](../../analysis-services/tabular-models/hide-or-freeze-columns-ssas-tabular.md)|Descreve como ocultar colunas que você não deseja exibir e como manter uma área de um modelo visível enquanto você rola para outra área do modelo congelando (bloqueando) colunas específicas em uma área.|  
|[Colunas calculadas](../../analysis-services/tabular-models/ssas-calculated-columns.md)|Os tópicos nesta seção descrevem como você pode usar colunas calculadas para adicionar dados agregados a seu modelo.|  
|[Filtrar e classificar dados](http://msdn.microsoft.com/library/55ebd7a6-2458-4398-911f-fcfeb2413f1b)|Os tópicos nesta seção descrevem como você pode filtrar ou classificar dados usando controles no designer de modelo.|  
  
  
