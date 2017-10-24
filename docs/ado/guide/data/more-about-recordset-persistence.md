---
title: "Mais informações sobre o conjunto de registros persistência | Microsoft Docs"
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
- updating data [ADO], persisting data
ms.assetid: a9b287f5-04b0-4514-8143-f67879ca9842
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8baac18c8d27face9438a85a2c35db57348836a3
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="more-about-recordset-persistence"></a>Mais informações sobre a persistência de conjunto de registros
O objeto de conjunto de registros ADO dá suporte ao armazenar o conteúdo de um **registros** objeto em um arquivo usando seu [salvar](../../../ado/reference/ado-api/save-method.md) método. O arquivo armazenado persistentemente pode existir em um local da unidade, server, ou como uma URL em uma Web sites. Posteriormente, o arquivo pode ser restaurado com o o [abrir](../../../ado/reference/ado-api/open-method-ado-recordset.md) método do **registros** objeto ou o [Execute](../../../ado/reference/ado-api/execute-method-ado-connection.md) método do [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) objeto.  
  
 Além disso, o [GetString](../../../ado/reference/ado-api/getstring-method-ado.md) método converte um **registros** objeto a um formulário no qual as colunas e linhas são delimitadas por caracteres que você especificar.  
  
 Para manter um **registros**, comece convertê-la em um formulário que pode ser armazenado em um arquivo. **Conjunto de registros** objetos podem ser armazenados no formato de TableGram de dados avançado (ADTG) proprietário ou o abra Extensible Markup Language (XML). Exemplos ADTG são mostrados na próxima seção. Para obter mais informações sobre a persistência de XML, consulte [manter registros em formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md).  
  
 Salve as alterações pendentes no arquivo persistente. Isso permite que você emita uma consulta que retorna um **registros** objeto, edições a **registros**, salva-o e as alterações pendentes, restaura mais tarde o **Recordset**e, em seguida, Atualiza a fonte de dados com o salva as alterações pendentes.  
  
 Para obter informações sobre o armazenamento persistente **fluxo** objetos, consulte [fluxos e persistência](../../../ado/guide/data/streams-and-persistence.md).  
  
 Para obter um exemplo de **registros** persistência, consulte o cenário de persistência do conjunto de registros de XML.  
  
## <a name="example"></a>Exemplo  
  
### <a name="save-a-recordset"></a>Salve um conjunto de registros:  
  
```  
Dim rs as New ADODB.Recordset  
rs.Save "c:\yourFile.adtg", adPersistADTG  
```  
  
### <a name="open-a-persisted-file-with-recordsetopen"></a>Abra um arquivo persistente com Recordset.Open:  
  
```  
Dim rs as New ADODB.Recordset  
rs.Open "c:\yourFile.adtg", "Provider=MSPersist",,,adCmdFile  
```  
  
 Opcionalmente, se o **registros** does não tem uma conexão ativa, você pode aceitar todos os padrões e de código a seguir:  
  
```  
Dim rs as New ADODB.Recordset  
rs.Open "c:\yourFile.adtg"  
```  
  
### <a name="open-a-persisted-file-with-connectionexecute"></a>Abra um arquivo persistente com Connection.Execute:  
  
```  
Dim conn as New ADODB.Connection  
Dim rs as ADODB.Recordset  
conn.Open "Provider=MSPersist"  
Set rs = conn.execute("c:\yourFile.adtg")  
```  
  
### <a name="open-a-persisted-file-with-rdsdatacontrol"></a>Abrir um arquivo persistente com RDS. DataControl:  
 Nesse caso, o **Server** propriedade não está definida.  
  
```  
Dim dc as New RDS.DataControl  
dc.Connection = "Provider=MSPersist"  
dc.SQL = "c:\yourFile.adtg"  
dc.Refresh  
```  
  
## <a name="see-also"></a>Consulte também  
 [Método GetString (ADO)](../../../ado/reference/ado-api/getstring-method-ado.md)   
 [Provedor de persistência do Microsoft OLE DB (provedor de serviços de ADO)](../../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md)   
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Fluxos e persistência](../../../ado/guide/data/streams-and-persistence.md)

