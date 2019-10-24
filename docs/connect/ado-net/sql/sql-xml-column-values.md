---
title: Valores de coluna XML do SQL
description: Demonstra como recuperar e trabalhar com dados XML recuperados do SQL Server.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: d97ce4da-f09c-4d1e-85b7-a0ccedd7246a
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: d8dc9d5100f71fed39c1e4166882230451dd139e
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72451935"
---
# <a name="sql-xml-column-values"></a>Valores de coluna XML do SQL

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Download ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

SQL Server dá suporte ao tipo de dados `xml`, e os desenvolvedores podem recuperar conjuntos de resultados, incluindo esse tipo usando o comportamento padrão da classe <xref:Microsoft.Data.SqlClient.SqlCommand>. Uma coluna `xml` pode ser recuperada da mesma forma que qualquer coluna é recuperada (em uma <xref:Microsoft.Data.SqlClient.SqlDataReader>, por exemplo), mas se você quiser trabalhar com o conteúdo da coluna como XML, deverá usar uma <xref:System.Xml.XmlReader>.  
  
## <a name="example"></a>Exemplo  
O aplicativo de console a seguir seleciona duas linhas, cada uma contendo uma `xml` coluna, da tabela **Sales. Store** no banco de dados **AdventureWorks** para uma instância <xref:Microsoft.Data.SqlClient.SqlDataReader>. Para cada linha, o valor da coluna `xml` é lido usando o método <xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlXml%2A> de <xref:Microsoft.Data.SqlClient.SqlDataReader>. O valor é armazenado em um <xref:System.Xml.XmlReader>. Observe que você deve usar <xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlXml%2A> em vez do método <xref:System.Data.IDataRecord.GetValue%2A> se quiser definir o conteúdo para uma variável <xref:System.Data.SqlTypes.SqlXml>;  <xref:System.Data.IDataRecord.GetValue%2A> retorna o valor da coluna `xml` como uma cadeia de caracteres.  
  
> [!NOTE]
>  O banco de dados de exemplo **AdventureWorks** não é instalado por padrão quando você instala o SQL Server. Você pode instalá-lo executando SQL Server configuração.  
  
[!code-csharp[DataWorks SqlDataReader_GetSqlXml#1](~/../sqlclient/doc/samples/SqlDataReader_GetSqlXml.cs#1)]
  
## <a name="next-steps"></a>Próximas etapas
- <xref:System.Data.SqlTypes.SqlXml>
- [Dados XML no SQL Server](xml-data-sql-server.md)
