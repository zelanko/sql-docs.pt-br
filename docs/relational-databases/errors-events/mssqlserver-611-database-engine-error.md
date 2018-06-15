---
title: MSSQLSERVER_611 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 611 (Database Engine error)
ms.assetid: ac6a213f-5c38-44ad-bc85-a62863786614
caps.latest.revision: 19
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e118451f77e736da34edad35d7e1c64ec95bad37
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2018
ms.locfileid: "34324987"
---
# <a name="mssqlserver611"></a>MSSQLSERVER_611
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
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
  
