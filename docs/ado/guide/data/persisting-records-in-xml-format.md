---
description: Persistência de registros em formato XML
title: Persistência de registros em formato XML | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- persisting data [ADO]
- data updates [ADO], persisting data
- data persistence [ADO]
- XML persistence [ADO]
- updating data [ADO], persisting data
ms.assetid: f3113ec4-ae31-428f-89c6-bc1024f128ea
author: rothja
ms.author: jroth
ms.openlocfilehash: 31512fd9843ae5ff15fc2f7c6981fccdc926dbb5
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88980057"
---
# <a name="persisting-records-in-xml-format"></a>Persistência de registros em formato XML
Como o formato ADTG, a persistência do **conjunto de registros** em formato XML é implementada com o provedor de persistência do Microsoft OLE DB. Esse provedor gera um conjunto de linhas somente de encaminhamento, somente leitura, de um arquivo XML salvo ou fluxo que contém as informações de esquema geradas pelo ADO. Da mesma forma, ele pode pegar um **conjunto de registros**ADO, gerar XML e salvá-lo em um arquivo ou em qualquer objeto que implemente a interface com **IStream** . (Na verdade, um arquivo é apenas outro exemplo de um objeto que dá suporte a **IStream**.) Para as versões 2,5 e posteriores, o ADO depende do Microsoft XML Parser (MSXML) para carregar o XML no **conjunto de registros**; Portanto, msxml.dll é necessário.  
  
> [!NOTE]
>  Algumas limitações se aplicam ao salvar **conjuntos de registros** hierárquicos (formas de dados) em formato XML. Você não poderá salvar em XML se o **conjunto de registros** hierárquico contiver atualizações pendentes e não for possível salvar um **conjunto de registros**hierárquicos parametrizados. Para obter mais informações, consulte [mantendo conjuntos de registros filtrados e hierárquicos](../../../ado/guide/data/persisting-filtered-and-hierarchical-recordsets.md).  
  
 A maneira mais fácil de manter os dados em XML e carregá-los novamente por meio do ADO é com os métodos **Save** e **Open** , respectivamente. O exemplo de código ADO a seguir demonstra como salvar os dados na tabela **títulos** em um arquivo nomeado titles. SAV.  
  
```  
Dim rs as new Recordset  
Dim rs2 as new Recordset  
Dim c as new Connection  
Dim s as new Stream  
  
' Query the Titles table.  
c.Open "provider=sqloledb;data source=MySQLServer;initial catalog=pubs;Integrated Security='SSPI'"  
rs.cursorlocation = adUseClient  
rs.Open "select * from titles", c, adOpenStatic  
  
' Save to the file in the XML format. Note that if you don't specify   
' adPersistXML, a binary format (ADTG) will be used by default.  
rs.Save "titles.sav", adPersistXML  
  
' Save the recordset into the ADO Stream object.  
rs.save s, adPersistXML  
rs.Close  
c.Close  
  
set rs = nothing  
  
' Reopen the file.  
rs.Open "titles.sav",,,,adCmdFile  
' Open the Stream back into a Recordset.  
rs2.open s  
```  
  
 O ADO sempre persiste todo o objeto **Recordset** . Se você quiser manter um subconjunto de linhas do objeto **Recordset** , use o método **Filter** para restringir as linhas ou alterar sua cláusula de seleção. No entanto, você deve abrir um objeto **Recordset** com um cursor do lado do cliente (**CursorLocation**  =  **adUseClient**) para usar o método de **filtro** para salvar um subconjunto de linhas. Por exemplo, para recuperar títulos que começam com a letra "b", você pode aplicar um filtro a um objeto Open **Recordset** :  
  
```  
rs.Filter "title_id like 'B*'"  
rs.Save "btitles.sav", adPersistXML  
```  
  
 O ADO sempre usa o conjunto de linhas do mecanismo de cursor do cliente para produzir um objeto de **conjunto de registros** que poderá ser marcado como rolável sobre os dados somente de encaminhamento gerados pelo provedor de persistência.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Formato de persistência XML](../../../ado/guide/data/xml-persistence-format.md)  
  
-   [Namespaces](../../../ado/guide/data/namespaces.md)  
  
-   [Seção de esquema](../../../ado/guide/data/schema-section.md)  
  
-   [Seção de dados](../../../ado/guide/data/data-section.md)  
  
-   [Conjuntos de registros hierárquicos em XML](../../../ado/guide/data/hierarchical-recordsets-in-xml.md)  
  
-   [Propriedades dinâmicas do conjunto de registros em XML](../../../ado/guide/data/recordset-dynamic-properties-in-xml.md)  
  
-   [Transformações XSLT](../../../ado/guide/data/xslt-transformations.md)  
  
-   [Salvar no objeto DOM XML](../../../ado/guide/data/saving-to-the-xml-dom-object.md)  
  
-   [Considerações sobre segurança XML](../../../ado/guide/data/xml-security-considerations.md)  
  
-   [Cenário de persistência do conjunto de registros XML](../../../ado/guide/data/xml-recordset-persistence-scenario.md)
