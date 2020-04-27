---
title: LOCALDB_ERROR_INSTANCE_FOLDER_PATH_TOO_LONG | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: reference
ms.assetid: c178a308-8d99-47fc-8a49-5a480dc592f6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 94439a6981a2cf891a55bcbda7498db83e1fa52e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62990574"
---
# <a name="localdb_error_instance_folder_path_too_long"></a>LOCALDB_ERROR_INSTANCE_FOLDER_PATH_TOO_LONG
    
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
  
  
