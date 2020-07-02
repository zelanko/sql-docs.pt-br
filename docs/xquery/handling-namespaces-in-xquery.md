---
title: Manipulando namespaces no XQuery | Microsoft Docs
description: Veja exemplos de tratamento de namespaces em um XQuery que incluem como declarar namespaces novos e padrão.
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- declaring namespaces
- namespaces [XQuery]
- XQuery, namespaces
ms.assetid: 542b63da-4d3d-4ad5-acea-f577730688f1
author: rothja
ms.author: jroth
ms.openlocfilehash: 6a6f5a6dbe1db85dc5f25e9d68fa94dcd245e5a4
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85772924"
---
# <a name="handling-namespaces-in-xquery"></a>Manipulando namespaces em XQuery
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  Este tópico fornece exemplos para manipular namespaces em consultas.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-declaring-a-namespace"></a>a. Declarando um namespace  
 A consulta a seguir recupera as etapas do processo de produção de um modelo de produto específico.  
  
```  
SELECT Instructions.query('  
     declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
        /AWMI:root/AWMI:Location[1]/AWMI:step  
    ') as x  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 Este é o resultado parcial:  
  
```  
<AWMI:step xmlns:AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions">Insert <AWMI:material>aluminum sheet MS-2341</AWMI:material> into the <AWMI:tool>T-85A framing tool</AWMI:tool>. </AWMI:step>  
...  
```  
  
 Observe que a palavra-chave **namespace** é usada para definir um novo prefixo de namespace, "AWMI:". Esse prefixo deve, então, ser usado na consulta para todos os elementos que estejam dentro do escopo desse namespace.  
  
### <a name="b-declaring-a-default-namespace"></a>B. Declarando um namespace padrão  
 Na consulta anterior, um novo prefixo de namespace foi definido. Depois, esse prefixo teve de ser usado na consulta para selecionar as estruturas XML planejadas. Alternativamente, você pode declarar um namespace como o namespace padrão, como mostrado na seguinte consulta modificada:  
  
```  
SELECT Instructions.query('  
     declare default element namespace "https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
        /root/Location[1]/step  
    ') as x  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 Este será o resultado  
  
```  
<step xmlns="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions">Insert <material>aluminum sheet MS-2341</material> into the <tool>T-85A framing tool</tool>. </step>  
...  
```  
  
 Observe neste exemplo que o namespace definido, `"https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions"`, foi criado para anular o namespace padrão ou vazio. Por causa disso, você não tem mais um prefixo de namespace na expressão de caminho usada para a consulta. Você também não tem mais um prefixo de namespace nos nomes de elemento que aparecem nos resultados. Adicionalmente, o namespace padrão é aplicado a todos os elementos, mas não a seus atributos.  
  
### <a name="c-using-namespaces-in-xml-construction"></a>C. Usando namespaces na construção XML  
 Quando você definir novos namespaces, eles não só são trazidos no escopo para a consulta, mas para a construção. Por exemplo, na construção de XML, você pode definir um novo namespace usando a declaração “`declare namespace ...`” e depois usar esse namespace com qualquer elemento e atributo construído para que apareça nos resultados da consulta.  
  
```  
SELECT CatalogDescription.query('  
     declare default element namespace "https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     declare namespace myNS="uri:SomeNamespace";<myNS:Result>  
          { /ProductDescription/Summary }  
       </myNS:Result>  
  
    ') as Result  
FROM Production.ProductModel  
where ProductModelID=19  
```  
  
 Este é o resultado:  
  
```  
  
      <myNS:Result xmlns:myNS="uri:SomeNamespace">  
  <Summary xmlns="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">  
   <p1:p xmlns:p1="http://www.w3.org/1999/xhtml">  
     Our top-of-the-line competition mountain bike. Performance-enhancing   
     options include the innovative HL Frame, super-smooth front   
     suspension, and traction for all terrain.</p1:p>  
  </Summary>  
</myNS:Result>  
```  
  
 Como alternativa, você também pode definir o namespace explicitamente em cada ponto em que ele for usado como parte da construção XML, como mostrado na consulta a seguir:  
  
```  
SELECT CatalogDescription.query('  
     declare default element namespace "https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
       <myNS:Result xmlns:myNS="uri:SomeNamespace">  
          { /ProductDescription/Summary }  
       </myNS:Result>  
    ') as Result  
FROM Production.ProductModel  
where ProductModelID=19  
```  
  
### <a name="d-construction-using-default-namespaces"></a>D. Construção com o uso de namespaces padrão  
 Você também pode definir um namespace padrão para uso em XML construído. Por exemplo, a consulta a seguir mostra como você pode especificar um namespace padrão, "URI: SomeNamespace" \\ , para usar como o padrão para os elementos nomeados localmente que são construídos, como o `<Result>` elemento.  
  
```  
SELECT CatalogDescription.query('  
      declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
      declare default element namespace "uri:SomeNamespace";<Result>  
          { /PD:ProductDescription/PD:Summary }  
       </Result>  
  
    ') as Result  
FROM Production.ProductModel  
where ProductModelID=19  
```  
  
 Este é o resultado:  
  
```  
  
      <Result xmlns="uri:SomeNamespace">  
  <PD:Summary xmlns:PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">  
   <p1:p xmlns:p1="http://www.w3.org/1999/xhtml">  
         Our top-of-the-line competition mountain bike. Performance-  
         enhancing options include the innovative HL Frame, super-smooth   
         front suspension, and traction for all terrain.</p1:p>  
  </PD:Summary>  
</Result>  
```  
  
 Observe que ao substituir o elemento namespace padrão ou namespace vazio, todos os elementos nomeados localmente no XML construído serão subsequentemente associados ao namespace padrão substituído. Portanto, se você precisar de flexibilidade na construção XML para aproveitar o namespace vazio, não substitua o elemento namespace padrão.  
  
## <a name="see-also"></a>Consulte Também  
 [Adicionar namespaces a consultas com WITH sqlnamespaces](../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)   
 [&#40;de dados XML SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)   
 [Referência de linguagem XQuery &#40;SQL Server&#41;](../xquery/xquery-language-reference-sql-server.md)  
  
  
