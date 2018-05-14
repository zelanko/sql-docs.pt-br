---
title: Elemento AssociationSet (CSDLBI) | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c2ae4f565a2383284421bb433ed5cc98371196d3
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="associationset-element-csdlbi"></a>Elemento AssociationSet (CSDLBI)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  O elemento **AssociationSet** é um tipo complexo que define uma associação. Em um modelo de dados da CSDLBI, uma associação é uma relação entre duas tabelas.  
  
 Um **AssociationSet** deve ser especificado para cada relação exclusiva em um modelo. O **AssociationSet** define os pontos de extremidade usando o elemento **Association** . O elemento **AssociationSet** também define os metadados sobre a relação e seu uso no modelo de dados.  
  
## <a name="applicable-attributes"></a>Atributos aplicáveis  
 A tabela a seguir lista os elementos e atributos que definem o elemento **AssociationSet** .  
  
|Nome|É obrigatório|Descrição|  
|----------|-----------------|-----------------|  
|Estado|Sim|Uma cadeia de caracteres que indica se a associação está ativa ou não. O valor é definido pelo elemento State.|  
|Oculto|Não|Um valor booliano que indica se a relação está visível. Por padrão, o valor de Hidden é **false**, o que significa que todas as relações ficam visíveis no modelo.|  
  
## <a name="state-element"></a>Elemento State  
 O elemento **State** é um tipo simples que descreve se uma associação está ativa, e deve ser usada em cálculos, ou se ela está inativa, e deve ser explicitamente referenciada nos cálculos.  
  
 Se houver vários conjuntos de associações conectando duas entidade, apenas um conjunto de associações poderá ser marcado como Ativo. Em outras palavras, se houver duas relações entre as duas mesmas tabelas, somente uma relação poderá estar ativa.  
  
 A tabela a seguir lista os valores do elemento **State** .  
  
|Value|Descrição|  
|-----------|-----------------|  
|Ativa|A associação está ativa.|  
|Inativa|A associação está ativa.|  
  
## <a name="example"></a>Exemplo  
 **Tabela**  
  
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
 [Referência técnica para anotações de BI para CSDL](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/technical-reference-for-bi-annotations-to-csdl.md)  
  
  
