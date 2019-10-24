---
title: Operações de dados do SQL Server no ADO.NET
description: Descreve como trabalhar com os dados no SQL Server. Contém seções sobre operações de cópia em massa, MARS, operações assíncronas e parâmetros com valor de tabela.
ms.date: 08/15/2019
ms.assetid: b864ebc9-ed8e-4059-85fd-36d9198f5521
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: ed9beea680575bba7fb01fc56af147e20b39218a
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452045"
---
# <a name="sql-server-data-operations-in-adonet"></a>Operações de dados do SQL Server no ADO.NET

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Download ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

Esta seção descreve SQL Server recursos e funcionalidades que são específicos para o Microsoft SqlClient Provedor de Dados para SQL Server (<xref:Microsoft.Data.SqlClient>).  
  
## <a name="in-this-section"></a>Nesta seção  
[Operações de cópia em massa no SQL Server](bulk-copy-operations-sql-server.md)  
Descreve a funcionalidade de cópia em massa para o Provedor de Dados .NET para SQL Server.  
  
[MARS (conjunto de resultados ativos múltiplos)](multiple-active-result-sets-mars.md)  
Descreve como ter mais de um <xref:Microsoft.Data.SqlClient.SqlDataReader> aberto em uma conexão quando cada instância do <xref:Microsoft.Data.SqlClient.SqlDataReader> é iniciada a partir de um comando separado.  
  
[Operações assíncronas](asynchronous-operations.md)  
Descreve como executar operações de banco de dados assíncronas usando uma API que é modelada após o modelo assíncrono usado pelo .NET Framework.  
  
[Parâmetros com valor de tabela](table-valued-parameters.md)  
Descreve como trabalhar com parâmetros com valor de tabela, que foram introduzidos no SQL Server 2008.  
  
## <a name="next-steps"></a>Próximas etapas
- [SQL Server e ADO.NET](index.md)
