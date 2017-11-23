---
title: "Conjuntos de registros hierárquicos em XML | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: hierarchical Recordsets [ADO], in XML
ms.assetid: 5d4b11c4-c94f-4910-b99b-5b9abc50d791
caps.latest.revision: "4"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: eb5fb67b0572ea7edea1259ac1314706cc883cd8
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="hierarchical-recordsets-in-xml"></a>Conjuntos de registros hierárquicos em XML
ADO permite a persistência de objetos hierárquicas do conjunto de registros em XML. Com objetos hierárquicos do conjunto de registros, o valor de um campo no conjunto de registros pai é outro conjunto de registros. Esses campos são representados como elementos filho no fluxo XML em vez de um atributo.  
  
## <a name="remarks"></a>Comentários  
 O exemplo a seguir demonstra esse caso:  
  
```  
Rs.Open "SHAPE {select stor_id, stor_name, state from stores} APPEND ({select stor_id, ord_num, ord_date, qty from sales} AS rsSales RELATE stor_id TO stor_id)", "Provider=MSDataShape;DSN=pubs;Integrated Security=SSPI;"  
```  
  
 Este é o formato XML do conjunto de registros persistente:  
  
```  
<xml xmlns:s="uuid:BDC6E3F0-6DA3-11d1-A2A3-00AA00C14882"     xmlns:dt="uuid:C2F41010-65B3-11d1-A29F-00AA00C14882"     xmlns:rs="urn:schemas-microsoft-com:rowset"   
    xmlns:z="#RowsetSchema">   
  <s:Schema id="RowsetSchema">   
    <s:ElementType name="row" content="eltOnly" rs:updatable="true">   
      <s:AttributeType name="stor_id" rs:number="1"   
        rs:writeunknown="true">   
        <s:datatype dt:type="string" dt:maxLength="4"   
          rs:fixedlength="true" rs:maybenull="false"/>   
      </s:AttributeType>   
      <s:AttributeType name="stor_name" rs:number="2" rs:nullable="true"   
        rs:writeunknown="true">   
          <s:datatype dt:type="string" dt:maxLength="40"/>   
      </s:AttributeType>   
      <s:AttributeType name="state" rs:number="3" rs:nullable="true"   
        rs:writeunknown="true">   
        <s:datatype dt:type="string" dt:maxLength="2"   
          rs:fixedlength="true"/>   
      </s:AttributeType>   
      <s:ElementType name="rsSales" content="eltOnly"   
        rs:updatable="true" rs:relation="010000000100000000000000">   
        <s:AttributeType name="stor_id" rs:number="1"   
          rs:writeunknown="true">   
          <s:datatype dt:type="string" dt:maxLength="4"   
            rs:fixedlength="true" rs:maybenull="false"/>   
        </s:AttributeType>   
        <s:AttributeType name="ord_num" rs:number="2"   
          rs:writeunknown="true">   
          <s:datatype dt:type="string" dt:maxLength="20"   
            rs:maybenull="false"/>   
        </s:AttributeType>   
        <s:AttributeType name="ord_date" rs:number="3"   
          rs:writeunknown="true">   
            <s:datatype dt:type="dateTime" dt:maxLength="16"   
              rs:scale="3" rs:precision="23" rs:fixedlength="true"   
              rs:maybenull="false"/>   
        </s:AttributeType>   
        <s:AttributeType name="qty" rs:number="4" rs:writeunknown="true">   
          <s:datatype dt:type="i2" dt:maxLength="2" rs:precision="5"   
            rs:fixedlength="true" rs:maybenull="false"/>   
        </s:AttributeType>   
        <s:extends type="rs:rowbase"/>   
      </s:ElementType>   
      <s:extends type="rs:rowbase"/>   
    </s:ElementType>   
  </s:Schema>   
  <rs:data>   
    <z:row stor_id="6380" stor_name="Eric the Read Books" state="WA">   
      <rsSales stor_id="6380" ord_num="6871"   
        ord_date="1994-09-14T00:00:00" qty="5"/>   
      <rsSales stor_id="6380" ord_num="722a"   
        ord_date="1994-09-13T00:00:00" qty="3"/>   
    </z:row>   
    <z:row stor_id="7066" stor_name="Barnum's" state="CA">   
      <rsSales stor_id="7066" ord_num="A2976"   
        ord_date="1993-05-24T00:00:00" qty="50"/>   
      <rsSales stor_id="7066" ord_num="QA7442.3"   
        ord_date="1994-09-13T00:00:00" qty="75"/>   
    </z:row>   
    <z:row stor_id="7067" stor_name="News & Brews" state="CA">   
      <rsSales stor_id="7067" ord_num="D4482"   
        ord_date="1994-09-14T00:00:00" qty="10"/>   
      <rsSales stor_id="7067" ord_num="P2121"   
        ord_date="1992-06-15T00:00:00" qty="40"/>   
      <rsSales stor_id="7067" ord_num="P2121"   
        ord_date="1992-06-15T00:00:00" qty="20"/>   
      <rsSales stor_id="7067" ord_num="P2121"   
        ord_date="1992-06-15T00:00:00" qty="20"/>   
    </z:row>   
  </rs:data>   
</xml>   
```  
  
 A ordem exata das colunas no conjunto de registros pai não é óbvia quando ele é mantido dessa maneira. Qualquer campo no pai pode conter um conjunto de registros filho. O provedor de persistência persistir todas as colunas escalares primeiro como atributos e, em seguida, persistir as colunas"todos os filhos Recordset" como elementos filho da linha pai. A posição ordinal do campo no pai conjunto de registros pode ser obtido consultando a definição de esquema do conjunto de registros. Cada campo tem uma propriedade do OLE DB, rs: número definida no namespace do esquema de conjunto de registros que contém o número ordinal para esse campo.  
  
 Os nomes de todos os campos no conjunto de registros filho são concatenados com o nome do campo no conjunto de registros que contém esse filho do pai. Isso é para garantir que não haja nenhum colisões de nomes em casos onde pai e filho conjuntos de registros ambos contêm um campo que é obtido de duas tabelas diferentes, mas é denominado individualmente.  
  
 Ao salvar o conjunto de registros hierárquicos em XML, você deve estar ciente das seguintes restrições no ADO:  
  
