---
title: Detalhes de associação de tabela (caixa de diálogo origem da partição) (Analysis Services-dados multidimensionais) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.partitions.partitiontableselection.f1
ms.assetid: 67d05389-81ae-4a6b-947b-986d37ec72b1
author: minewiskan
ms.author: owend
ms.openlocfilehash: ca06f4267edd65885bf4fec1838ecc4360c304fd
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84940147"
---
# <a name="table-binding-detail-partition-source-dialog-box-analysis-services---multidimensional-data"></a>Detalhes de Associação de Tabela (caixa de diálogo Origem da Partição) (Analysis Services - Dados Multidimensionais)
  Use a opção **Associação de Tabela** na caixa de diálogo **Origem da Partição** para especificar a tabela de fatos que fornece os dados para a partição. É possível exibir este painel selecionando **Associação de Tabela** da opção **Tipo de Associação** na caixa de diálogo **Origem da Partição** .  
  
## <a name="options"></a>Opções  
 **Grupo de medidas**  
 Exibe o grupo de medidas desta partição.  
  
 **Examinar**  
 Selecione a fonte de dados ou exibição da fonte de dados que contém as tabelas de origem desta partição. A exibição da fonte de dados usada pelo grupo de medidas selecionado é selecionada por padrão.  
  
 **Filtrar tabelas**  
 Digite a cadeia de caracteres usada para restringir, por nome de tabela, as tabelas exibidas em **Tabelas disponíveis**.  
  
 **Localizar tabelas**  
 Selecione para atualizar a lista de tabelas em **Tabelas disponíveis**, restringindo ainda mais a lista, se uma cadeia de caracteres tiver sido especificada em **Filtrar tabelas**.  
  
 **Tabelas Disponíveis**  
 Clique para selecionar a tabela a ser usada como uma tabela de origem para a partição.  
  
 Se nenhum filtro for especificado em **Filtrar tabelas**, todas as tabelas da fonte de dados ou exibição da fonte de dados especificadas em **Examinar** que forem semelhantes em estrutura à tabela de fatos usada pelo grupo de medidas especificado em **Grupo de medidas** serão listadas.  
  
 Se um filtro for especificado em **Filtrar tabelas**, a lista será restringida ainda mais comparando o filtro com os nomes das tabelas que atendem aos critérios acima. Apenas as tabelas que contêm a cadeia de caracteres especificada em **Filtrar tabelas** são exibidas.  
  
## <a name="see-also"></a>Consulte Também  
 [Caixa de diálogo origem da partição &#40;Analysis Services-dados multidimensionais&#41;](partition-source-dialog-box-analysis-services-multidimensional-data.md)  
  
  
