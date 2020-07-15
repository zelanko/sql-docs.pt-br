---
title: Heurística do modo AUTO na formação do XML retornado | Microsoft Docs
description: Saiba como usar a heurística de modo AUTO com a cláusula FOR XML para comparar valores de coluna em linhas adjacentes e determinar a forma do XML retornado por uma consulta.
ms.custom: fresh2019may
ms.date: 04/03/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- AUTO FOR XML mode, heuristics in shaping returned XML
ms.assetid: 6c5cb6c1-2921-4ba1-8100-0bf8074f9103
author: RothJa
ms.author: jroth
ms.openlocfilehash: 99a1858ce4784c9a320258689827110e0df3dd8e
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84529374"
---
# <a name="auto-mode-heuristics-in-shaping-returned-xml"></a>Heurística de modo AUTO na formação do XML retornado

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

O modo AUTO determina a forma do  XML retornado com base na consulta. Para determinar como os elementos devem ser aninhados, a heurística do modo AUTO compara valores da coluna em linhas adjacentes. São comparadas colunas de todos os tipos, menos **ntext**, **text**, **image**e **xml**. São comparadas colunas do tipo **(n)varchar(max)** e **varbinary(max)** .  
  
 O exemplo seguinte ilustra a heurística do modo AUTO que determina a forma do XML resultante:  
  
```sql
SELECT T1.Id, T2.Id, T1.Name  
FROM   T1, T2  
WHERE ...  
ORDER BY T1.Id
FOR XML AUTO;
```  
  
 Para determinar o local em que um novo elemento <`T1`> começa, todos os valores de T1 da coluna, exceto **ntext**, **text**, **image** r **xml**, serão comparados se a chave na tabela T1 não for especificada. Em seguida, assuma que a coluna **Name** é **nvarchar(40)** e a instrução SELECT retornará este conjunto de linhas:  
  
```  
T1.Id  T1.Name  T2.Id  
-----------------------  
1       Andrew    2  
1       Andrew    3  
1       Nancy     4  
```  
  
 A heurística do modo AUTO compara todos os valores da tabela T1 e as colunas Name e Id. Como as duas primeiras linhas têm os mesmos valores para as colunas ID e Nome, um elemento \<T1> com dois elementos filho \<T2> é adicionado ao resultado.  
  
 O XML retornado é o seguinte:  
  
```xml
<T1 Id="1" Name="Andrew">  
    <T2 Id="2" />  
    <T2 Id="3" />  
</T1>  
<T1 Id="1" Name="Nancy" >  
      <T2 Id="4" />  
</T>  
```  
  
 Agora assuma que a coluna Name é de tipo **text** . A heurística de modo AUTO não compara valores desse tipo. Em vez disso, ela assume que os valores não são os mesmos. Isso resulta em geração de XML conforme mostrado a seguir:  
  
```xml
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
  
## <a name="see-also"></a>Consulte Também  
 [Usar o modo AUTO com FOR XML](../../relational-databases/xml/use-auto-mode-with-for-xml.md)  
  
  
