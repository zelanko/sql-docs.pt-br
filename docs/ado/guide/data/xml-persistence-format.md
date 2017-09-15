---
title: "Formato de persistência XML | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- XML persistence [ADO], persistence format
ms.assetid: 6e146738-ac4d-47bb-b6cd-d87b2260aead
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8694aac4f8699d102d94664862f5ad357579eab9
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="xml-persistence-format"></a>Formato de persistência XML
ADO usa codificação UTF-8 para o fluxo XML que ele persistir.  
  
 O formato XML ADO é dividido em duas seções, uma seção de esquema seguida a seção de dados. Este é um arquivo XML de exemplo para a tabela Transportadoras do banco de dados Northwind. Várias partes do XML são discutidas o exemplo a seguir.  
  
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
  
 O esquema mostra as declarações de namespaces, a seção do esquema e a seção de dados. A seção de esquema contém definições de linha, CódigoDaTransportadora, CompanyName e telefone.  
  
 Definições de esquema estão em conformidade com a [especificação W3C XML-Data](http://www.w3.org/TR/1998/NOTE-XML-data/) e podem ser validadas totalmente (embora a validação não ocorrerá no Internet Explorer 5). Dados XML no momento são o formato de esquema com suporte apenas para a persistência de conjunto de registros.  
  
 A seção de dados tem três linhas que contém informações sobre transportadores. Para um conjunto de linhas vazio, a seção de dados pode estar vazia, mas o \<: dados do rs > marcas devem estar presentes. Sem dados, você poderia escrever a abreviação de marca simplesmente \<: dados do rs / >. Qualquer marca prefixada com "rs" indica que é o namespace definido pelo urn: schemas-microsoft-com:rowset.  
  
## <a name="see-also"></a>Consulte também  
 [Persistência de registros em formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md)
