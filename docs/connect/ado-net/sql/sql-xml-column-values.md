---
title: Valores de coluna XML do SQL
description: Demonstra como recuperar e trabalhar com os dados XML recuperados do SQL Server.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: d97ce4da-f09c-4d1e-85b7-a0ccedd7246a
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: aa02072e139c2446ae67086ef43668af4403890c
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "75244007"
---
# <a name="sql-xml-column-values"></a>Valores de coluna XML do SQL

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Download ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

O SQL Server dá suporte ao tipo de dados `xml`, e os desenvolvedores podem recuperar conjuntos de resultados, incluindo esse tipo usando o comportamento padrão da classe <xref:Microsoft.Data.SqlClient.SqlCommand>. Uma coluna `xml` pode ser recuperada da mesma forma que qualquer coluna é recuperada (em um <xref:Microsoft.Data.SqlClient.SqlDataReader>, por exemplo), mas se você quiser trabalhar com o conteúdo da coluna como XML, deverá usar um <xref:System.Xml.XmlReader>.  
  
## <a name="example"></a>Exemplo  
O aplicativo de console a seguir seleciona duas linhas, cada uma contendo uma coluna `xml`, da tabela **Sales.Store** no banco de dados **AdventureWorks** para uma instância do <xref:Microsoft.Data.SqlClient.SqlDataReader>. Para cada linha, o valor da coluna `xml` é lido usando o método <xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlXml%2A> de <xref:Microsoft.Data.SqlClient.SqlDataReader>. O valor é armazenado em <xref:System.Xml.XmlReader>. Observe que você deverá usar <xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlXml%2A> em vez do método <xref:System.Data.IDataRecord.GetValue%2A> se desejar definir o conteúdo para uma variável <xref:System.Data.SqlTypes.SqlXml>; <xref:System.Data.IDataRecord.GetValue%2A> retorna o valor da coluna `xml` como uma cadeia de caracteres.  
  
> [!NOTE]
>  O banco de dados **AdventureWorks** de exemplo não é instalado por padrão quando você instala o SQL Server. Você pode instalá-lo executando a Instalação do SQL Server.  
  
[!code-csharp [SqlDataReader_GetSqlXml#1](~/../sqlclient/doc/samples/SqlDataReader_GetSqlXml.cs#1)]
  
## <a name="next-steps"></a>Próximas etapas
- <xref:System.Data.SqlTypes.SqlXml>
- [Dados XML no SQL Server](xml-data-sql-server.md)
