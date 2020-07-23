---
title: Função Position (XQuery) | Microsoft Docs
description: Saiba mais sobre a posição da função XQuery () que retorna um valor inteiro que indica a posição de um item de contexto dentro de uma sequência de itens.
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- position function
- fn:position function
ms.assetid: f1bab9e4-1715-4c06-9cb0-06c7e0c9c97f
author: rothja
ms.author: jroth
ms.openlocfilehash: 83f744f2b9361a81afada82245bf2d4265cea833
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86923622"
---
# <a name="context-functions---position-xquery"></a>Funções de Contexto – position (XQuery)
[!INCLUDE[sqlserver](../includes/applies-to-version/sqlserver.md)]

  Retorna um valor inteiro que indica a posição do item de contexto na sequência de itens que estão sendo processados atualmente.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
fn:position() as xs:integer  
```  
  
## <a name="remarks"></a>Comentários  
 Em [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , **fn: Position ()** só pode ser usada no contexto de um predicado dependente de contexto. Especificamente, ele só pode ser usado entre parênteses ([ ]). A comparação contra essa função não reduz a cardinalidade durante a inferência de tipo estática.  
  
## <a name="examples"></a>Exemplos  
 Este tópico fornece exemplos de XQuery em relação a instâncias XML que são armazenadas em várias colunas de tipo **XML** no [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] banco de dados.  
  
### <a name="a-using-the-position-xquery-function-to-retrieve-the-first-two-product-features"></a>a. Usando a função position() XQuery para recuperar os primeiros dois recursos de produto  
 A consulta a seguir recupera os dois primeiros recursos, os dois primeiros elementos filho do `Features` elemento <>, da descrição do catálogo de modelos do produto. Se houver mais recursos, ele adicionará um `there-is-more/` elemento <> ao resultado.  
  
```  
SELECT CatalogDescription.query('  
     declare namespace pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     <Product>   
          { /pd:ProductDescription/@ProductModelID }  
          { /pd:ProductDescription/@ProductModelName }   
          {  
            for $f in /pd:ProductDescription/pd:Features/*[position()<=2]  
            return  
            $f   
          }  
          {  
            if (count(/pd:ProductDescription/pd:Features/*) > 2)  
            then <there-is-more/>  
            else ()  
          }   
     </Product>          
') as x  
FROM Production.ProductModel  
WHERE CatalogDescription is not null  
```  
  
 Observe o seguinte na consulta anterior:  
  
-   A palavra-chave **namespace** no [prólogo XQuery](../xquery/modules-and-prologs-xquery-prolog.md) define um prefixo de namespace que é usado no corpo da consulta.  
  
-   O corpo da consulta constrói XML que tem um \<Product> elemento com os atributos **ProductModelID** e **ProductModelName** e tem recursos do produto retornados como elementos filho.  
  
-   A função **Position ()** é usada no predicado para determinar a posição do \<Features> elemento filho no contexto. Se ele for o primeiro ou segundo recurso, será retornado.  
  
-   A instrução IF adiciona um \<there-is-more/> elemento ao resultado se houver mais de dois recursos no catálogo de produtos.  
  
-   Como nem todos os modelos de produtos têm as descrições de catálogo armazenadas na tabela, a cláusula WHERE é usada para descartar linhas em que CatalogDescriptions é NULL.  
  
 Este é um resultado parcial:  
  
```  
<Product ProductModelID="19" ProductModelName="Mountain 100">  
  <p1:Warranty xmlns:p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    <p1:WarrantyPeriod>3 year</p1:WarrantyPeriod>  
    <p1:Description>parts and labor</p1:Description>  
  </p1:Warranty>  
  <p2:Maintenance xmlns:p2="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    <p2:NoOfYears>10</p2:NoOfYears>  
    <p2:Description>maintenance contact available through your dealer or  
                    any AdventureWorks retail store.</p2:Description>  
  </p2:Maintenance>  
  <there-is-more/>  
</Product>   
...  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Funções XQuery em tipos de dados xml](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
