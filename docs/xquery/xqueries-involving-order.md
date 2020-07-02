---
title: XQueries envolvendo a ordem | Microsoft Docs
description: Exibir exemplos de XQueries que se baseiam na sequência em que os nós aparecem em um documento.
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- sequence [XQuery]
- XQuery, sequence
- ordered expressions [XQuery]
ms.assetid: 4f1266c5-93d7-402d-94ed-43f69494c04b
author: rothja
ms.author: jroth
ms.openlocfilehash: 1171740ae04b4fc03609659fa27a711bf36fa6f0
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85775448"
---
# <a name="xqueries-involving-order"></a>XQueries que envolvem ordem
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  Bancos de dados relacionais não têm um conceito de sequência. Por exemplo, você não pode fazer uma solicitação como "Obtenha o primeiro cliente do banco de dados". No entanto, você pode consultar um documento XML e recuperar o primeiro \<Customer> elemento. Então, você sempre recuperará o mesmo cliente.  
  
 Este tópico ilustra consultas baseadas na sequência em que os nós aparecem no documento.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-retrieve-manufacturing-steps-at-the-second-work-center-location-for-a-product"></a>a. Recuperar as etapas de fabricação no segundo local do centro de trabalho de um produto  
 Para um modelo de produto específico, a consulta a seguir recupera as etapas de produção no segundo centro de trabalho em uma sequência de locais de centro de trabalho no processo de produção.  
  
```sql
SELECT Instructions.query('  
     declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
    <ManuStep ProdModelID = "{sql:column("Production.ProductModel.ProductModelID")}"  
                ProductModelName = "{ sql:column("Production.ProductModel.Name") }" >  
     <Location>  
       { (//AWMI:root/AWMI:Location)[2]/@* }  
       <Steps>  
         { for $s in (//AWMI:root/AWMI:Location)[2]//AWMI:step  
           return  
              <Step>  
               { string($s) }  
              </Step>  
         }  
        </Steps>  
      </Location>  
     </ManuStep>  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 Observe o seguinte na consulta anterior:  
  
-   As expressões nas chaves são substituídas pelo resultado de sua avaliação. Para obter mais informações, consulte [construção XML &#40;XQuery&#41;](../xquery/xml-construction-xquery.md).  
  
-   **@\*** Recupera todos os atributos do segundo local do centro de trabalho.  
  
-   A iteração FLWOR (para... RETORNAR) recupera todos os <`step`> elementos filho do segundo local do centro de trabalho.  
  
-   A [função SQL: Column () (XQuery)](../xquery/xquery-extension-functions-sql-column.md) inclui o valor relacional no XML que está sendo construído.  
  
 Este é o resultado:  
  
```  
<ManuStep ProdModelID="7" ProductModelName="HL Touring Frame">  
  <Location LocationID="20" SetupHours="0.15"   
              MachineHours="2"  LaborHours="1.75" LotSize="1">  
  <Steps>  
   <Step>Assemble all frame components following blueprint 1299.</Step>  
     ...  
  </Steps>  
 </Location>  
