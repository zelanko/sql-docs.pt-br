---
title: Adicionar uma tabela (SSAS tabular) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: d713c432-db99-4983-acc1-52b0fdd58bd6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 81c1d3d2f0a0098fea271a782af10fbd26245a28
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/25/2020
ms.locfileid: "66067792"
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
  
## <a name="see-also"></a>Consulte Também  
 [Importar dados &#40;SSAS de tabela&#41;](../import-data-ssas-tabular.md)   
 [Excluir uma tabela &#40;SSAS Tabular&#41;](delete-a-table-ssas-tabular.md)  
  
  
