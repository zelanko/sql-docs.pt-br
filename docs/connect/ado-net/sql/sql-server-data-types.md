---
title: Tipos de dados do SQL Server e do ADO.NET
description: Descreve como trabalhar com tipos de dados do SQL Server e como eles interagem com os tipos de dados do .NET.
ms.date: 08/15/2019
ms.assetid: 81b43550-23e8-43bb-b460-7eb8ac825c33
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 12ad13d6788ae2b8995289100883b06c5ab6d7c6
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452030"
---
# <a name="sql-server-data-types-and-adonet"></a>Tipos de dados do SQL Server e do ADO.NET

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Download ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

SQL Server e o .NET são baseados em sistemas de tipos diferentes, o que pode resultar em potencial perda de dados. Para preservar a integridade dos dados, o Microsoft SqlClient Provedor de Dados for SQL Server (<xref:Microsoft.Data.SqlClient>) fornece métodos de acessadores tipados para trabalhar com dados de SQL Server. Você pode usar as enumerações nas classes de <xref:System.Data.SqlDbType> para especificar <xref:Microsoft.Data.SqlClient.SqlParameter> tipos de dados.  
  
SQL Server 2008 apresenta novos tipos de dados que são projetados para atender às necessidades de negócios para trabalhar com dados de data e hora, estruturados, semiestruturados e não estruturados. Eles estão documentados nos manuais online do SQL Server 2008.  
  
Os tipos de dados SQL Server que estão disponíveis para uso em seu aplicativo dependem da versão do SQL Server que você está usando. Para obter mais informações, consulte [tipos de dados (mecanismo de banco de dados)](https://go.microsoft.com/fwlink/?LinkID=107468) de manuais online do SQL Server.
  
## <a name="in-this-section"></a>Nesta seção  
[SqlTypes e o DataSet](sqltypes-dataset.md)  
Descreve o suporte de tipo para `SqlTypes` no `DataSet`.  
  
[Manipulando valores nulos](handle-null-values.md)  
Demonstra como trabalhar com valores nulos e lógica de três valores.  
  
[Comparando valores de GUID e uniqueidentifier](compare-guid-uniqueidentifier-values.md)  
Demonstra como trabalhar com valores de GUID e uniqueidentifier em SQL Server e .NET.  
  
[Dados de data e hora](date-time-data.md)  
Descreve como usar os novos tipos de dados de data e hora introduzidos no SQL Server 2008.  
  
[UDTs grandes](large-udts.md)  
Demonstra como recuperar dados de UDTs de valor grande introduzidos no SQL Server 2008.  
  
[Dados XML no SQL Server](xml-data-sql-server.md)  
Descreve como trabalhar com dados XML recuperados do SQL Server.  
  
## <a name="reference"></a>Referência  
<xref:System.Data.DataSet>  
Descreve a classe `DataSet` e todos os seus membros.  
  
<xref:System.Data.SqlTypes>  
Descreve o namespace `SqlTypes` e todos os seus membros.  
  
<xref:System.Data.SqlDbType>  
Descreve a enumeração de `SqlDbType` e todos os seus membros.  
  
<xref:System.Data.DbType>  
Descreve a enumeração de `DbType` e todos os seus membros.  
  
## <a name="next-steps"></a>Próximas etapas
- [Parâmetros com valor de tabela](table-valued-parameters.md)
- [Dados binários e de valor grande do SQL Server](sql-server-binary-large-value-data.md)
