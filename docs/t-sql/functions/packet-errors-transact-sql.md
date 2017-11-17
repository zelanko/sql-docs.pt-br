---
title: '@@PACKET_ERRORS (Transact-SQL) | Microsoft Docs'
ms.custom: 
ms.date: 09/18/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '@@PACKET_ERRORS'
- '@@PACKET_ERRORS_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@PACKET_ERRORS function'
- number of packet errors
- packets [SQL Server], errors
- networking [SQL Server], packet errors
- connections [SQL Server], packets
ms.assetid: f7da1b80-5cbe-42fa-be71-40c6af16383a
caps.latest.revision: 31
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: c6ea46c5187f00190cb39ba9a502b3ecb6a28bc6
ms.openlocfilehash: 57a215132b55d655752db867e0c3dadcced9e92e
ms.contentlocale: pt-br
ms.lasthandoff: 09/19/2017

---
# <a name="x40x40packeterrors-transact-sql"></a>& #x 40; & #x 40. PACKET_ERRORS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna o número de erros de pacote de rede que ocorreram em conexões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] desde a última vez em que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] foi iniciado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
@@PACKET_ERRORS  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 **inteiro**  
  
## <a name="remarks"></a>Comentários  
 Para exibir um relatório que contém várias [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estatísticas, incluindo erros de pacotes, executar **sp_monitor**.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir mostra o uso de `@@PACKET_ERRORS`.  
  
```  
SELECT @@PACKET_ERRORS AS 'Packet Errors';  
```  
  
 Este é um exemplo de conjunto de resultados.  
  
```  
Packet Errors  
-------------  
0  
```  
  
## <a name="see-also"></a>Consulte também  
 [@@PACK_RECEIVED &#40;Transact-SQL&#41;](../../t-sql/functions/pack-received-transact-sql.md)   
 [@@PACK_SENT &#40;Transact-SQL&#41;](../../t-sql/functions/pack-sent-transact-sql.md)   
 [sp_monitor &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-monitor-transact-sql.md)   
 [Funções estatísticas do sistema &#40; Transact-SQL &#41;](../../t-sql/functions/system-statistical-functions-transact-sql.md)  
  
  

