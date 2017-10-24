---
title: Manter registros em formato XML | Microsoft Docs
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
- persisting data [ADO]
- data updates [ADO], persisting data
- data persistence [ADO]
- XML persistence [ADO]
- updating data [ADO], persisting data
ms.assetid: f3113ec4-ae31-428f-89c6-bc1024f128ea
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a45c434bdcf551e97eb97f85997ab73c883b599c
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="persisting-records-in-xml-format"></a>Manter registros em formato XML
Como o formato ADTG, **registros** persistência em formato XML é implementada com o Microsoft OLE DB provedor de persistência. Este provedor gera um conjunto de linhas de somente avanço, somente leitura de um arquivo XML salvo ou um fluxo que contém as informações de esquema geradas pelo ADO. Da mesma forma, pode levar um ADO **registros**, gerar o XML e salvá-lo em um arquivo ou qualquer objeto que implementa o COM **IStream** interface. (Na verdade, um arquivo é apenas um exemplo de um objeto que oferece suporte a **IStream**.) Para versões 2.5 e superior, ADO baseia-se no Microsoft XML Parser (MSXML) ao carregar o XML para o **registros**; portanto MSXML é necessária.  
  
> [!NOTE]
>  Algumas limitações se aplicam ao salvar hierárquica **conjuntos de registros** (formas de dados) em formato XML. Não é possível salvar em XML se o hierárquica **Recordset** contém as atualizações pendentes, e não é possível salvar um parametrizadas hierárquica **registros**. Para obter mais informações, consulte [persistentes filtrados e conjuntos de registros hierárquicos](../../../ado/guide/data/persisting-filtered-and-hierarchical-recordsets.md).  
  
 A maneira mais fácil de manter os dados em XML e carregá-lo de volta novamente por meio de ADO é com o **salvar** e **abrir** métodos, respectivamente. O exemplo de código ADO demonstra salvando os dados a **títulos** tabela para um arquivo chamado titles.sav.  
  
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
  
 ADO sempre persiste todo o **registros** objeto. Se você deseja manter um subconjunto de linhas do **registros** de objeto, use o **filtro** método para restringir as linhas ou altere a cláusula de seleção. No entanto, você deve abrir um **registros** objeto com um cursor do lado do cliente (**CursorLocation** = **adUseClient**) para usar o **defiltro** método para salvar um subconjunto de linhas. Por exemplo, para recuperar os títulos que começam com a letra "b", você pode aplicar um filtro para um abrir **registros** objeto:  
  
```  
rs.Filter "title_id like 'B*'"  
rs.Save "btitles.sav", adPersistXML  
```  
  
 ADO sempre usa o conjunto de linhas do mecanismo de Cursor do cliente para produzir um rolável bookmarkable **registros** objeto sobre os dados de somente avanço gerados pelo provedor de persistência.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Formato de persistência XML](../../../ado/guide/data/xml-persistence-format.md)  
  
-   [Namespaces](../../../ado/guide/data/namespaces.md)  
  
-   [Seção de esquema](../../../ado/guide/data/schema-section.md)  
  
-   [Seção de dados](../../../ado/guide/data/data-section.md)  
  
-   [Conjuntos de registros hierárquicos em XML](../../../ado/guide/data/hierarchical-recordsets-in-xml.md)  
  
-   [Propriedades dinâmicas do conjunto de registros em XML](../../../ado/guide/data/recordset-dynamic-properties-in-xml.md)  
  
-   [Transformações XSLT](../../../ado/guide/data/xslt-transformations.md)  
  
-   [Salvando no objeto DOM XML](../../../ado/guide/data/saving-to-the-xml-dom-object.md)  
  
-   [Considerações sobre segurança XML](../../../ado/guide/data/xml-security-considerations.md)  
  
-   [Cenário de persistência do conjunto de registros XML](../../../ado/guide/data/xml-recordset-persistence-scenario.md)

