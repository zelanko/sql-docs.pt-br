---
title: Heurística do modo AUTO na formação do XML retornado | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- AUTO FOR XML mode, heuristics in shaping returned XML
ms.assetid: 6c5cb6c1-2921-4ba1-8100-0bf8074f9103
caps.latest.revision: 7
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: b05d8f71798071d3fef1e4e744ebdc8799c14d1f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36130921"
---
# <a name="auto-mode-heuristics-in-shaping-returned-xml"></a>Heurística de modo AUTO na formação do XML retornado
  O modo AUTO determina a forma do  XML retornado com base na consulta. Para determinar como os elementos devem ser aninhados, a heurística do modo AUTO compara valores da coluna em linhas adjacentes. São comparadas colunas de todos os tipos, menos **ntext**, **text**, **image**e **xml**. São comparadas colunas do tipo **(n)varchar(max)** e **varbinary(max)** .  
  
 O exemplo seguinte ilustra a heurística do modo AUTO que determina a forma do XML resultante:  
  
```  
SELECT T1.Id, T2.Id, T1.Name  
FROM   T1, T2  
WHERE ...  
FOR XML AUTO  
ORDER BY T1.Id  
```  
  
 Para determinar o local em que um novo elemento <`T1`> começa, todos os valores de T1 da coluna, exceto **ntext**, **text**, **image** r **xml**, serão comparados se a chave na tabela T1 não for especificada. Em seguida, assuma que a coluna **Name** é **nvarchar(40)** e a instrução SELECT retornará este conjunto de linhas:  
  
```  
T1.Id  T1.Name  T2.Id  
-----------------------  
1       Andrew    2  
1       Andrew    3  
1       Nancy     4  
```  
  
 A heurística do modo AUTO compara todos os valores da tabela T1 e as colunas Name e Id. Uma vez que as primeiras duas linhas têm os mesmos valores para as colunas Id e Nome, um elemento \<T1> com dois elementos filho \<T2> é adicionado ao resultado.  
  
 O XML retornado é o seguinte:  
  
```  
<T1 Id="1" Name="Andrew">  
    <T2 Id="2" />  
    <T2 Id="3" />  
</T1>  
<T1 Id="1" Name="Nancy" >  
      <T2 Id="4" />  
</T>  
```  
  
 Agora assuma que a coluna Name é de tipo **text** . A heurística de modo AUTO não compara valores desse tipo. Em vez disso, ela assume que os valores não são os mesmos. Isso resulta em geração de XML conforme mostrado a seguir:  
  
```  
<T1 Id="1" Name="Andrew" >  
  <T2 Id="2" />  
</T1>  
<T1 Id="1" Name="Andrew" >  
  <T2 Id="3" />  
</T1>  
<T1 Id="1" Name="Nancy" >  
  <T2 Id="4" />  
</T1>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Usar o modo AUTO com FOR XML](use-auto-mode-with-for-xml.md)  
  
  