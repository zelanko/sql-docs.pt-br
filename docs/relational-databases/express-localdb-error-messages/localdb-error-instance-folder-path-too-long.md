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
ms.openlocfilehash: 3db8328576d69fe32cea28d3596c5f9b1658d7b2
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67995817"
---
# <a name="localdb_error_instance_folder_path_too_long"></a>LOCALDB_ERROR_INSTANCE_FOLDER_PATH_TOO_LONG
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|260|  
|Origem do Evento|Runtime de banco de dados local do SQL Server 12.0|  
|Componente|API do runtime de banco de dados local|  
|Texto da mensagem|O comprimento do caminho completo da pasta da instância do Banco de Dados Local é maior que MAX_PATH. A instância deve ser armazenada na pasta:%% LOCALAPPDATA%% \ Microsoft\Microsoft SQL Server local\\ DB\Instances<nome\>da instância.|  
  
## <a name="explanation"></a>Explicação  
 O caminho em que a instância deve estar armazenada não é maior que MAX_PATH.  
  
## <a name="user-action"></a>Ação do usuário  
 Crie um novo caminho mais curto que MAX_PATH.  
  
  
