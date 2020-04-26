---
title: 'Tarefa 11: adicionando transformação de divisão condicional para filtrar duplicatas | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 3094bd57-5cf4-4860-bf51-fadd1b309f94
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 71b050e49440764d355d4658607600c135741f50
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "65476747"
---
# <a name="task-11-adding-conditional-split-transform-to-filter-duplicates"></a>Tarefa 11: Adicionando a Transformação Divisão Condicional para filtrar duplicatas
  Nesta tarefa, você adiciona a Transformação Divisão Condicional ao fluxo de dados. Essa transformação ajuda o ajuda a filtrar duplicatas do conjunto de registros de entrada. A transformação Grupo Difuso agrupa os registros que considera correspondências e escolhe um dos registros como registro dinâmico. Todos os registros em um grupo têm o mesmo valor _key_out. O registro dinâmico no grupo tem o valor _key_in igual ao valor _key_out. Os outros registros no grupo têm valores diferentes para _key_in e _key_out. Assim, quando você filtrar usando a condição _key_in==_key_out, receberá apenas a linha dinâmica no grupo.  
  
1.  Arraste e solte a transformação de **divisão condicional** da seção **comum** na **caixa de ferramentas do SSIS** para a guia fluxo de **dados** .  
  
2.  Clique com o botão direito do mouse em **transformação de divisão condicional** na guia **fluxo de dados** e clique em **renomear**. Digite **duplicatas de filtro** e pressione **Enter**.  
  
3.  Conecte os **fornecedores do grupo com as IDs correspondentes** para **Filtrar duplicatas**.  
  
4.  Clique duas vezes em **Filtrar duplicatas** para iniciar a caixa de diálogo **Editor de transformação de divisão condicional** .  
  
5.  Expanda **colunas** no painel superior esquerdo.  
  
6.  Arraste e solte **_key_in** para a coluna **condição** .  
  
7.  Digite = = (igual a) ao lado de **_key_in** e arrastar e soltar **_key_out**.  
  
8.  Clique em **caso 1** na coluna **nome de saída** , digite **registros exclusivos**e pressione **Enter**.  
  
     ![Editor de Transformação Divisão Condicional](../../2014/tutorials/media/et-addingconditionalsplittransformtofilterduplicates.jpg "Editor de Transformação Divisão Condicional")  
  
9. Clique em **OK** para fechar a caixa de diálogo **Editor de transformação Divisão condicional** .  
  
## <a name="next-step"></a>Próxima etapa  
 [Tarefa 12: Adicionando a Transformação Coluna Derivada para adicionar as colunas necessárias pelo MDS](../../2014/tutorials/task-12-adding-derived-column-transform-to-add-columns-required-by-mds.md)  
  
  
