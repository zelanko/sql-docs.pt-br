---
title: Operações de dados do SQL Server no ADO.NET
description: Descreve como trabalhar com os dados no SQL Server. Contém seções sobre operações de cópia em massa, MARS, operações assíncronas e parâmetros com valor de tabela.
ms.date: 08/15/2019
ms.assetid: b864ebc9-ed8e-4059-85fd-36d9198f5521
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: aea8e0ecbb542645f0553e8bf34172381f37929b
ms.sourcegitcommit: 610e49c3e1fa97056611a85e31e06ab30fd866b1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/07/2020
ms.locfileid: "78896637"
---
# <a name="sql-server-data-operations-in-adonet"></a>Operações de dados do SQL Server no ADO.NET

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

Esta seção descreve a funcionalidade e os recursos do SQL Server específicos para o Provedor de Dados do Microsoft SqlClient para SQL Server (<xref:Microsoft.Data.SqlClient>).  
  
## <a name="in-this-section"></a>Nesta seção  
[Operações de cópia em massa no SQL Server](bulk-copy-operations-sql-server.md)  
Descreve a funcionalidade de cópia em massa para o Provedor de Dados .NET para SQL Server.  
  
[MARS (conjunto de resultados ativos múltiplos)](multiple-active-result-sets-mars.md)  
Descreve como ter mais de um <xref:Microsoft.Data.SqlClient.SqlDataReader> aberto em uma conexão quando cada instância de <xref:Microsoft.Data.SqlClient.SqlDataReader> é iniciada a partir de um comando separado.  
  
[Operações assíncronas](asynchronous-operations.md)  
Descreve como executar operações de banco de dados assíncronas usando uma API que é modelada após o modelo assíncrono usado pelo .NET Framework.  
  
[Parâmetros com valor de tabela](table-valued-parameters.md)  
Descreve como trabalhar com parâmetros com valor de tabela introduzidos no SQL Server 2008.  
  
## <a name="next-steps"></a>Próximas etapas
- [SQL Server e ADO.NET](index.md)
