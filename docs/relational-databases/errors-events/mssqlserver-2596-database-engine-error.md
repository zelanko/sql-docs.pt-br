---
title: MSSQLSERVER_2596 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 2596 (Database Engine error)
ms.assetid: 49ab892f-8ba3-4ba1-b562-ddf205019802
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 8d39e007653bfdccd68ad9b5a2705b629d1e9979
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68022956"
---
# <a name="mssqlserver_2596"></a>MSSQLSERVER_2596
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|2596|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DBCC_DATABASE_IN_READ_ONLY_MODE|  
|Texto da mensagem|A instrução de correção não foi processada. O banco de dados não pode ficar no modo somente leitura.|  
  
## <a name="explanation"></a>Explicação  
Essa mensagem indica que o banco de dados está no modo somente leitura. Não é possível fazer correções quando um banco de dados está no modo somente leitura.  
  
## <a name="user-action"></a>Ação do usuário  
Defina o banco de dados como leitura/gravação usando ALTER DATABASE e, em seguida, execute o comando DBCC novamente.  
  
## <a name="see-also"></a>Consulte Também  
[ALTER DATABASE &#40;Transact-SQL&#41;](~/t-sql/statements/alter-database-transact-sql-set-options.md)  
  
