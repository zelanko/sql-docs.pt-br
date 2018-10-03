---
title: MSSQLSERVER_611 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 611 (Database Engine error)
ms.assetid: ac6a213f-5c38-44ad-bc85-a62863786614
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 634c86066508aae367f90ff6e00b452a81939967
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48060436"
---
# <a name="mssqlserver611"></a>MSSQLSERVER_611
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|611|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|VAR_SIZE_TOO_BIG|  
|Texto da mensagem|Não é possível inserir ou atualizar uma linha porque o tamanho total da coluna variável, incluindo a sobrecarga, está %d bytes acima do limite.|  
  
## <a name="explanation"></a>Explicação  
 O tamanho máximo da coluna variável é maior que o permitido pelo esquema. O erro 611 é retornado quando a coluna variável está acima do limite no caso fixo quando o formato de armazenamento vardecimal está habilitado ou quando o tamanho da coluna variável está acima do limite permitido no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] para um registro de dados compactado.  
  
## <a name="user-action"></a>Ação do usuário  
 Reduza o tamanho do registro.  
  
  
