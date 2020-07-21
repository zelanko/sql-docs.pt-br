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
ms.openlocfilehash: b889779da7f48ffd52d55c63e2ddb0742c065e59
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/21/2020
ms.locfileid: "86553501"
---
# <a name="mssqlserver_17887"></a>MSSQLSERVER_17887
    
## <a name="details"></a>Detalhes  
  
|Atributo|Valor|  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|17887|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|SRV_IO_COMP_LISTENER_NONYIELDING|  
|Texto da mensagem|Ouvinte de Conclusão de E/S (0x%lx) Trabalho 0x%p parece não estar respondendo no Nó %ld. Quant. aprox. de CPU usada: kernel %I64d ms, usuário %I64d ms, Intervalo: %I64d.|  
  
## <a name="explanation"></a>Explicação  
 Indica que há um problema possível com o Ouvinte de Porta de Conclusão de E/S no nó especificado ao executar a rotina de Conclusão de E/S para um evento de leitura/gravação de rede. Este erro será removido quando o Ouvinte de Porta de Conclusão de E/S retornar da execução da rotina de Conclusão de E/S.  
  
## <a name="user-action"></a>Ação do usuário  
 Contate os Serviços de Atendimento ao Cliente da Microsoft (CSS).  
  
  
