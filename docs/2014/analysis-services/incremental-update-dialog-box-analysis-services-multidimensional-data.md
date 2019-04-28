---
title: Caixa de diálogo atualização incremental (Analysis Services - dados multidimensionais) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.process.incrementalupdate.f1
ms.assetid: d5a5ae27-44e7-4179-b9e2-efbf21d6c5f5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 354ec6968698dc5b6a7bbca8ffcd33a34db4389d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62730331"
---
# <a name="incremental-update-dialog-box-analysis-services---multidimensional-data"></a>Caixa de diálogo Atualização Incremental (Analysis Services - Dados Multidimensionais)
  Use a caixa de diálogo **Atualização Incremental** no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] e no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] para definir as configurações a serem usadas quando grupos de medidas e partições forem atualizados incrementalmente. É possível exibir a caixa de diálogo **Atualização Incremental** clicando em **Configurar** na coluna **Configurações** da grade **Lista de Objetos** na caixa de diálogo **Processar** .  
  
## <a name="options"></a>Opções  
  
|Termo|Definição|  
|----------|----------------|  
|**Grupo de Medidas**|Selecione o grupo de medidas a ser atualizado incrementalmente.<br /><br /> Observação: Essa opção é habilitada somente se você estiver atualizando um cubo incrementalmente. Se você estiver atualizando um grupo de medidas ou partição incrementalmente, esta opção será desabilitada.|  
|**Partição**|Selecione a partição a ser atualizada.<br /><br /> Observação: Essa opção é habilitada somente se você estiver atualizando um cubo incrementalmente. Se você estiver atualizando um grupo de medidas ou partição incrementalmente, esta opção será desabilitada.|  
|**Table**|Clique para atualizar o objeto de uma tabela.|  
|**Fonte de dados ou exibição**|Selecione a fonte de dados ou exibição da fonte de dados na qual a tabela de origem está localizada.<br /><br /> Observação: Essa opção estará habilitada apenas se **tabela** está selecionado.|  
|**Nome e o esquema de tabela**|Selecione a tabela de origem usada para recuperar dados para atualização incremental do cubo, grupo de medidas ou partição.<br /><br /> Observação: Essa opção estará habilitada apenas se **tabela** está selecionado.|  
|**Consulta**|Clique para atualizar o objeto de uma consulta.|  
|**Fonte de dados**|Selecione a fonte de dados na qual as tabelas a serem consultadas estão localizadas.<br /><br /> Observação: Essa opção estará habilitada apenas se **consulta** está selecionado.|  
|**Texto da consulta**|Digite o texto da consulta usada para recuperar dados para atualização incremental do cubo, grupo de medidas ou partição.<br /><br /> Observação: Essa opção estará habilitada apenas se **consulta** está selecionado.|  
  
## <a name="see-also"></a>Consulte também  
 [Designers e caixas de diálogo do Analysis Services &#40;dados multidimensionais&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [Processar caixa de diálogo &#40;Analysis Services - dados multidimensionais&#41;](process-dialog-box-analysis-services-multidimensional-data.md)  
  
  
