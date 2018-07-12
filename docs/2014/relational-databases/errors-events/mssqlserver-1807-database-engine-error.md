---
title: MSSQLSERVER_1807 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 1807 (Database Engine error)
ms.assetid: 13c1b240-098b-4d9e-89aa-21599548e074
caps.latest.revision: 17
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4a9df8969a0dbae5dbdb2959c621f287d08c9f75
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37420695"
---
# <a name="mssqlserver1807"></a>MSSQLSERVER_1807
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|1807|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|CANNOT_EX_LOCK|  
|Texto da mensagem|Não foi possível obter bloqueio exclusivo no banco de dados '%.*ls'. Tente novamente a operação mais tarde.|  
  
## <a name="explanation"></a>Explicação  
 Uma operação que exigia acesso exclusivo ao banco de dados não pôde obtê-lo.  
  
## <a name="user-action"></a>Ação do usuário  
 Desconecte todas as conexões com esse banco de dados ou tente a consulta novamente mais tarde.  
  
  
