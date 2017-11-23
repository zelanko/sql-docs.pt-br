---
title: Adicionar uma tabela (SSAS Tabular) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d713c432-db99-4983-acc1-52b0fdd58bd6
caps.latest.revision: "5"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 95113c2053b0e37cc4ee3d94d2baf0ed64d71d57
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="add-a-table-ssas-tabular"></a>Adicionar uma tabela (SSAS tabular)
  Este tópico descreve como adicionar uma tabela de uma fonte de dados da qual você tem dados previamente importados em seu modelo. Para adicionar uma tabela da mesma fonte de dados, você pode usar a conexão de fonte de dados existente. É recomendado sempre usar uma única conexão ao importar qualquer número de tabelas de uma única fonte de dados.  
  
### <a name="to-add-a-table-from-an-existing-data-source"></a>Para adicionar uma tabela de uma fonte de dados existente  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], clique no menu **Modelo** e em **Conexões Existentes**.  
  
2.  Na página **Conexões existentes** , selecione a conexão para a fonte de dados que tem a tabela que você deseja adicionar e clique em **Abrir**.  
  
3.  Na página **Selecionar Tabelas e Exibições** , selecione a tabela da fonte de dados que você deseja adicionar a seu modelo.  
  
    > [!NOTE]  
    >  A página **Selecionar Tabelas e Exibições** não mostrará tabelas que foram importadas previamente como marcadas.  Se você selecionar uma tabela que foi importada previamente usando esta conexão, e você não deu à tabela um nome amigável diferente, um 1 será acrescentado ao nome amigável. Você não precisa selecionar novamente nenhuma tabela que foi previamente importada usando esta conexão.  
  
4.  Se necessário, use **Visualizar e Filtrar** para selecionar somente certas colunas ou aplicar filtros aos dados a serem importados.  
  
5.  Clique em **Concluir** para importar a nova tabela.  
  
> [!NOTE]  
>  Ao importar várias tabelas ao mesmo tempo de uma única fonte de dados, as relações entre essas tabelas na origem serão automaticamente criadas no modelo. Ao adicionar uma tabela posteriormente, porém, você pode precisar criar relações manualmente no modelo entre tabelas recém-adicionadas e as tabelas que foram previamente importadas.  
  
## <a name="see-also"></a>Consulte também  
 [Importar dados &#40;SSAS de Tabela&#41;](http://msdn.microsoft.com/library/6617b2a2-9f69-433e-89e0-4c5dc92982cf)   
 [Excluir uma tabela &#40;SSAS Tabular&#41;](../../analysis-services/tabular-models/delete-a-table-ssas-tabular.md)  
  
  
