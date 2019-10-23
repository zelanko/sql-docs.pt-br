---
title: SqlTypes e o DataSet
description: Descreve o suporte de tipo para SqlTypes no DataSet.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 9172c20a-9876-4b3b-9c97-1963c02b1993
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 70efb8615a70677c709abd6d9129c63de9420ffc
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72451988"
---
# <a name="sqltypes-and-the-dataset"></a>SqlTypes e o DataSet

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Download ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

O ADO.NET 2,0 introduziu suporte de tipo avançado para o `DataSet` por meio do namespace <xref:System.Data.SqlTypes>. Os tipos em <xref:System.Data.SqlTypes> são projetados para fornecer tipos de dados com a mesma semântica e precisão que os tipos de dados em um banco de SQL Server. Cada tipo de dados no <xref:System.Data.SqlTypes> tem um tipo de dados equivalente em SQL Server, com a mesma representação de dados subjacente.  
  
Usar <xref:System.Data.SqlTypes> diretamente em um <xref:System.Data.DataSet> confere vários benefícios ao trabalhar com SQL Server tipos de dados. <xref:System.Data.SqlTypes> dá suporte à mesma semântica que SQL Server tipos de dados nativos. A especificação de um dos <xref:System.Data.SqlTypes> na definição de um <xref:System.Data.DataColumn> elimina a perda de precisão que pode ocorrer ao converter tipos de dados decimais ou numéricos em um dos tipos de dados Common Language Runtime (CLR).  

O exemplo a seguir cria um objeto <xref:System.Data.DataTable>, definindo explicitamente os tipos de dados de <xref:System.Data.DataColumn> usando <xref:System.Data.SqlTypes> em vez de tipos CLR. O código preenche a <xref:System.Data.DataTable> com dados da tabela Sales. SalesOrderDetail no banco de dados AdventureWorks em SQL Server. A saída exibida na janela do console mostra o tipo de dados de cada coluna e os valores recuperados de SQL Server.  
  
[!code-csharp[DataWorks DataColumn_DataType#1](~/../sqlclient/doc/samples/DataColumn_DataType.cs#1)]
