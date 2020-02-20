---
title: SqlTypes e o DataSet
description: Descreve a compatibilidade de tipo para SqlTypes no DataSet.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 9172c20a-9876-4b3b-9c97-1963c02b1993
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: a7ef43ca6afa243e313e8e38bdd05d929161e71f
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "75233787"
---
# <a name="sqltypes-and-the-dataset"></a>SqlTypes e o DataSet

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Download ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

O ADO.NET 2.0 introduziu a compatibilidade com tipo avançada para `DataSet` por meio do namespace <xref:System.Data.SqlTypes>. Os tipos em <xref:System.Data.SqlTypes> são projetados para fornecer tipos de dados com a mesma semântica e precisão que os tipos de dados em um banco de dados SQL Server. Cada tipo de dados no <xref:System.Data.SqlTypes> tem um tipo de dados equivalente em SQL Server, com a mesma representação de dados subjacente.  
  
Usar <xref:System.Data.SqlTypes> diretamente em um <xref:System.Data.DataSet> confere vários benefícios ao trabalhar com tipos de dados do SQL Server. <xref:System.Data.SqlTypes> é compatível com a mesma semântica que os tipos de dados nativos do SQL Server. A especificação de um dos <xref:System.Data.SqlTypes> na definição de um <xref:System.Data.DataColumn> elimina a perda de precisão que pode ocorrer ao converter tipos de dados decimais ou numéricos em um dos tipos de dados de CLR (Common Language Runtime).  

O exemplo a seguir cria um objeto <xref:System.Data.DataTable>, definindo explicitamente os tipos de dados de <xref:System.Data.DataColumn> usando <xref:System.Data.SqlTypes> em vez de tipos CLR. O código preenche a <xref:System.Data.DataTable> com os dados da tabela Sales.SalesOrderDetail no banco de dados AdventureWorks no SQL Server. A saída exibida na janela do console mostra o tipo de dados de cada coluna e os valores recuperados do SQL Server.  
  
[!code-csharp[DataWorks DataColumn_DataType#1](~/../sqlclient/doc/samples/DataColumn_DataType.cs#1)]
