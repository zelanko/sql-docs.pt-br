---
title: Mais sobre a persistência do conjunto de registros | Microsoft Docs
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
- updating data [ADO], persisting data
ms.assetid: a9b287f5-04b0-4514-8143-f67879ca9842
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3e626c924e7b84312877b47f811329e215f47e42
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47846854"
---
# <a name="more-about-recordset-persistence"></a>Mais informações sobre a persistência do conjunto de registros
O objeto de conjunto de registros ADO dá suporte ao armazenar o conteúdo de um **conjunto de registros** objeto em um arquivo usando seu [salvar](../../../ado/reference/ado-api/save-method.md) método. O arquivo persistentemente armazenado pode existir em um local da unidade, servidor, ou como uma URL em uma Web sites. Posteriormente, o arquivo pode ser restaurado com um a [aberto](../../../ado/reference/ado-api/open-method-ado-recordset.md) método da **conjunto de registros** objeto ou o [Execute](../../../ado/reference/ado-api/execute-method-ado-connection.md) o método da [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) objeto.  
  
 Além disso, o [GetString](../../../ado/reference/ado-api/getstring-method-ado.md) método converte um **Recordset** objeto a um formulário no qual as colunas e linhas são delimitadas por caracteres que você especificar.  
  
 Para manter uma **Recordset**, comece convertê-la em um formulário que pode ser armazenado em um arquivo. **Conjunto de registros** objetos podem ser armazenados no formato TableGram avançada de dados (ADTG) proprietárias ou formato aberto Extensible Markup Language (XML). Exemplos ADTG são mostrados na próxima seção. Para obter mais informações sobre a persistência do XML, consulte [manter registros em formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md).  
  
 Salve as alterações pendentes no arquivo persistente. Isso permite que você emita uma consulta que retorna um **conjunto de registros** objeto, as edições a **conjunto de registros**, salva a ele e as alterações pendentes, posterior restaura o **conjunto de registros**e, em seguida, Atualiza a fonte de dados com o salva as alterações pendentes.  
  
 Para obter informações sobre como armazenar persistentemente **Stream** objetos, consulte [fluxos e persistência](../../../ado/guide/data/streams-and-persistence.md).  
  
 Para obter um exemplo de **Recordset** persistência, consulte o cenário de persistência do conjunto de registros XML.  
  
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
  
 Opcionalmente, se o **Recordset** faz não tem uma conexão ativa, você pode aceitar todos os padrões e de código a seguir:  
  
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
  
### <a name="open-a-persisted-file-with-rdsdatacontrol"></a>Abrir um arquivo persistente com o RDS. DataControl:  
 Nesse caso, o **Server** não está definida.  
  
```  
Dim dc as New RDS.DataControl  
dc.Connection = "Provider=MSPersist"  
dc.SQL = "c:\yourFile.adtg"  
dc.Refresh  
```  
  
## <a name="see-also"></a>Consulte também  
 [Método GetString (ADO)](../../../ado/reference/ado-api/getstring-method-ado.md)   
 [Persistência do Microsoft OLE DB Provider (provedor de serviços do ADO)](../../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md)   
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Fluxos e persistência](../../../ado/guide/data/streams-and-persistence.md)
