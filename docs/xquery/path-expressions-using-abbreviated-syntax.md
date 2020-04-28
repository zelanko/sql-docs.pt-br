---
title: Usando a sintaxe abreviada em uma expressão de caminho | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- axis step [XQuery]
- abbreviated syntax [XQuery]
ms.assetid: f83c2e41-5722-47c3-b5b8-bf0f8cbe05d3
author: rothja
ms.author: jroth
ms.openlocfilehash: 8e75db08f283631cf9b5daf064790786a1abc10f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67946416"
---
# <a name="path-expressions---using-abbreviated-syntax"></a>Expressões de Caminho – Usar Sintaxe Abreviada
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Todos os exemplos em [entender as expressões de caminho no XQuery](../xquery/path-expressions-xquery.md) usam sintaxe não abreviada para expressões de caminho. A sintaxe não abreviada para uma etapa de eixo em uma expressão de caminho inclui o nome de eixo e teste de nó, separados por dois-pontos duplos e seguidos por zero ou mais qualificadores de etapa.  
  
 Por exemplo:  
  
```  
child::ProductDescription[attribute::ProductModelID=19]  
```  
  
 O XQuery oferece suporte para as abreviações a seguir para uso em expressões de caminho:  
  
-   O eixo **filho** é o eixo padrão. Portanto, o eixo **Child::** pode ser omitido de uma etapa em uma expressão. Por exemplo, `/child::ProductDescription/child::Summary` pode ser escrito como `/ProductDescription/Summary`.  
  
-   Um eixo de **atributo** pode ser abreviado @como. Por exemplo, `/child::ProductDescription[attribute::ProductModelID=10]` pode ser escrito como `/ProudctDescription[@ProductModelID=10]`.  
  
-   Um **/descendant-or-self:: node ()/** pode ser abreviado como//. Por exemplo, `/descendant-or-self::node()/child::act:telephoneNumber` pode ser escrito como `//act:telephoneNumber`.  
  
     A consulta anterior recupera todos os números de telefone armazenados na coluna AdditionalContactInfo na tabela Contact. O esquema para AdditionalContactInfo é definido de forma que um \<elemento de> de telephoneNumber possa aparecer em qualquer lugar do documento. Então, para recuperar todos os números de telefone, você deve pesquisar cada nó no documento. A pesquisa inicia na raiz do documento e continua por todos os nós descendentes.  
  
     A consulta a seguir recupera todos os números de telefone de um contato de cliente específico:  
  
    ```  
    SELECT AdditionalContactInfo.query('             
                declare namespace act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";             
                declare namespace crm="https://schemas.adventure-works.com/Contact/Record";             
                declare namespace ci="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo";             
                /descendant-or-self::node()/child::act:telephoneNumber             
                ') as result             
    FROM Person.Contact             
    WHERE ContactID=1             
    ```  
  
     Se você substituir a expressão de caminho com a sintaxe abreviada, `//act:telephoneNumber`, receberá os mesmos resultados.  
  
-   O **próprio: node ()** em uma etapa pode ser abreviado para um único ponto (.). No entanto, o ponto não é equivalente ou intercambiável com o **próprio nó:: ()**.  
  
     Por exemplo, na consulta a seguir, o uso de um ponto representa um valor e não um nó:  
  
    ```  
    ("abc", "cde")[. > "b"]  
    ```  
  
-   O **pai:: node ()** em uma etapa pode ser abreviado como um ponto duplo (..).  
  
  
