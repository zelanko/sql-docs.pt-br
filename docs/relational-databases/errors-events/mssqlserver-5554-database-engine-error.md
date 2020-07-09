---
title: MSSQLSERVER_5554 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 5554 (Database Engine error)
ms.assetid: 7134bbe5-d240-4a98-85ce-b13cc8ae9b0e
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 20bfb8f859cbb6bfd1ca6a113556ff1f5902977a
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85728356"
---
# <a name="mssqlserver_5554"></a>MSSQLSERVER_5554
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |  
| :-------- | :---- |  
|Nome do Produto|MSSQLSERVER|  
|ID do evento|5554|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|FS_MINIVER_OVERFLOW|  
|Texto da mensagem|O número total de versões para um único arquivo atingiu o limite máximo definido pelo sistema de arquivos.|  
  
## <a name="explanation"></a>Explicação  
No MARS (conjunto de resultados ativos múltiplos) ou em cenários de gatilho, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa a miniversão especificada pelo sistema operacional.  
  
## <a name="user-action"></a>Ação do usuário  
Tente evitar atualizações repetidas nos dados da mesma transação.  
  
