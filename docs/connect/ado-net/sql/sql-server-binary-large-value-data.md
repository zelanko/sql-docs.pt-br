---
title: Dados binários e de valor grande do SQL Server
description: Descreve como trabalhar com os dados de valor grande no SQL Server.
ms.date: 08/15/2019
ms.assetid: e00827b3-7511-4b2d-91d7-851ca86cc6b5
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: e60f8ce6bc8e7ef05a2de942d8bbc2885095d493
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "75251119"
---
# <a name="sql-server-binary-and-large-value-data"></a>Dados binários e de valor grande do SQL Server

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Download ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

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