-   Um conjunto de registros hierárquico com atualizações pendentes não pode ser mantido em XML.  
  
-   Um conjunto de registros hierárquico criado com um comando de forma com parâmetros não pode ser persistentes (em formato XML ou ADTG).  
  
-   Atualmente, o ADO salva a relação entre pai e o conjunto de registros filho como um objeto binário grande (BLOB). Marcas XML para descrever esse relação ainda não tem sido definidas no namespace do esquema de conjunto de linhas.  
  
-   Quando um conjunto de registros hierárquico é salvo, filho todos os conjuntos de registros são salvas com ela. Se o conjunto de registros atual é um filho de outro conjunto de registros, seu pai não serão salvas. Filho de todos os conjuntos de registros que formam a subárvore do conjunto de registros atual são salvas.  
  
 Quando um conjunto de registros hierárquico é reaberto do formato XML persistentes, você deve estar ciente das seguintes limitações:  
  
-   Se o registro filho contém registros para o qual não há nenhum registro correspondente do pai, essas linhas não são gravadas na representação XML do conjunto de registros hierárquicos. Portanto, essas linhas serão perdidas quando o conjunto de registros é reaberto do local de armazenamento persistente.  
  
-   Se um registro filho tiver referências a mais de um registro pai, em seguida, em reabrir o conjunto de registros, o conjunto de registros filho pode conter registros duplicados. No entanto, essas duplicatas só estará visíveis se o usuário trabalha diretamente com o conjunto de linhas filho subjacente. Se um capítulo é usado para navegar o filho do conjunto de registros (que é a única maneira de navegar por meio de ADO), as duplicatas não são visíveis.  
  
## <a name="see-also"></a>Consulte também  
 [Persistência de registros em formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md)
