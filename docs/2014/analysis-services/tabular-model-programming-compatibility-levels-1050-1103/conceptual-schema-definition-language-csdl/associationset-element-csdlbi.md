---
title: Elemento AssociationSet (CSDLBI) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 93e5ac4d-d7e8-490e-b775-28263a48cfcc
caps.latest.revision: 8
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7d418e75aa451c14db6010f6cb3673cd8c3a74bc
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37229556"
---
# <a name="associationset-element-csdlbi"></a>Elemento AssociationSet (CSDLBI)
  O elemento `AssociationSet` é um tipo complexo que define uma associação. Em um modelo de dados da CSDLBI, uma associação é uma relação entre duas tabelas.  
  
 Um `AssociationSet` deve ser especificado para cada relação exclusiva em um modelo. O `AssociationSet` define os pontos de extremidade usando o elemento `Association`. O elemento `AssociationSet` também define os metadados sobre a relação e seu uso no modelo de dados.  
  
## <a name="applicable-attributes"></a>Atributos aplicáveis  
 A tabela a seguir lista os elementos e atributos que definem o elemento `AssociationSet`.  
  
|Nome|É obrigatório|Description|  
|----------|-----------------|-----------------|  
|Estado|Sim|Uma cadeia de caracteres que indica se a associação está ativa ou não. O valor é definido pelo elemento State.|  
|Hidden|não|Um valor booliano que indica se a relação está visível. Por padrão, o valor de Hidden é `false`, o que significa que todas as relações ficam visíveis no modelo.|  
  
## <a name="state-element"></a>Elemento State  
 O elemento `State` é um tipo simples que descreve se uma associação está ativa, e deve ser usada em cálculos, ou se ela está inativa, e deve ser explicitamente referenciada nos cálculos.  
  
 Se houver vários conjuntos de associações conectando duas entidade, apenas um conjunto de associações poderá ser marcado como Ativo. Em outras palavras, se houver duas relações entre as duas mesmas tabelas, somente uma relação poderá estar ativa.  
  
 A tabela a seguir lista os valores do elemento `State`.  
  
|Valor|Description|  
|-----------|-----------------|  
|Ativa|A associação está ativa.|  
|Inativa|A associação está ativa.|  
  
## <a name="example"></a>Exemplo  
 **Tabular**  
  
 O exemplo a seguir mostra uma relação no modelo de tabela da AdventureWorks (na versão 1.1 da CSDLBI). A associação é marcada como Inactive, pois existe uma relação (entre OrderKey e Date).  
  
```  
<AssociationSet   
    Name="InternetSales_Date_Date_Date"  
    Association="Sandbox.InternetSales_Date_Date_Date">  
    <End EntitySet="InternetSales" />  
    <End EntitySet="DimDate" />  
<bi:AssociationSet State="Inactive" />  
</AssociationSet>  
  
```  
  
## <a name="example"></a>Exemplo  
 **Multidimensional**  
  
 O exemplo a seguir mostra a relação que é definida entre as tabelas Sales e Currency, no cubo Operações da Contoso.  
  
```  
<AssociationSet   
    Name ="Sales_Currency_Currency_Currency_Name2"  
    Association ="Sandbox.Sales_Currency_Currency_Currency_Name2">  
    <End EntitySet ="Sales" />  
    <End EntitySet ="Currency" />  
<bi:AssociationSet />  
</AssociationSet>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência técnica para Anotações de BI para CSDL](technical-reference-for-bi-annotations-to-csdl.md)  
  
  
