---
title: "Usando DRILLTHROUGH para recuperar a fonte de dados (MDX) | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Instrução DRILLTHROUGH"
  - "recuperando dados"
  - "consultas [MDX], instrução DRILLTHROUGH"
  - "recuperação de dados [MDX]"
ms.assetid: fe0ab170-25a9-45a8-a377-f71a67f77018
caps.latest.revision: 30
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Usando DRILLTHROUGH para recuperar a fonte de dados (MDX)
  As expressões multidimensionais (MDX) usam a instrução [DRILLTHROUGH](../Topic/DRILLTHROUGH%20Statement%20\(MDX\).md) para recuperar um conjunto de linhas dos dados de origem de uma célula de cubo.  
  
 Para executar uma instrução **DRILLTHROUGH** em um cubo, uma ação de drillthrough deve ser definida para esse cubo. Para definir a ação de drillthrough, no [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)], no Designer de Cubo, no painel **Ações**, na barra de ferramentas, clique em **Nova Ação de Drillthrough**. Na nova ação de drillthrough, especifique o nome da ação, o destino, a condição e as colunas que serão retornadas pela instrução **DRILLTHROUGH**.  
  
## Sintaxe da instrução DRILLTHROUGH  
 A instrução **DRILLTHROUGH** utiliza esta sintaxe:  
  
```  
<drillthrough> ::= DRILLTHROUGH [<Max_Rows>] [<First_Rowset>] <MDX select> [<Return_Columns>]  
   < Max_Rows> ::= MAXROWS <positive number>  
   <First_Rowset> ::= FIRSTROWSET <positive number>  
   <Return_Columns> ::= RETURN <member or attribute> [, <member or attribute>]  
```  
  
 A cláusula **SELECT** identifica a célula de cubo que contém os dados de origem que serão recuperados. Essa cláusula **SELECT** é igual a uma instrução MDX **SELECT** comum, com exceção de que, na cláusula **SELECT**, apenas um membro pode ser especificado em cada eixo. Se mais de um membro for especificado em um eixo, ocorrerá um erro.  
  
 A sintaxe de `<Max_Rows>` especifica o número de máximo de linhas em cada conjunto de linhas retornado. Se o provedor OLE DB usado para estabelecer a conexão com a fonte de dados não oferecer suporte a **DBPRP_MAXROWS**, a configuração `<Max_Rows>` será ignorada.  
  
 A sintaxe de `<First_Rowset>` identifica a partição cujo conjunto de linhas será retornado primeiro.  
  
 A sintaxe de `<Return_Columns>` identifica as colunas do banco de dados subjacente que serão retornadas.  
  
## Exemplo da instrução DRILLTHROUGH  
 O exemplo a seguir demonstra o uso da instrução **DRILLTHROUGH**. Nesse exemplo, a instrução DRILLTHROUGH consulta as folhas das dimensões Loja, Produto e Tempo junto com a dimensão Lojas (o eixo de slicer) e, em seguida, retorna o grupo de medidas departamento, a identificação do departamento e o nome do funcionário.  
  
```  
DRILLTHROUGH  
Select {Leaves(Store), Leaves(Product), Leaves(Time),*} on 0  
From Stores  
RETURN [Department MeasureGroup].[Department Id], [Employee].[First Name]  
```  
  
## Consulte também  
 [Manipulando dados &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/manipulating-data-mdx.md)  
  
  