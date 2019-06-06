---
title: Persistência de registros em formato XML | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 783dfb43f1eaebcc823f49000f589542465b1735
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66701939"
---
# <a name="persisting-records-in-xml-format"></a>Persistência de registros em formato XML
Como o formato ADTG **Recordset** persistência em formato XML é implementada com o Microsoft OLE DB provedor de persistência. Esse provedor gera um conjunto de linhas de somente avanço, somente leitura de um fluxo que contém as informações de esquema geradas por ADO ou arquivo XML salvo. Da mesma forma, pode levar a um ADO **conjunto de registros**, gerar o XML e salvá-lo em um arquivo ou qualquer objeto que implementa o COM **IStream** interface. (Na verdade, um arquivo é somente outro exemplo de um objeto que dá suporte a **IStream**.) Para as versões 2.5 e posteriores, o ADO baseia-se no Microsoft XML Parser (MSXML) para carregar o XML para o **conjunto de registros**; portanto, o MSXML. dll é necessária.  
  
> [!NOTE]
>  Algumas limitações se aplicam ao salvar hierárquica **conjuntos de registros** (formas de dados) em formato XML. Não é possível salvar em XML se o hierárquica **conjunto de registros** contém as atualizações pendentes, e não é possível salvar um parametrizada hierárquica **conjunto de registros**. Para obter mais informações, consulte [persistindo filtrados e conjuntos de registros hierárquicos](../../../ado/guide/data/persisting-filtered-and-hierarchical-recordsets.md).  
  
 A maneira mais fácil de manter os dados em XML e carregá-lo de volta novamente por meio de ADO é com o **salve** e **abrir** métodos, respectivamente. O exemplo de código ADO demonstra salvando os dados a **títulos** tabela em um arquivo chamado titles.sav.  
  
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
  
 ADO sempre persiste todo o **Recordset** objeto. Se você desejar manter um subconjunto de linhas do **conjunto de registros** do objeto, use o **filtro** método para restringir as linhas ou alterar sua cláusula de seleção. No entanto, você deve abrir um **conjunto de registros** objeto com um cursor do lado do cliente (**CursorLocation** = **adUseClient**) para usar o **filtrar** método para salvar um subconjunto de linhas. Por exemplo, para recuperar os títulos que começam com a letra "b", você pode aplicar um filtro para um aberto **Recordset** objeto:  
  
```  
rs.Filter "title_id like 'B*'"  
rs.Save "btitles.sav", adPersistXML  
```  
  
 ADO sempre usa o conjunto de linhas do mecanismo de Cursor do cliente para produzir um rolável possíveis de indicação **Recordset** objeto sobre os dados de somente avanço gerados pelo provedor de persistência.  
  
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
