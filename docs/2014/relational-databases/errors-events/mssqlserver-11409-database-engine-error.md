---
title: MSSQLSERVER_11409 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 11409 (Database Engine error)
ms.assetid: 99b71a1c-a72d-4ca9-9d00-4230c9042ba5
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: bc894e8b7a058e1f85f4068c9de7eb3a91a62721
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62870162"
---
# <a name="mssqlserver11409"></a>MSSQLSERVER_11409
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|11409|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|ALTERCOL_COLSET_DROP|  
|Texto da mensagem|Não é possível remover o conjunto de colunas '%.*ls' na tabela '%.\*ls' porque ela contém mais de 1.025 colunas.|  
  
## <a name="explanation"></a>Explicação  
As tabelas podem conter no máximo 1024 colunas que não estejam designadas como esparsas ou computadas. Quando colunas esparsas fazem com que a tabela exceda as 1024 colunas, é necessário definir um conjunto de colunas para ela. A tabela referenciada tem mais de 1024 colunas, e você tentou remover o conjunto de colunas.  
  
## <a name="user-action"></a>Ação do usuário  
Com as colunas atuais da tabela, você deve reter o conjunto de colunas.  
  
Para remover o conjunto de colunas, remova primeiro as colunas da tabela até que o número de colunas não ultrapasse 1024. Em seguida, você poderá remover o conjunto de colunas.  
  
