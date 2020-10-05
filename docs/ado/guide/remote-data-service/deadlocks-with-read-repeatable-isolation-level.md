---
description: Deadlocks com o nível de isolamento repetível de leitura
title: Deadlocks com nível de isolamento replicável de leitura | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- deadlocks in RDS [ADO]
- read repeatable in RDS [ADO]
ms.assetid: 29f3683f-12f3-4304-8a54-fe133c25a423
author: rothja
ms.author: jroth
ms.openlocfilehash: 46444bf6e34278af9ca80f56f7d3bfdea1f3feef
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91724727"
---
# <a name="deadlocks-with-read-repeatable-isolation-level"></a>Deadlocks com o nível de isolamento repetível de leitura
Se um objeto comercial personalizado usar um nível de isolamento de leitura reproduzível para acessar um SQL Server e o objeto comercial for chamado simultaneamente por dois clientes que enviam uma consulta e são atualizados na mesma transação, um deadlock é possível. O serviço de dados remoto foi projetado para permitir que um dos processos expire para liberar o deadlock, mas a atualização falhará para esse cliente.  
  
 Use a propriedade dinâmica **tempo limite do comando** do [serviço de cursor](../appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) para modificar o comprimento do tempo limite.  
  
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](/dotnet/framework/wcf/).  
  
## <a name="see-also"></a>Consulte Também  
 [Conceitos básicos do RDS](./rds-fundamentals.md)