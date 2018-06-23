---
title: MSSQLSERVER_7308 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 7308 (Database Engine error)
- single-threaded apartment mode
ms.assetid: cca9eab9-afb9-463d-abfd-0802257e2c99
caps.latest.revision: 7
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 6a85c217cc88367f287b2d60ee56be4183ea1850
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36009762"
---
# <a name="mssqlserver7308"></a>MSSQLSERVER_7308
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|7308|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|RMT_STA_DISABLED|  
|Texto da mensagem|Não é possível usar o provedor OLE DB '%ls' para consultas distribuídas porque ele está configurado para execução no modo STA.|  
  
## <a name="explanation"></a>Explicação  
 Você usou um provedor OLE DB configurado para execução no modo STA. Provedores do OLE DB executados no modo STA não podem ser usados para consultas distribuídas.  
  
## <a name="user-action"></a>Ação do usuário  
 Para resolver o erro, configure o provedor para execução no modo MTA. Se o provedor não tiver suporte para MTA e não for possível atualizá-lo para uma versão com suporte a MTA, considere configurá-lo para execução fora do processo. O fornecedor do provedor deverá ser capaz de informar se o provedor dá suporte para MTA ou execução fora do processo.  
  
  