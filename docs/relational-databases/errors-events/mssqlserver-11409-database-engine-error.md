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
ms.openlocfilehash: 8dcb8bba87d83f4127bc7358c45b5f5a7664d46b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47600514"
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
  
