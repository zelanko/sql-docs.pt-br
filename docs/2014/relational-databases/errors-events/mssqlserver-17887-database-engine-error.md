---
title: MSSQLSERVER_17887 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 17887 (Database Engine error)
ms.assetid: ad0806e6-3296-4c32-b103-fccf0f8a8d3d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3de0d505f99fd1f8f7da968bde13eb56fe50efc1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62915203"
---
# <a name="mssqlserver17887"></a>MSSQLSERVER_17887
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|17887|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|SRV_IO_COMP_LISTENER_NONYIELDING|  
|Texto da mensagem|Ouvinte de Conclusão de E/S (0x%lx) Trabalho 0x%p parece não estar respondendo no Nó %ld. Quant. aprox. de CPU usada: kernel %I64d ms, usuário %I64d ms, Intervalo: %I64d.|  
  
## <a name="explanation"></a>Explicação  
 Indica que há um problema possível com o Ouvinte de Porta de Conclusão de E/S no nó especificado ao executar a rotina de Conclusão de E/S para um evento de leitura/gravação de rede. Este erro será removido quando o Ouvinte de Porta de Conclusão de E/S retornar da execução da rotina de Conclusão de E/S.  
  
## <a name="user-action"></a>Ação do usuário  
 Contate os Serviços de Atendimento ao Cliente da Microsoft (CSS).  
  
  
