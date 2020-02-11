---
title: Caixa de diálogo atualização incremental (Analysis Services-dados multidimensionais) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.process.incrementalupdate.f1
ms.assetid: d5a5ae27-44e7-4179-b9e2-efbf21d6c5f5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0948fda951bb415d9fe3f457729200752a8afaaf
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66080493"
---
# <a name="incremental-update-dialog-box-analysis-services---multidimensional-data"></a>Caixa de diálogo Atualização Incremental (Analysis Services - Dados Multidimensionais)
  Use a caixa de diálogo **Atualização Incremental** no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] e no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] para definir as configurações a serem usadas quando grupos de medidas e partições forem atualizados incrementalmente. É possível exibir a caixa de diálogo **Atualização Incremental** clicando em **Configurar** na coluna **Configurações** da grade **Lista de Objetos** na caixa de diálogo **Processar** .  
  
## <a name="options"></a>Opções  
  
|Termo|Definição|  
|----------|----------------|  
|**Grupo de medidas**|Selecione o grupo de medidas a ser atualizado incrementalmente.<br /><br /> Observação: esta opção apenas estará habilitada se você estiver atualizando um cubo incrementalmente. Se você estiver atualizando um grupo de medidas ou partição incrementalmente, esta opção será desabilitada.|  
|**Partição**|Selecione a partição a ser atualizada.<br /><br /> Observação: esta opção apenas estará habilitada se você estiver atualizando um cubo incrementalmente. Se você estiver atualizando um grupo de medidas ou partição incrementalmente, esta opção será desabilitada.|  
|**Table**|Clique para atualizar o objeto de uma tabela.|  
|**Fonte de dados ou exibição**|Selecione a fonte de dados ou exibição da fonte de dados na qual a tabela de origem está localizada.<br /><br /> Observação: esta opção apenas estará habilitada se **Tabela** estiver selecionada.|  
|**Nome e esquema da tabela**|Selecione a tabela de origem usada para recuperar dados para atualização incremental do cubo, grupo de medidas ou partição.<br /><br /> Observação: esta opção apenas estará habilitada se **Tabela** estiver selecionada.|  
|**Consulta**|Clique para atualizar o objeto de uma consulta.|  
|**Fonte de Dados**|Selecione a fonte de dados na qual as tabelas a serem consultadas estão localizadas.<br /><br /> Observação: esta opção apenas estará habilitada se **Consulta** estiver selecionada.|  
|**Texto da consulta**|Digite o texto da consulta usada para recuperar dados para atualização incremental do cubo, grupo de medidas ou partição.<br /><br /> Observação: esta opção apenas estará habilitada se **Consulta** estiver selecionada.|  
  
## <a name="see-also"></a>Consulte Também  
 [Analysis Services designers e caixas de diálogo &#40;dados multidimensionais&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [Caixa de diálogo processo &#40;Analysis Services de dados multidimensionais&#41;](process-dialog-box-analysis-services-multidimensional-data.md)  
  
  
