---
title: Caixa de diálogo colunas de chave (Analysis Services-dados multidimensionais) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql.asvs.dimensiondesigner.dbv.dataitemCollection.f1
helpviewer_keywords:
- DataItem Collection dialog box
ms.assetid: 585f27f2-d5eb-4516-b29a-2084010b7d51
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 26eb85c97c970f9fe1cfaf63ca9861c2be0b4695
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66079471"
---
# <a name="key-columns-dialog-box-analysis-services---multidimensional-data"></a>Caixa de diálogo Colunas de Chave (Analysis Services - Dados multidimensionais)
  Use a caixa de diálogo **Colunas de Chave** para alterar a propriedade **KeyColumns** de um atributo. Para obter mais informações, consulte [Modificar a propriedade KeyColumn de um atributo](multidimensional-models/attribute-properties-modify-the-keycolumn-property.md).  
  
 **Para exibir a caixa de diálogo Colunas de Chave**  
  
-   No [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] ou [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], selecione um atributo e, na janela **Propriedades** , clique no botão de reticências (**...**) associado à propriedade **KeyColumns** desse atributo.  
  
## <a name="options"></a>Opções  
 **Tabela de origem**  
 Selecione a tabela de origem para a qual você quer selecionar as colunas de chave. Você pode selecionar a tabela de origem em uma lista que contém todas as tabelas na Exibição da Fonte de Dados.  
  
 **Colunas disponíveis**  
 Selecione as colunas que deseja usar como colunas de chave. Você pode selecionar colunas de uma lista de colunas na **Tabela de origem** especificada que não tenham ainda sido selecionadas como colunas de chave.  
  
 Para adicionar as colunas selecionadas à lista **Colunas de Chave** , clique no botão **>** .  
  
 **Colunas de Chave**  
 Defina a ordem das colunas de chave selecionadas. A ordem das colunas de chave é importante ao se definir a chave composta correta. Para ordenar ou reordenar a lista de colunas de chave, selecione uma coluna e clique nos botões **Acima** ou **Abaixo** .  
  
 Para remover uma coluna de chave da lista **Colunas de Chave** , selecione a coluna e clique no botão **\<** .  
  
 **Para cima**  
 Clique para mover a coluna selecionada em **Colunas de Chave** uma posição acima.  
  
> [!NOTE]  
>  Esta opção só será habilitada se a lista contiver mais de uma coluna e uma coluna estiver selecionada.  
  
 **Para baixo**  
 Clique para mover a coluna selecionada em **Colunas de Chave** uma posição abaixo.  
  
> [!NOTE]  
>  Esta opção só será habilitada se a lista contiver mais de uma coluna e uma coluna estiver selecionada.  
  
 **>**  
  Clique para adicionar uma nova coluna ao final das colunas listadas em **Colunas de Chave**.  
  
 **<**  
  Clique para remover a coluna selecionada das colunas listadas em **Colunas de Chave**.  
  
## <a name="see-also"></a>Consulte Também  
 [Analysis Services designers e caixas de diálogo &#40;dados multidimensionais&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)  
  
  