</ManuStep>    
```  
  
 A consulta anterior recupera apenas os nós de texto. Se você quiser que todo o <`step`> elemento retornado, remova a função **String ()** da consulta:  
  
### <a name="b-find-all-the-material-and-tools-used-at-the-second-work-center-location-in-the-manufacturing-of-a-product"></a>B. Localizar todos os materiais e ferramentas usados no segundo local do centro de trabalho na fabricação de um produto  
 Para um modelo de produto específico, a consulta a seguir recupera as ferramentas e os materiais usados no segundo centro de trabalho na sequência de locais de centro de trabalho no processo de produção.  
  
```sql
SELECT Instructions.query('  
    declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
   <Location>  
      { (//AWMI:root/AWMI:Location)[1]/@* }  
       <Tools>  
         { for $s in (//AWMI:root/AWMI:Location)[1]//AWMI:step//AWMI:tool  
           return  
              <Tool>  
                { string($s) }  
              </Tool>  
          }  
        </Tools>  
        <Materials>  
            { for $s in (//AWMI:root/AWMI:Location)[1]//AWMI:step//AWMI:material  
              return  
                 <Material>  
                    { string($s) }  
                 </Material>  
             }  
         </Materials>  
  </Location>  
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 Observe o seguinte na consulta anterior:  
  
-   A consulta constrói o elemento <localizável `tion`> e recupera seus valores de atributo do banco de dados.  
  
-   Ela usa duas iterações FLWOR (for...return): uma para recuperar ferramentas e outra para recuperar o material usado.  
  
 Este é o resultado:  
  
```xml
<Location LocationID="10" SetupHours=".5"   
          MachineHours="3" LaborHours="2.5" LotSize="100">  
  <Tools>  
    <Tool>T-85A framing tool</Tool>  
    <Tool>Trim Jig TJ-26</Tool>  
    <Tool>router with a carbide tip 15</Tool>  
    <Tool>Forming Tool FT-15</Tool>  
  </Tools>  
  <Materials>  
    <Material>aluminum sheet MS-2341</Material>  
  </Materials>  
</Location>  
```  
  
### <a name="c-retrieve-the-first-two-product-feature-descriptions-from-the-product-catalog"></a>C. Recuperar as descrições dos dois primeiros recursos do produto no catálogo de produtos  
 Para um modelo de produto específico, a consulta recupera as duas primeiras descrições de recursos do `Features` elemento <> no catálogo de modelos do produto.  
  
```sql
SELECT CatalogDescription.query('  
     declare namespace p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     <ProductModel ProductModelID= "{ data( (/p1:ProductDescription/@ProductModelID)[1] ) }"  
                   ProductModelName = "{ data( (/p1:ProductDescription/@ProductModelName)[1] ) }" >  
       {  
         for $F in /p1:ProductDescription/p1:Features  
         return   
           $F/*[position() <= 2]   
       }  
     </ProductModel>  
      ') as x  
FROM Production.ProductModel  
where ProductModelID=19  
```  
  
 Observe o seguinte na consulta anterior:  
  
 O corpo da consulta constrói XML que inclui o `ProductModel` elemento <> que tem os atributos ProductModelID e ProductModelName.  
  
-   A consulta usa um para... Loop de retorno para recuperar as descrições de recursos do modelo de produto. A função **Position ()** é usada para recuperar os dois primeiros recursos.  
  
 Este é o resultado:  
  
```xml
<ProductModel ProductModelID="19" ProductModelName="Mountain 100">  
 <p1:Warranty   
  xmlns:p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
  <p1:WarrantyPeriod>3 year</p1:WarrantyPeriod>  
  <p1:Description>parts and labor</p1:Description>  
 </p1:Warranty>  
 <p2:Maintenance   
  xmlns:p2="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
  <p2:NoOfYears>10</p2:NoOfYears>  
  <p2:Description>maintenance contact available through your dealer   
            or any AdventureWorks retail store.  
  </p2:Description>  
 </p2:Maintenance>  
</ProductModel>   
```  
  
### <a name="d-find-the-first-two-tools-used-at-the-first-work-center-location-in-the-manufacturing-process-of-the-product"></a>D. Localizar as duas primeiras ferramentas usadas no primeiro local do centro de trabalho no processo de fabricação do produto  
 Para um modelo de produto, a consulta recupera as duas primeiras ferramentas no primeiro centro de trabalho na sequência de locais de centro de trabalho no processo de produção. A consulta é especificada em relação às instruções de fabricação armazenadas na coluna **instruções** da tabela **Production. ProductModel** .  
  
```sql
SELECT Instructions.query('  
     declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
   for $Inst in (//AWMI:root/AWMI:Location)[1]  
   return   
     <Location>  
       { $Inst/@* }  
       <Tools>  
         { for $s in ($Inst//AWMI:step//AWMI:tool)[position() <= 2]  
           return  
             <Tool>  
               { string($s) }  
             </Tool>  
         }  
       </Tools>  
     </Location>  
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 Este é o resultado:  
  
```xml
<Location LocationID="10" SetupHours=".5"   
            MachineHours="3" LaborHours="2.5" LotSize="100">  
  <Tools>  
    <Tool>T-85A framing tool</Tool>  
    <Tool>Trim Jig TJ-26</Tool>  
  </Tools>  
</Location>   
```  
  
### <a name="e-find-the-last-two-manufacturing-steps-at-the-first-work-center-location-in-the-manufacturing-of-a-specific-product"></a>E. Localizar as duas últimas etapas de fabricação no primeiro local do centro de trabalho no processo de fabricação de um produto específico  
 A consulta usa a função **Last ()** para recuperar as duas últimas etapas de fabricação.  
  
```sql
SELECT Instructions.query('   
declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
  <LastTwoManuSteps>  
   <Last-1Step>   
     { (/AWMI:root/AWMI:Location)[1]/AWMI:step[(last()-1)]/text() }  
   </Last-1Step>  
   <LastStep>   
     { (/AWMI:root/AWMI:Location)[1]/AWMI:step[last()]/text() }  
   </LastStep>  
  </LastTwoManuSteps>') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 Este é o resultado:  
  
```xml
<LastTwoManuSteps>  
   <Last-1Step>When finished, inspect the forms for defects per   
               Inspection Specification .</Last-1Step>  
   <LastStep>Remove the frames from the tool and place them in the   
             Completed or Rejected bin as appropriate.</LastStep>  
</LastTwoManuSteps>  
```  
  
## <a name="see-also"></a>Consulte Também  
 [&#40;de dados XML SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)   
 [Referência de linguagem XQuery &#40;SQL Server&#41;](../xquery/xquery-language-reference-sql-server.md)   
 [Construção XML &#40;&#41;XQuery](../xquery/xml-construction-xquery.md)  
  
  
