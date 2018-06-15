---
title: Usando DRILLTHROUGH para recuperar dados de origem (MDX) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 81c873d0ea6e5c21d97fc719ce1c72a773df43e5
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34027506"
---
# <a name="mdx-data-manipulation---retrieve-source-data-using-drillthrough"></a>Manipulação de dados MDX - recuperar dados de origem usando o DETALHAMENTO
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
 [Manipulação de dados & #40; MDX & #41;](../../../analysis-services/multidimensional-models/mdx/mdx-data-manipulation-manipulating-data.md)  
  
  
