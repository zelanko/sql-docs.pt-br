---
title: Manipulando Namespaces em XQuery | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: sql
ms.component: xquery
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- declaring namespaces
- namespaces [XQuery]
- XQuery, namespaces
ms.assetid: 542b63da-4d3d-4ad5-acea-f577730688f1
caps.latest.revision: 24
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 4602c1234c00b15191ca616ed56352f0eb784d9a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="handling-namespaces-in-xquery"></a>Manipulando namespaces em XQuery
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Este tópico fornece exemplos para manipular namespaces em consultas.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-declaring-a-namespace"></a>A. Declarando um namespace  
 A consulta a seguir recupera as etapas do processo de produção de um modelo de produto específico.  
  
```  
SELECT Instructions.query('  
     declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
        /AWMI:root/AWMI:Location[1]/AWMI:step  
    ') as x  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 Este é o resultado parcial:  
  
```  
<AWMI:step xmlns:AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions">Insert <AWMI:material>aluminum sheet MS-2341</AWMI:material> into the <AWMI:tool>T-85A framing tool</AWMI:tool>. </AWMI:step>  
…  
```  
  
 Observe que o **namespace** palavra-chave é usada para definir um novo prefixo de namespace, "AWMI:". Esse prefixo deve, então, ser usado na consulta para todos os elementos que estejam dentro do escopo desse namespace.  
  
### <a name="b-declaring-a-default-namespace"></a>B. Declarando um namespace padrão  
 Na consulta anterior, um novo prefixo de namespace foi definido. Depois, esse prefixo teve de ser usado na consulta para selecionar as estruturas XML planejadas. Alternativamente, você pode declarar um namespace como o namespace padrão, como mostrado na seguinte consulta modificada:  
  
```  
SELECT Instructions.query('  
     declare default element namespace "http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
        /root/Location[1]/step  
    ') as x  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 Este será o resultado  
  
```  
<step xmlns="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions">Insert <material>aluminum sheet MS-2341</material> into the <tool>T-85A framing tool</tool>. </step>  
…  
```  
  
 Observe neste exemplo que o namespace definido, `"http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions"`, foi criado para anular o namespace padrão ou vazio. Por causa disso, você não tem mais um prefixo de namespace na expressão de caminho usada para a consulta. Você também não tem mais um prefixo de namespace nos nomes de elemento que aparecem nos resultados. Adicionalmente, o namespace padrão é aplicado a todos os elementos, mas não a seus atributos.  
  
### <a name="c-using-namespaces-in-xml-construction"></a>C. Usando namespaces na construção XML  
 Quando você definir novos namespaces, eles não só são trazidos no escopo para a consulta, mas para a construção. Por exemplo, na construção de XML, você pode definir um novo namespace usando a declaração “`declare namespace ...`” e depois usar esse namespace com qualquer elemento e atributo construído para que apareça nos resultados da consulta.  
  
```  
SELECT CatalogDescription.query('  
     declare default element namespace "http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
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
  <Summary xmlns="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">  
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
     declare default element namespace "http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
       <myNS:Result xmlns:myNS="uri:SomeNamespace">  
          { /ProductDescription/Summary }  
       </myNS:Result>  
    ') as Result  
FROM Production.ProductModel  
where ProductModelID=19  
```  
  
### <a name="d-construction-using-default-namespaces"></a>D. Construção com o uso de namespaces padrão  
 Você também pode definir um namespace padrão para uso em XML construído. Por exemplo, a consulta a seguir mostra como você pode especificar um namespace padrão, "URI: SomeNameSpace"\\, para usar como padrão para os elementos nomeados localmente que sejam construídos, como o `<Result>` elemento.  
  
```  
SELECT CatalogDescription.query('  
      declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
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
  <PD:Summary xmlns:PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">  
   <p1:p xmlns:p1="http://www.w3.org/1999/xhtml">  
         Our top-of-the-line competition mountain bike. Performance-  
         enhancing options include the innovative HL Frame, super-smooth   
         front suspension, and traction for all terrain.</p1:p>  
  </PD:Summary>  
</Result>  
```  
  
 Observe que ao substituir o elemento namespace padrão ou namespace vazio, todos os elementos nomeados localmente no XML construído serão subsequentemente associados ao namespace padrão substituído. Portanto, se você precisar de flexibilidade na construção XML para aproveitar o namespace vazio, não substitua o elemento namespace padrão.  
  
## <a name="see-also"></a>Consulte também  
 [Adicionar namespaces a consultas com WITH XMLNAMESPACES](../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)   
 [Dados XML &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)   
 [Referência de linguagem XQuery &#40;SQL Server&#41;](../xquery/xquery-language-reference-sql-server.md)  
  
  
