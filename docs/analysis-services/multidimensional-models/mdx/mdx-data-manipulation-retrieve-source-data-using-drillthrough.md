---
title: Usando DRILLTHROUGH para recuperar dados de origem (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- DRILLTHROUGH statement
- retrieving data
- queries [MDX], DRILLTHROUGH statement
- data retrieval [MDX]
ms.assetid: fe0ab170-25a9-45a8-a377-f71a67f77018
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9470c5edd50bab3622ad73f3e3404a4747b07dd7
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="mdx-data-manipulation---retrieve-source-data-using-drillthrough"></a>Manipulação de dados MDX - recuperar dados de origem usando o DETALHAMENTO
  As expressões multidimensionais (MDX) usam a instrução [DRILLTHROUGH](../../../mdx/mdx-data-manipulation-drillthrough.md)para recuperar um conjunto de linhas dos dados de origem de uma célula de cubo.  
  
 Para executar uma instrução **DRILLTHROUGH** em um cubo, uma ação de drillthrough deve ser definida para esse cubo. Para definir a ação de drillthrough, no [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)], no Designer de Cubo, no painel **Ações** , na barra de ferramentas, clique em **Nova Ação de Drillthrough**. Na nova ação de drillthrough, especifique o nome da ação, o destino, a condição e as colunas que serão retornadas pela instrução **DRILLTHROUGH** .  
  
## <a name="drillthrough-statement-syntax"></a>Sintaxe da instrução DRILLTHROUGH  
 A instrução **DRILLTHROUGH** utiliza esta sintaxe:  
  
```  
<drillthrough> ::= DRILLTHROUGH [<Max_Rows>] [<First_Rowset>] <MDX select> [<Return_Columns>]  
   < Max_Rows> ::= MAXROWS <positive number>  
   <First_Rowset> ::= FIRSTROWSET <positive number>  
   <Return_Columns> ::= RETURN <member or attribute> [, <member or attribute>]  
```  
  
 A cláusula **SELECT** identifica a célula de cubo que contém os dados de origem que serão recuperados. Essa cláusula **SELECT** é igual a uma instrução MDX **SELECT** comum, com exceção de que, na cláusula **SELECT** , apenas um membro pode ser especificado em cada eixo. Se mais de um membro for especificado em um eixo, ocorrerá um erro.  
  
 A sintaxe de `<Max_Rows>` especifica o número de máximo de linhas em cada conjunto de linhas retornado. Se o provedor OLE DB usado para estabelecer a conexão com a fonte de dados não oferecer suporte a **DBPRP_MAXROWS**, a configuração `<Max_Rows>` será ignorada.  
  
 A sintaxe de `<First_Rowset>` identifica a partição cujo conjunto de linhas será retornado primeiro.  
  
 A sintaxe de `<Return_Columns>` identifica as colunas do banco de dados subjacente que serão retornadas.  
  
## <a name="drillthrough-statement-example"></a>Exemplo da instrução DRILLTHROUGH  
 O exemplo a seguir demonstra o uso da instrução **DRILLTHROUGH** . Nesse exemplo, a instrução DRILLTHROUGH consulta as folhas das dimensões Loja, Produto e Tempo junto com a dimensão Lojas (o eixo de slicer) e, em seguida, retorna o grupo de medidas departamento, a identificação do departamento e o nome do funcionário.  
  
```  
DRILLTHROUGH  
Select {Leaves(Store), Leaves(Product), Leaves(Time),*} on 0  
From Stores  
RETURN [Department MeasureGroup].[Department Id], [Employee].[First Name]  
```  
  
## <a name="see-also"></a>Consulte também  
 [Manipulando dados &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-data-manipulation-manipulating-data.md)  
  
  

