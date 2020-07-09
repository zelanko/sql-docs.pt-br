---
title: MSSQLSERVER_611 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 611 (Database Engine error)
ms.assetid: ac6a213f-5c38-44ad-bc85-a62863786614
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 92875014b61628330f42a2ee9e631eb4b3b89ba9
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85733804"
---
# <a name="mssqlserver_611"></a>MSSQLSERVER_611
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |  
| :-------- | :---- |  
|Nome do Produto|SQL Server|  
|ID do evento|611|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|VAR_SIZE_TOO_BIG|  
|Texto da mensagem|Não é possível inserir ou atualizar uma linha porque o tamanho total da coluna variável, incluindo a sobrecarga, está %d bytes acima do limite.|  
  
## <a name="explanation"></a>Explicação  
O tamanho máximo da coluna variável é maior que o permitido pelo esquema. O erro 611 é retornado quando a coluna variável está acima do limite no caso fixo quando o formato de armazenamento vardecimal está habilitado ou quando o tamanho da coluna variável está acima do limite permitido no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] para um registro de dados compactado.  
  
## <a name="user-action"></a>Ação do usuário  
Reduza o tamanho do registro.  
  
