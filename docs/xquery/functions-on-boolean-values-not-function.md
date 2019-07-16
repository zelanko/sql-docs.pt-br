---
title: Função not (XQuery) | Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68038907"
---
# <a name="functions-on-boolean-values---not-function"></a>Funções em Valores Boolianos – função not 
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Retorna VERDADEIRO se o valor booliano efetivo de *$arg* é false e retornará FALSE se o valor booliano efetivo da *$arg* é verdadeiro.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
fn:not($arg as item()*) as xs:boolean  
```  
  
## <a name="arguments"></a>Argumentos  
 *$arg*  
 Uma sequência de itens para quais há um valor Booliano efetivo.  
  
## <a name="examples"></a>Exemplos  
 Este tópico fornece exemplos de XQuery contra instâncias XML armazenadas em várias **xml** colunas de tipo de banco de dados AdventureWorks.  
  
### <a name="a-using-the-not-xquery-function-to-find-product-models-whose-catalog-descriptions-do-not-include-the-specifications-element"></a>A. Usando a função XQuery de not () para localizar modelos de produto cujas descrições de catálogo não incluem o \<especificações > elemento.  
 A consulta a seguir constrói XML que contém as IDs de modelo de produto para modelos de produto cujas descrições de catálogo não incluem o <`Specifications`> elemento.  
  
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
  
-   Como documento usa namespaces, a amostra usa a instrução WITH NAMESPACES. Outra opção é usar o **declarar o namespace** palavra-chave na [prólogo do XQuery](../xquery/modules-and-prologs-xquery-prolog.md) para definir o prefixo.  
  
-   A consulta então constrói o XML que inclui o <`Product`> elemento e seu **ProductModelID** atributo.  
  
-   A cláusula WHERE usa o [método exist () (tipo de dados XML)](../t-sql/xml/exist-method-xml-data-type.md) para filtrar as linhas. O **exist ()** método retornará True se houver \<ProductDescription > elementos que não têm \<especificação > elementos filho. Observe o uso do **not ()** função.  
  
 Esse conjunto de resultados está vazio, porque cada descrição de catálogo do modelo de produto inclui o \<especificações > elemento.  
  
### <a name="b-using-the-not-xquery-function-to-retrieve-work-center-locations-that-do-not-have-a-machinehours-attribute"></a>B. Usando a função not() XQuery para recuperar locais de centro de trabalho que não têm um atributo MachineHours  
 A consulta a seguir é especificada na coluna Instructions. Essa coluna armazena instruções de fabricação para os modelos de produtos.  
  
 Para um modelo de produto em particular, a consulta recupera locais de centro de trabalho que não especificam MachineHours. Ou seja, o atributo **MachineHours** não for especificado para o \<local > elemento.  
  
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
  
-   O **declarenamespace** na [prólogo do XQuery](../xquery/modules-and-prologs-xquery-prolog.md) define o prefixo de namespace de instruções de fabricação do Adventure Works. Ela representa o mesmo namespace usado no documento de instruções de fabricação.  
  
-   Na consulta, o **não (@MachineHours)** predicado retornar True se não houver nenhuma **MachineHours** atributo.  
  
 Esse é o resultado:  
  
```  
ProductModelID Result   
-------------- --------------------------------------------  
7              <Location LocationID="30" LaborHrs="1"/>  
               <Location LocationID="50" LaborHrs="3"/>  
               <Location LocationID="60" LaborHrs="4"/>  
```  
  
### <a name="implementation-limitations"></a>Limitações de implementação  
 Estas são as limitações:  
  
-   O **not ()** função só dá suporte a argumentos de tipo xs: Boolean ou Node () * ou a sequência vazia.  
  
## <a name="see-also"></a>Consulte também  
 [Funções XQuery em Tipos de Dados XML](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
