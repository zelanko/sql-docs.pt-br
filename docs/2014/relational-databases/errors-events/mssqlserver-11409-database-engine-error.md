---
title: MSSQLSERVER_11409 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 11409 (Database Engine error)
ms.assetid: 99b71a1c-a72d-4ca9-9d00-4230c9042ba5
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 6573f54651188ab5d7eed352db13a521c05f8923
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/21/2020
ms.locfileid: "86553958"
---
# <a name="mssqlserver_11409"></a>MSSQLSERVER_11409
    
## <a name="details"></a>Detalhes  
  
|Atributo|Valor|  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|11409|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|ALTERCOL_COLSET_DROP|  
|Texto da mensagem|Não é possível remover o conjunto de colunas '%.*ls' na tabela '%.\*ls' porque ela contém mais de 1.025 colunas.|  
  
## <a name="explanation"></a>Explicação  
 As tabelas podem conter no máximo 1024 colunas que não estejam designadas como esparsas ou computadas. Quando colunas esparsas fazem com que a tabela exceda as 1024 colunas, é necessário definir um conjunto de colunas para ela. A tabela referenciada tem mais de 1024 colunas, e você tentou remover o conjunto de colunas.  
  
## <a name="user-action"></a>Ação do usuário  
 Com as colunas atuais da tabela, você deve reter o conjunto de colunas.  
  
 Para remover o conjunto de colunas, remova primeiro as colunas da tabela até que o número de colunas não ultrapasse 1024. Em seguida, você poderá remover o conjunto de colunas.  
  
  
