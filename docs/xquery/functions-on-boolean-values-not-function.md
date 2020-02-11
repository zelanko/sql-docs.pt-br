---
title: Não função (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- effective Boolean value [XQuery]
- fn:not function
- not function [XQuery]
- EBV
ms.assetid: 93dfc377-45f1-4384-9392-560d9331a915
author: rothja
ms.author: jroth
ms.openlocfilehash: 8711190a6d3cbae0c716f7f62af478b70b9473e0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68038907"
---
# <a name="functions-on-boolean-values---not-function"></a>Funções em Valores Boolianos – função not 
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Retornará TRUE se o valor booliano efetivo de *$ARG* for false e retornará false se o valor booliano efetivo de *$ARG* for true.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
fn:not($arg as item()*) as xs:boolean  
```  
  
## <a name="arguments"></a>Argumentos  
 *$arg*  
 Uma sequência de itens para quais há um valor Booliano efetivo.  
  
## <a name="examples"></a>Exemplos  
 Este tópico fornece exemplos de XQuery em relação a instâncias XML que são armazenadas em várias colunas de tipo **XML** no banco de dados AdventureWorks.  
  
### <a name="a-using-the-not-xquery-function-to-find-product-models-whose-catalog-descriptions-do-not-include-the-specifications-element"></a>a. Usando a função not () XQuery para localizar modelos de produto cujas descrições de catálogo não incluem \<as especificações> elemento.  
 A consulta a seguir constrói XML que contém IDs de modelo de produto para modelos de produto cujas descrições de catálogo não `Specifications` incluem o elemento <>.  
  
```  
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
SELECT ProductModelID, CatalogDescription.query('  
       <Product   
           ProductModelID="{ sql:column("ProductModelID") }"  
        />  
') as Result  
FROM Production.ProductModel  
WHERE CatalogDescription.exist('  
     /pd:ProductDescription[not(pd:Specifications/*)]  '  
     ) = 0  
```  
  
 Observe o seguinte na consulta anterior:  
  
-   Como documento usa namespaces, a amostra usa a instrução WITH NAMESPACES. Outra opção é usar a palavra-chave **declare namespace** no [prólogo XQuery](../xquery/modules-and-prologs-xquery-prolog.md) para definir o prefixo.  
  
-   Em seguida, a consulta constrói o XML que inclui o `Product` elemento <> e seu atributo **ProductModelID** .  
  
-   A cláusula WHERE usa o [método exist () (tipo de dados XML)](../t-sql/xml/exist-method-xml-data-type.md) para filtrar as linhas. O método **exist ()** retornará true se houver elementos \<de> ProductDescription que não têm \<especificação> elementos filho. Observe o uso da função **not ()** .  
  
 Este conjunto de resultados está vazio, pois cada descrição do catálogo de modelos \<de produto inclui as especificações> elemento.  
  
### <a name="b-using-the-not-xquery-function-to-retrieve-work-center-locations-that-do-not-have-a-machinehours-attribute"></a>B. Usando a função not() XQuery para recuperar locais de centro de trabalho que não têm um atributo MachineHours  
 A consulta a seguir é especificada na coluna Instructions. Essa coluna armazena instruções de fabricação para os modelos de produtos.  
  
 Para um modelo de produto em particular, a consulta recupera locais de centro de trabalho que não especificam MachineHours. Ou seja, o atributo **MachineHours** não é especificado para o \<local> elemento.  
  
```  
SELECT ProductModelID, Instructions.query('  
declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions" ;  
     for $i in /AWMI:root/AWMI:Location[not(@MachineHours)]  
     return  
       <Location LocationID="{ $i/@LocationID }"   
                   LaborHrs="{ $i/@LaborHours }" >  
        </Location>  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7   
```  
  
 Na consulta anterior, observe o seguinte:  
  
-   O **declarenamespace** no [prólogo do XQuery](../xquery/modules-and-prologs-xquery-prolog.md) define o prefixo de namespace de instruções de fabricação da Adventure Works. Ela representa o mesmo namespace usado no documento de instruções de fabricação.  
  
-   Na consulta, o predicado **not (@MachineHours)** retornará true se não houver nenhum atributo **MachineHours** .  
  
 Este é o resultado:  
  
```  
ProductModelID Result   
-------------- --------------------------------------------  
7              <Location LocationID="30" LaborHrs="1"/>  
               <Location LocationID="50" LaborHrs="3"/>  
               <Location LocationID="60" LaborHrs="4"/>  
```  
  
### <a name="implementation-limitations"></a>Limitações de implementação  
 Estas são as limitações:  
  
-   A função **not ()** dá suporte apenas a argumentos do tipo xs: Boolean ou node () *, ou a sequência vazia.  
  
## <a name="see-also"></a>Consulte Também  
 [Funções XQuery em tipos de dados xml](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
