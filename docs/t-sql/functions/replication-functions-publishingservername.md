---
title: PUBLISHINGSERVERNAME (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- PUBLISHINGSERVERNAME_TSQL
- PUBLISHINGSERVERNAME
dev_langs:
- TSQL
helpviewer_keywords:
- PUBLISHINGSERVERNAME function
- Publishers [SQL Server replication], names
ms.assetid: e7c278e5-ab23-419e-ab3e-3bb20b0636df
caps.latest.revision: 16
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a5aeeb414f9c980429d20f123e1f9c986b147eee
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="replication-functions---publishingservername"></a>Funções de replicação - PUBLISHINGSERVERNAME
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna o nome do Publicador de origem de um banco de dados publicado que participa de uma sessão de espelhamento de banco de dados. Esta função é executada em uma instância de Publicador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no banco de dados de publicação. Use-a para determinar o Publicador original do banco de dados publicado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
PUBLISHINGSERVERNAME()  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 **nvarchar**  
  
## <a name="remarks"></a>Comentários  
 PUBLISHINGSERVERNAME é usada em todos os tipos de replicação.  
  
 PUBLISHINGSERVERNAME é usada quando há uma sessão de espelhamento de banco de dados no banco de dados de publicação entre o Publicador e a instância parceira espelho.  
  
 Essa função deve ser executada dentro do contexto de um banco de dados de publicação. Quando PUBLISHINGSERVERNAME é executada em um banco de dados de publicação na instância de servidor espelho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o nome da instância do Publicador de origem do banco de dados publicado é retornado. Quando esta é executada em um banco de dados publicador na instância de servidor espelho não publicada ou que seja publicada pela instância de servidor espelho após um failover, o nome da instância de servidor de espelho é retornado. Quando esta função for executada na instância do Publicador original, o nome do Publicador será retornado.  
  
## <a name="see-also"></a>Consulte também  
 [Espelhamento e replicação de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-and-replication-sql-server.md)   
 [Funções de replicação &#40; Transact-SQL &#41;](http://msdn.microsoft.com/library/53702dee-de58-47d5-a552-7f32000f77d4)  
  
  

