---
title: Id Function (XQuery) | Microsoft Docs
description: Aprenda a usar a função de identificação XQuery para retornar uma seqüência de elementos na instância XML, em ordem de documento, com os valores xs:IDREF fornecidos.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- fn:id function
- id function
ms.assetid: de99fc60-d0ad-4117-a17d-02bdde6512b4
author: rothja
ms.author: jroth
ms.openlocfilehash: 45b7f9f7ee9fa301b10c29fafb663c3a307509d7
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/15/2020
ms.locfileid: "81388511"
---
# <a name="functions-on-sequences---id"></a>Funções em Sequências – ID
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Retorna a seqüência de nós de elemento com valores xs:ID que correspondem aos valores de um ou mais dos valores xs:IDREF fornecidos em *$arg*.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
fn:id($arg as xs:IDREF*) as element()*  
```  
  
## <a name="arguments"></a>Argumentos  
 *$arg*  
 Um ou mais valores xs:IDREF.  
  
## <a name="remarks"></a>Comentários  
 O resultado da função é uma sequência de elementos na instância XML, na ordem do documento, que tem um valor xs:ID igual a um ou mais dos xs:IDREFs na lista de xs:IDREFs candidatos.  
  
 Se o valor xs:IDREF não corresponder a qualquer elemento, a função retornará a sequência vazia.  
  
## <a name="examples"></a>Exemplos  
 Este tópico fornece exemplos de XQuery contra instâncias XML armazenadas [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] em várias colunas do tipo **xml** no banco de dados.  
  
### <a name="a-retrieving-elements-based-on-the-idref-attribute-value"></a>a. Recuperando elementos com base no valor do atributo IDREF  
 O exemplo a seguir usa fn:id para recuperar o <`employee`> elementos, com base no atributo do gerenciador IDREF. Neste exemplo, o atributo gerente é um atributo do tipo IDREF e o atributo eid é um atributo do tipo do ID.  
  
 Para um valor de atributo de gerente específico, a função **id()** encontra o elemento <`employee`> cujo valor de atributo do tipo DeD corresponde ao valor de IDREF de entrada. Em outras palavras, para um funcionário específico, a função **de id()** retorna o gerente do funcionário.  
  
 Isso é o que ocorre no exemplo:  
  
-   Uma coleção de esquemas XML é criada.  
  
-   Uma variável **xml** digitada é criada usando a coleção de esquemas XML.  
  
-   A consulta recupera o elemento que tem um valor de atributo ID `employee` referenciado pelo atributo IDREF do **<** elemento>.  
  
```  
-- If exists, drop the XML schema collection (SC).  
-- drop xml schema collection SC  
-- go  
  
create xml schema collection SC as  
'<schema xmlns="http://www.w3.org/2001/XMLSchema" xmlns:e="emp" targetNamespace="emp">  
            <element name="employees" type="e:EmployeesType"/>  
            <complexType name="EmployeesType">  
                 <sequence>  
                      <element name="employee" type="e:EmployeeType" minOccurs="0" maxOccurs="unbounded" />  
                 </sequence>  
            </complexType>    
  
            <complexType name="EmployeeType">  
                        <attribute name="eid" type="ID" />  
                        <attribute name="name" type="string" />  
                        <attribute name="manager" type="IDREF" />  
            </complexType>         
</schema>'  
go  
```  
  
```  
declare @x xml(SC)  
set @x='<e:employees xmlns:e="emp">  
<employee eid="e1" name="Joe" manager="e10" />  
<employee eid="e2" name="Bob" manager="e10" />  
<employee eid="e10" name="Dave" manager="e10" />  
</e:employees>'  
  
