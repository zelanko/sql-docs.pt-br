---
title: MSSQLSERVER_12304 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 12304 (Database Engine error)
ms.assetid: a2c252c2-e815-4ac8-a101-7af5b32e3233
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d6c4ad312340df31e5a5c1d689cefe2f30f97f85
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62860639"
---
# <a name="mssqlserver12304"></a>MSSQLSERVER_12304
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|12304|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|HK_UNSUPPORTED_IDENTITY_TABLE_VAR|  
|Texto da mensagem|Usar um tipo de tabela com otimização de memória que usa a propriedade IDENTITY com qualquer uma de suas colunas não tem suporte ao usar o tipo fora do contexto de um procedimento armazenado compilado nativamente.|  
  
## <a name="user-action"></a>Ação do usuário  
Não use um tipo de tabela com otimização de memória que usa a propriedade de identidade com qualquer uma de suas colunas.  
  
## <a name="see-also"></a>Consulte Também  
[OLTP in-memory &#40;Otimização na memória&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
