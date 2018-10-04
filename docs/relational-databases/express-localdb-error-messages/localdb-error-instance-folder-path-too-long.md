---
title: LOCALDB_ERROR_INSTANCE_FOLDER_PATH_TOO_LONG | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: reference
ms.assetid: c178a308-8d99-47fc-8a49-5a480dc592f6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6d4053fd7633d642c0cc139826ca8e30ed3fa3fa
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47777784"
---
# <a name="localdberrorinstancefolderpathtoolong"></a>LOCALDB_ERROR_INSTANCE_FOLDER_PATH_TOO_LONG
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
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
  
  
