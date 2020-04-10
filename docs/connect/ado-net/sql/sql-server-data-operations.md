---
title: Operações de dados do SQL Server no ADO.NET
description: Descreve como trabalhar com os dados no SQL Server. Contém seções sobre operações de cópia em massa, MARS, operações assíncronas e parâmetros com valor de tabela.
ms.date: 08/15/2019
ms.assetid: b864ebc9-ed8e-4059-85fd-36d9198f5521
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-kaywon
ms.openlocfilehash: f6e842b38291fb704828b9b5a70d0652cfda51e0
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80920986"
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
Descreve como trabalhar com parâmetros com valor de tabela, apresentados no SQL Server 2008.  
  
## <a name="next-steps"></a>Próximas etapas
- [SQL Server e ADO.NET](index.md)
