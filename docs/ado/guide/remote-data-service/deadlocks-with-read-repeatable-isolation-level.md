---
title: Deadlocks com o nível de isolamento repetível de leitura | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- deadlocks in RDS [ADO]
- read repeatable in RDS [ADO]
ms.assetid: 29f3683f-12f3-4304-8a54-fe133c25a423
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c8e4e59606f3b68fbd9ce272db8ea8a50ab53e88
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67922712"
---
# <a name="deadlocks-with-read-repeatable-isolation-level"></a>Deadlocks com o nível de isolamento repetível de leitura
Se um objeto comercial personalizado usa um nível de isolamento de leitura repetível para acessar um SQL Server e o objeto de negócios é chamado simultaneamente por dois clientes que enviar uma consulta e atualização na mesma transação, um deadlock é possível. Serviço de dados remoto foi projetado para permitir que um dos processos de tempo limite para liberar o bloqueio, mas a atualização falhará para esse cliente.  
  
 Use o [serviço de Cursor](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) **tempo limite do comando** propriedade dinâmica para modificar o período de tempo limite.  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (consulte o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Devem ser migrados para aplicativos que usam o RDS [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="see-also"></a>Consulte também  
 [Conceitos básicos do RDS](../../../ado/guide/remote-data-service/rds-fundamentals.md)



