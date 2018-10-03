---
title: LOCALDB_ERROR_INSTANCE_FOLDER_PATH_TOO_LONG | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: reference
ms.assetid: c178a308-8d99-47fc-8a49-5a480dc592f6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1084075fe90a752a07a7abc1feb46679bd9cf5d9
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48058037"
---
# <a name="localdberrorinstancefolderpathtoolong"></a>LOCALDB_ERROR_INSTANCE_FOLDER_PATH_TOO_LONG
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|260|  
|Origem do evento|Tempo de execução de banco de dados local do SQL Server 12.0|  
|Componente|API do tempo de execução de banco de dados local|  
|Texto da mensagem|O comprimento do caminho completo da pasta da instância do Banco de Dados Local é maior que MAX_PATH. A instância deve ser armazenada na pasta: %%LOCALAPPDATA%%\Microsoft\Microsoft SQL Server Local DB\Instances\\< nome da instância\>.|  
  
## <a name="explanation"></a>Explicação  
 O caminho em que a instância deve estar armazenada não é maior que MAX_PATH.  
  
## <a name="user-action"></a>Ação do usuário  
 Crie um novo caminho mais curto que MAX_PATH.  
  
  
