---
title: Dados binários e de valor grande do SQL Server
description: Descreve como trabalhar com os dados de valor grande no SQL Server.
ms.date: 08/15/2019
ms.assetid: e00827b3-7511-4b2d-91d7-851ca86cc6b5
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-kaywon
ms.openlocfilehash: 17a38bd45a467625be467f5fb01f0e733f7546bc
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80920980"
---
# <a name="sql-server-binary-and-large-value-data"></a>Dados binários e de valor grande do SQL Server

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

O SQL Server fornece o especificador `max`, que expande a capacidade de armazenamento dos tipos de dados `varchar`, `nvarchar` e `varbinary`. `varchar(max)`, `nvarchar(max)` e `varbinary(max)` são coletivamente chamados de *tipos de dados do valor grande*. Você pode usar os tipos de dados de valor grande para armazenar até 2^31-1 bytes de dados.  
  
O SQL Server 2008 introduz o atributo FILESTREAM, que não é um tipo de dados, mas um atributo que pode ser definido em uma coluna, permitindo que dados de valor grande sejam armazenados no sistema de arquivos em vez de no banco de dados.  
  
## <a name="in-this-section"></a>Nesta seção  
[Modificando dados de valor grande (máx) no ADO.NET](modify-large-value-max-data.md)  
Descreve como trabalhar com tipos de dados de valores grandes.  
  
[Dados do FILESTREAM](filestream-data.md)  
Descreve como trabalhar usando dados de valor grande armazenados no SQL Server 2008 com o atributo FILESTREAM.  
  
## <a name="next-steps"></a>Próximas etapas
- [Tipos de dados do SQL Server e do ADO.NET](sql-server-data-types.md)
- [Operações de dados do SQL Server no ADO.NET](sql-server-data-operations.md)
