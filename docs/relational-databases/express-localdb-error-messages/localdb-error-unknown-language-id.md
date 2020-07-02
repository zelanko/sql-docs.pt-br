---
title: LOCALDB_ERROR_UNKNOWN_LANGUAGE_ID | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: reference
ms.assetid: fa082dca-bf88-46e7-b61e-7ac8835a3493
author: stevestein
ms.author: sstein
ms.openlocfilehash: 488199547cd5b96190b30ab415b08f9be2b4bd66
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85641270"
---
# <a name="localdb_error_unknown_language_id"></a>LOCALDB_ERROR_UNKNOWN_LANGUAGE_ID
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|270|  
|Origem do Evento|Runtime de banco de dados local do SQL Server 12.0|  
|Componente|API do runtime de banco de dados local|  
|Texto da mensagem|Erro ao obter a mensagem de erro localizada: O idioma especificado pelo parâmetro 'ID do idioma' é desconhecido.|  
  
## <a name="explanation"></a>Explicação  
 O idioma solicitado para a mensagem de erro de Runtime do Banco de Dados Local é desconhecido ou não tem suporte.  
  
## <a name="user-action"></a>Ação do usuário  
 Tente solicitar um dos idiomas com suporte para mensagens de erro de Runtime de Banco de Dados Local ou um idioma padrão.  
  
  
