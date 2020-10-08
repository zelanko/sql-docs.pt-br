---
title: Tipos de dados do SQL Server e do ADO.NET
description: Descreve como trabalhar com tipos de dados do SQL Server e como eles interagem com os tipos de dados do .NET.
ms.date: 08/15/2019
ms.assetid: 81b43550-23e8-43bb-b460-7eb8ac825c33
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-kaywon
ms.openlocfilehash: 57e0cec178c407cda530e6699e51743094c57dca
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91725587"
---
# <a name="sql-server-data-types-and-adonet"></a>Tipos de dados do SQL Server e do ADO.NET

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

O SQL Server e o .NET são baseados em sistemas de tipos diferentes, o que pode resultar em potencial perda de dados. Para preservar a integridade dos dados, o Provedor de Dados do Microsoft SqlClient para SQL Server (<xref:Microsoft.Data.SqlClient>) fornece métodos de acessadores tipados para trabalhar com os dados do SQL Server. Você pode usar as enumerações nas classes de <xref:System.Data.SqlDbType> para especificar tipos de dados <xref:Microsoft.Data.SqlClient.SqlParameter>.  
  
O SQL Server 2008 apresenta novos tipos de dados criados para atender às necessidades empresariais para trabalhar usando dados de data e hora, estruturados, semiestruturados e não estruturados. Eles são documentados nos Manuais Online do SQL Server 2008.  
  
Os tipos de dados do SQL Server disponíveis para uso em seu aplicativo dependem da versão do SQL Server que você está usando. Para obter mais informações, confira [Tipos de Dados (Mecanismo de Banco de Dados)](/previous-versions/sql/sql-server-2008-r2/ms187594(v=sql.105)) nos Manuais Online do SQL Server.
  
## <a name="in-this-section"></a>Nesta seção  
[SqlTypes e o DataSet](sqltypes-dataset.md)  
Descreve o suporte de tipo para `SqlTypes` no `DataSet`.  
  
[Manipulando valores nulos](handle-null-values.md)  
Demonstra como trabalhar com valores nulos e lógica de três valores.  
  
[Comparando valores de GUID e uniqueidentifier](compare-guid-uniqueidentifier-values.md)  
Demonstra como trabalhar com valores de GUID e uniqueidentifier no SQL Server e .NET.  
  
[Dados de data e hora](date-time-data.md)  
Descreve como usar os novos tipos de dados de data e hora introduzidos no SQL Server 2008.  
  
[UDTs grandes](large-udts.md)  
Demonstra como recuperar dados de UDTs de valor grande introduzidos no SQL Server 2008.  
  
[Dados XML no SQL Server](xml-data-sql-server.md)  
Descreve como trabalhar com os dados XML recuperados do SQL Server.  
  
## <a name="reference"></a>Referência  
<xref:System.Data.DataSet>  
Descreve a classe `DataSet` e todos os membros dela.  
  
<xref:System.Data.SqlTypes>  
Descreve o namespace `SqlTypes` e todos os membros dele.  
  
<xref:System.Data.SqlDbType>  
Descreve a enumeração `SqlDbType` e todos os membros dela.  
  
<xref:System.Data.DbType>  
Descreve a enumeração `DbType` e todos os membros dela.  
  
## <a name="next-steps"></a>Próximas etapas
- [Parâmetros com valor de tabela](table-valued-parameters.md)
- [Dados binários e de valor grande do SQL Server](sql-server-binary-large-value-data.md)