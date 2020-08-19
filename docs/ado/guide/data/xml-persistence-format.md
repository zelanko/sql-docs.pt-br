---
description: Formato de persistência XML
title: Formato de persistência XML | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- XML persistence [ADO], persistence format
ms.assetid: 6e146738-ac4d-47bb-b6cd-d87b2260aead
author: rothja
ms.author: jroth
ms.openlocfilehash: 7a014addf2d3ff6c7b02ed9abc103cdbd7b2ecb8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88452508"
---
# <a name="xml-persistence-format"></a>Formato de persistência XML
O ADO usa a codificação UTF-8 para o fluxo XML que ele mantém.  
  
 O formato ADO XML é dividido em duas seções, uma seção de esquema seguida da seção de dados. Este é um arquivo XML de exemplo para a tabela transportadoras do banco de dados Northwind. Várias partes do XML são discutidas seguindo o exemplo.  
  
## <a name="remarks"></a>Comentários  
  
```  
<xml xmlns:s="uuid:BDC6E3F0-6DA3-11d1-A2A3-00AA00C14882"   
xmlns:dt="uuid:C2F41010-65B3-11d1-A29F-00AA00C14882"   
xmlns:rs="urn:schemas-microsoft-com:rowset"   
xmlns:z="#RowsetSchema">   
  <s:Schema id="RowsetSchema">   
    <s:ElementType name="row" content="eltOnly" rs:updatable="true">   
      <s:AttributeType name="ShipperID" rs:number="1"   
        rs:basetable="shippers" rs:basecolumn="ShipperID"  
        rs:keycolumn="true">   
        <s:datatype dt:type="int" dt:maxLength="4" rs:precision="10"   
          rs:fixedlength="true" rs:maybenull="false"/>   
      </s:AttributeType>   
      <s:AttributeType name="CompanyName" rs:number="2"   
        rs:nullable="true" rs:write="true" rs:basetable="shippers"   
        rs:basecolumn="CompanyName">   
        <s:datatype dt:type="string" dt:maxLength="40" />   
      </s:AttributeType>   
      <s:AttributeType name="Phone" rs:number="3" rs:nullable="true"   
        rs:write="true" rs:basetable="shippers"   
        rs:basecolumn="Phone">   
        <s:datatype dt:type="string" dt:maxLength="24"/>   
      </s:AttributeType>   
      <s:extends type="rs:rowbase"/>   
    </s:ElementType>   
  </s:Schema>   
  
  <rs:data>   
    <z:row ShipperID="1" CompanyName="Speedy Express"   
      Phone="(503) 555-9831"/>   
    <z:row ShipperID="2" CompanyName="United Package"   
      Phone="(503) 555-3199"/>   
    <z:row ShipperID="3" CompanyName="Federal Shipping"   
      Phone="(503) 555-9931"/>   
  </rs:data>   
</xml>  
```  
  
 O esquema mostra as declarações de namespaces, a seção de esquema e a seção de dados. A seção de esquema contém definições para Row, transportadora, CompanyName e Phone.  
  
 As definições de esquema estão em conformidade com a [especificação de dados XML do W3C](http://www.w3.org/TR/1998/NOTE-XML-data/) e podem ser totalmente validadas (embora a validação não ocorra no Internet Explorer 5). XML-os dados atualmente são o único formato de esquema com suporte para persistência de conjunto de registros.  
  
 A seção de dados tem três linhas que contêm informações sobre transportadoras. Para um conjunto de linhas vazio, a seção de dados pode estar vazia, mas as \<rs:data> marcas devem estar presentes. Sem dados, você pode escrever a tag de forma abreviada como simplesmente \<rs:data/> . Qualquer marca prefixada com "RS" indica que está no namespace definido por urn: schemas-microsoft-com: Rowset.  
  
## <a name="see-also"></a>Consulte Também  
 [Persistência de registros em formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md)
