---
title: Selecionar tabelas e exibições (Feeds de dados) (SSAS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.asvs.bidtoolset.seltablesviewsdf.f1
ms.assetid: 6c4fafe0-e02e-47d1-b8bc-e70e872690af
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 199e225e6a3a4b63c704606418fae021b1ba3e9e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36117049"
---
# <a name="select-tables-and-views-data-feeds-ssas"></a>Selecionar tabelas e exibições (feeds de dados) (SSAS)
  Esta página do **Assistente de Importação de Tabela** o habilita a selecionar as tabelas e exibições das quais você deseja importar dados. Para acessar o assistente do [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], no menu **Modelo** , clique em **Importar de Fonte de Dados**.  
  
 A aparência de tabelas e exibições nesta página não garante que essa importação terá êxito. Se o usuário especificado na página Informações sobre Representação não tiver privilégios suficientes para ler do banco de dados selecionado, a importação falhará.  
  
 Para fontes de dados que usam a autenticação do Windows, as credenciais do usuário atual são usadas para buscar as tabelas e exibições na caixa de diálogo Selecionar Tabelas e Exibições. Para outras fontes de dados, as credenciais fornecidas na cadeia de conexão são usadas para buscar os dados.  
  
## <a name="uielement-list"></a>Lista de elementos de interface do usuário  
 **URL de feed de dados**  
 Exibe a URL do feed de dados que você selecionou.  
  
 **Tabelas e exibições**  
 Lista as tabelas e exibições do feed de dados. Marque a caixa de seleção ao lado de cada tabela e exibição que você deseja importar.  
  
 **Tabela de origem**  
 Especifica o nome da tabela de origem com base no tipo de fonte de dados.  
  
 **Nome amigável**  
 Especifica o nome amigável da tabela de origem. Por padrão, a coluna exibe o nome da tabela de origem que aparece na coluna **Tabela de Origem** .  
  
 **Detalhes do Filtro**  
 Exibe o filtro de importação de dados na caixa de diálogo **Detalhes do filtro** quando um filtro é aplicado aos dados sendo importados. Para obter mais informações, consulte [Detalhes do filtro &#40;SSAS&#41;](filter-details-ssas.md).  
  
 **Visualizar e filtrar**  
 Exibe a caixa de diálogo **Visualizar Tabela Selecionada**, que é usada para aplicar um filtro aos dados que estão sendo importados. Para obter mais informações, consulte [Visualizar Tabela Selecionada &#40;SSAS&#41;](preview-selected-table-ssas.md).  
  
 **Selecionar tabelas relacionadas**  
 Selecione as tabelas relacionadas às tabelas e exibições que você selecionou.  
  
  