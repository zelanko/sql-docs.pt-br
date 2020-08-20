---
description: MSSQLSERVER_7308
title: MSSQLSERVER_7308 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 7308 (Database Engine error)
- single-threaded apartment mode
ms.assetid: cca9eab9-afb9-463d-abfd-0802257e2c99
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 568cf7ae707b3e0b8da28b0a6c0ae9b076267c6f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487013"
---
# <a name="mssqlserver_7308"></a>MSSQLSERVER_7308
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |  
| :-------- | :---- |  
|Nome do Produto|SQL Server|  
|ID do evento|7308|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|RMT_STA_DISABLED|  
|Texto da mensagem|Não é possível usar o provedor OLE DB '%ls' para consultas distribuídas porque ele está configurado para execução no modo STA.|  
  
## <a name="explanation"></a>Explicação  
Você usou um provedor OLE DB configurado para execução no modo STA. Provedores do OLE DB executados no modo STA não podem ser usados para consultas distribuídas.  
  
## <a name="user-action"></a>Ação do usuário  
Para resolver o erro, configure o provedor para execução no modo MTA. Se o provedor não tiver suporte para MTA e não for possível atualizá-lo para uma versão com suporte a MTA, considere configurá-lo para execução fora do processo. O fornecedor do provedor deverá ser capaz de informar se o provedor dá suporte para MTA ou execução fora do processo.  
  