select @x.value(' declare namespace e="emp";   
 (fn:id(e:employees/employee[@name="Joe"]/@manager)/@name)[1]', 'varchar(50)')   
Go  
```  
  
 A consulta retorna "Dave" como o valor. Isso indica que Dave é o gerente de Joe.  
  
### <a name="b-retrieving-elements-based-on-the-orderlist-idrefs-attribute-value"></a>B. Recuperando elementos com base no valor do atributo IDREFS de OrderList  
 No exemplo a seguir, o atributo OrderList do elemento> <`Customer` é um atributo tipo IDREFS. Ele relaciona os ids de ordem desse cliente específico. Para cada id de pedido, há uma criança <`Order`> elemento sob o <`Customer`> fornecendo o valor do pedido.  
  
 A expressão de consulta, `data(CustOrders:Customers/Customer[1]/@OrderList)[1]`, recupera o primeiro valor da lista IDRES para o primeiro cliente. Esse valor é então passado para a função **id().** A função então `Order` encontra o elemento <> cujo valor do atributo OrderID corresponde à entrada à função **id().**  
  
```  
drop xml schema collection SC  
go  
create xml schema collection SC as  
'<schema xmlns="http://www.w3.org/2001/XMLSchema" xmlns:Customers="Customers" targetNamespace="Customers">  
            <element name="Customers" type="Customers:CustomersType"/>  
            <complexType name="CustomersType">  
                        <sequence>  
                            <element name="Customer" type="Customers:CustomerType" minOccurs="0" maxOccurs="unbounded" />  
                        </sequence>  
            </complexType>  
             <complexType name="OrderType">  
                <sequence minOccurs="0" maxOccurs="unbounded">  
                            <choice>  
                                <element name="OrderValue" type="integer" minOccurs="0" maxOccurs="unbounded"/>  
                            </choice>  
                </sequence>                                             
                <attribute name="OrderID" type="ID" />  
            </complexType>  
  
            <complexType name="CustomerType">  
                <sequence minOccurs="0" maxOccurs="unbounded">  
                            <choice>  
                                <element name="spouse" type="string" minOccurs="0" maxOccurs="unbounded"/>  
                                <element name="Order" type="Customers:OrderType" minOccurs="0" maxOccurs="unbounded"/>  
                            </choice>  
                </sequence>                                             
                <attribute name="CustomerID" type="string" />  
                <attribute name="OrderList" type="IDREFS" />  
            </complexType>  
 </schema>'  
go  
declare @x xml(SC)  
set @x='<CustOrders:Customers xmlns:CustOrders="Customers">  
                <Customer CustomerID="C1" OrderList="OrderA OrderB"  >  
                              <spouse>Jenny</spouse>  
                                <Order OrderID="OrderA"><OrderValue>11</OrderValue></Order>  
                                <Order OrderID="OrderB"><OrderValue>22</OrderValue></Order>  
  
                </Customer>  
                <Customer CustomerID="C2" OrderList="OrderC OrderD" >  
                                <spouse>John</spouse>  
                                <Order OrderID="OrderC"><OrderValue>33</OrderValue></Order>  
                                <Order OrderID="OrderD"><OrderValue>44</OrderValue></Order>  
  
                        </Customer>  
                <Customer CustomerID="C3"  OrderList="OrderE OrderF" >  
                                <spouse>Jane</spouse>  
                                <Order OrderID="OrderE"><OrderValue>55</OrderValue></Order>  
                                <Order OrderID="OrderF"><OrderValue>55</OrderValue></Order>  
                </Customer>  
                <Customer CustomerID="C4"  OrderList="OrderG"  >  
                                <spouse>Tim</spouse>  
                                <Order OrderID="OrderG"><OrderValue>66</OrderValue></Order>  
                        </Customer>  
                <Customer CustomerID="C5"  >  
                </Customer>  
                <Customer CustomerID="C6" >  
                </Customer>  
                <Customer CustomerID="C7"  >  
                </Customer>  
</CustOrders:Customers>'  
select @x.query('declare namespace CustOrders="Customers";  
  id(data(CustOrders:Customers/Customer[1]/@OrderList)[1])')  
  
-- result  
<Order OrderID="OrderA">  
  <OrderValue>11</OrderValue>  
</Order>  
```  
  
### <a name="implementation-limitations"></a>Limitações de implementação  
 Estas são as limitações:  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]não suporta a versão de dois argumentos do **id()**.  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]requer que o tipo de **argumento de id()** seja um subtipo de xs:IDREF*.  
  
## <a name="see-also"></a>Consulte Também  
 [Funções em sequências](https://msdn.microsoft.com/library/672d2795-53ab-49c2-bf24-bc81a47ecd3f)  
  
  
