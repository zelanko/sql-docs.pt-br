---
title: Classe de evento PreConnect:Completed | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- PreConnect:Completed Event Class
ms.assetid: 7ed2f620-6511-4985-9961-d2927c2b1759
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: bc4b65a9ffe3873401271d0bfcf0cf669a82c0b9
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85733773"
---
# <a name="preconnectcompleted-event-class"></a>Classe de evento PreConnect:Completed
[!INCLUDE [SQL Server - ASDB](../../includes/applies-to-version/sql-asdb.md)]
  A classe de evento PreConnect:Completed indica quando um gatilho LOGON ou a função de classificação do Administrador de Recursos conclui a execução.  
  
## <a name="preconnectcompleted-event-class-data-columns"></a>Colunas de dados da classe de evento PreConnect:Completed  
  
|Nome da coluna de dados|Tipo de dados|DESCRIÇÃO|ID da coluna|Filtrável|  
|----------------------|---------------|-----------------|---------------|----------------|  
|EventClass|**int**|216|27|Não|  
|SPID|**int**|O ID de processo de servidor que dispara este evento.|12|Sim|  
|EventSubClass|**int**|1 para a função de classificador definida pelo usuário.|21|Sim|  
|StartTime|**datetime**|A hora que inicia a função de classificador definida pelo usuário.|14|Sim|  
|EndTime|**datetime**|A hora que inicia a função de classificador definida pelo usuário.|15|Sim|  
|Duration|**bigint**|O número de hora, em microssegundo, usado pela função de classificação.|13|Sim|  
|ObjectID|**int**|A ID do objeto do classificador definido pelo usuário.|22|Sim|  
|CPU|**int**|Uso de CPU em milissegundos.|18|Sim|  
|Leituras|**int**|O número de leituras lógicas.|16|Sim|  
|Gravações|**int**|O número de gravações lógicas.|17|Sim|  
|GroupID|**int**|O ID do grupo de cargas de trabalho classificado.|66|Sim|  
|Erro|**int**|O último número do erro, caso a função de classificação definida pelo usuário não seja executada.|31|Sim|  
|Estado|**int**|O estado do último erro.|30|Sim|  
|TargetUserName|**sysname**|O valor de retorno (nome do grupo de cargas de trabalho) para a função de classificação definida pelo usuário, caso o sistema não consiga encontrar um grupo ativo correspondente. Caso contrário, essa coluna será definida como NULL.|39|Sim|  
|ObjectName|**nvarchar(256)**|O nome de duas partes da função de classificador definida pelo usuário. Por exemplo, dbo.classifier.|34|Sim|  
  
## <a name="see-also"></a>Consulte Também  
 [Eventos estendidos](../../relational-databases/extended-events/extended-events.md)   
 [Classe de evento PreConnect:Starting](../../relational-databases/event-classes/preconnect-starting-event-class.md)   
 [Resource Governor](../../relational-databases/resource-governor/resource-governor.md)  
  
  
