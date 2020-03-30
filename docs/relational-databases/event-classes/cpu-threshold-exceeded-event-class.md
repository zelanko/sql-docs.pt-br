---
title: Classe de evento CPU Threshold Exceeded | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- CPU Threshold Exceeded Event Class
ms.assetid: eb106f7d-baa3-4a2b-96b2-f9fe0844057d
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d74d1907b0f96275658c716a7a08061f0eec8995
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "67999568"
---
# <a name="cpu-threshold-exceeded-event-class"></a>Classe de evento CPU Threshold Exceeded
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  A classe de evento CPU Threshold Exceeded indica que o Administrador de Recursos detecta uma consulta que excede o limite da CPU especificado para REQUEST_MAX_CPU_TIME_SEC.  
  
> [!NOTE]  
>  O intervalo de detecção para esse evento é cinco segundos. Há garantia de que um evento será gerado se uma consulta exceder o limite especificado em pelo menos cinco segundos. Contudo, se uma consulta exceder o limite especificado em menos de cinco segundos, sua detecção poderá ser perdida, dependendo do controle de tempo da consulta e da hora da última varredura de detecção.  
  
## <a name="cpu-threshold-exceeded-data-columns"></a>Colunas de dados de CPU Threshold Exceeded  
  
|Nome da coluna de dados|Tipo de dados|DESCRIÇÃO|ID da coluna|Filtrável|  
|----------------------|---------------|-----------------|---------------|----------------|  
|CPU|**int**|Uso de CPU em milissegundos.|18|Sim|  
|EventClass|**int**|214|27|Não|  
|EventSubClass|**int**|Violação de limite da CPU.|21|Sim|  
|GroupID|**int**|ID do grupo onde a violação ocorreu.|66|Sim|  
|OwnerID|**int**|SPID do processo que causou a violação.|58|Sim|  
|SPID|**int**|ID do processo de servidor que dispara este evento.<br /><br /> Observação: poderá ser diferente do verdadeiro SPID do usuário se um thread de sistema validar o uso da CPU como uma tarefa em segundo plano.|12|Sim|  
|StartTime|**datetime**|A hora em que esse evento foi disparado.|14|Sim|  
  
## <a name="see-also"></a>Consulte Também  
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)  
  
  
