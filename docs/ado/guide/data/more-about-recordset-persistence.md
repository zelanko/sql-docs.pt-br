---
description: Mais informações sobre a persistência do conjunto de registros
title: Mais sobre a persistência do conjunto de registros | Microsoft Docs
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
- updating data [ADO], persisting data
ms.assetid: a9b287f5-04b0-4514-8143-f67879ca9842
author: rothja
ms.author: jroth
ms.openlocfilehash: 1dca646b07c441a4fccd617723aba98536f1a7e1
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88980327"
---
# <a name="more-about-recordset-persistence"></a>Mais informações sobre a persistência do conjunto de registros
O objeto Recordset ADO dá suporte ao armazenamento do conteúdo de um objeto **Recordset** em um arquivo usando seu método [Save](../../reference/ado-api/save-method.md) . O arquivo armazenado persistente pode existir em uma unidade local, servidor ou como uma URL em um site da Web. Posteriormente, o arquivo pode ser restaurado com o método [Open](../../reference/ado-api/open-method-ado-recordset.md) do objeto **Recordset** ou o método [Execute](../../reference/ado-api/execute-method-ado-connection.md) do objeto [Connection](../../reference/ado-api/connection-object-ado.md) .  
  
 Além disso, o método [GetString](../../reference/ado-api/getstring-method-ado.md) converte um objeto **Recordset** em um formulário no qual as colunas e linhas são delimitadas por caracteres especificados.  
  
 Para persistir um **conjunto de registros**, comece convertendo-o em um formulário que possa ser armazenado em um arquivo. Os objetos **Recordset** podem ser armazenados no formato TableGram de dados avançados (ADTG) proprietário ou no formato Open linguagem XML (XML). Os exemplos de ADTG são mostrados na próxima seção. Para obter mais informações sobre persistência XML, consulte [Persisteting Records in XML Format](./persisting-records-in-xml-format.md).  
  
 Salve as alterações pendentes no arquivo persistente. Isso permite que você emita uma consulta que retorne um objeto **Recordset** , edite o **conjunto de registros**, salve-o e as alterações pendentes, posteriormente, restaura o **conjunto de registros**e, em seguida, atualiza a fonte de dados com as alterações pendentes salvas.  
  
 Para obter informações sobre como armazenar objetos de **fluxo** de forma persistente, consulte [fluxos e persistência](./streams-and-persistence.md).  
  
 Para obter um exemplo de persistência do **conjunto de registros** , consulte o cenário de persistência do conjunto de registros XML.  
  
## <a name="example"></a>Exemplo  
  
### <a name="save-a-recordset"></a>Salvar um conjunto de registros:  
  
```  
Dim rs as New ADODB.Recordset  
rs.Save "c:\yourFile.adtg", adPersistADTG  
```  
  
### <a name="open-a-persisted-file-with-recordsetopen"></a>Abra um arquivo persistente com Recordset. Open:  
  
```  
Dim rs as New ADODB.Recordset  
rs.Open "c:\yourFile.adtg", "Provider=MSPersist",,,adCmdFile  
```  
  
 Opcionalmente, se o **conjunto de registros** não tiver uma conexão ativa, você poderá aceitar todos os padrões e codificar o seguinte:  
  
```  
Dim rs as New ADODB.Recordset  
rs.Open "c:\yourFile.adtg"  
```  
  
### <a name="open-a-persisted-file-with-connectionexecute"></a>Abra um arquivo persistente com Connection.Exegraciosos:  
  
```  
Dim conn as New ADODB.Connection  
Dim rs as ADODB.Recordset  
conn.Open "Provider=MSPersist"  
Set rs = conn.execute("c:\yourFile.adtg")  
```  
  
### <a name="open-a-persisted-file-with-rdsdatacontrol"></a>Abra um arquivo persistente com RDS. DataControl  
 Nesse caso, a propriedade do **servidor** não está definida.  
  
```  
Dim dc as New RDS.DataControl  
dc.Connection = "Provider=MSPersist"  
dc.SQL = "c:\yourFile.adtg"  
dc.Refresh  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Método GetString (ADO)](../../reference/ado-api/getstring-method-ado.md)   
 [Provedor de persistência do Microsoft OLE DB (provedor de serviços ADO)](../appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md)   
 [Objeto Recordset (ADO)](../../reference/ado-api/recordset-object-ado.md)   
 [Fluxos e persistência](./streams-and-persistence.md)