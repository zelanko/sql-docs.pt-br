---
title: MSSQLSERVER_41307 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 41307 (Database Engine error)
ms.assetid: 56f56410-b07d-4379-b01c-702c95761070
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: e3442e56275c3ebae663cab1e027ab82298081c8
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85694608"
---
# <a name="mssqlserver_41307"></a>MSSQLSERVER_41307
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |  
| :-------- | :---- |  
|Nome do Produto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|ID do evento|41307|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|HK_HEKATON_ROW_LIMIT|  
|Texto da mensagem|O limite de tamanho de linha de *number* bytes para tabelas com otimização de memória foi excedido. Simplifique a definição da tabela.|  
  
## <a name="explanation"></a>Explicação  
O limite de tamanho de linha para tabelas com otimização de memória é 8.060 bytes. Para obter mais informações, consulte [Tamanho da tabela e da linha em tabelas com otimização de memória](~/relational-databases/in-memory-oltp/table-and-row-size-in-memory-optimized-tables.md). Para obter mais informações, veja [OLTP in-memory &#40;Otimização na memória&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  
## <a name="see-also"></a>Consulte Também  
[OLTP in-memory &#40;Otimização na memória&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
