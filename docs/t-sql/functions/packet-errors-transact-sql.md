---
title: '@@PACKET_ERRORS (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 09/18/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 686722bcceaaabd69c2293ec48f71df20352b65a
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85892170"
---
# <a name="x40x40packet_errors-transact-sql"></a>&#x40;&#x40;PACKET_ERRORS (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Retorna o número de erros de pacote de rede que ocorreram em conexões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] desde a última vez em que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] foi iniciado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
@@PACKET_ERRORS  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 **inteiro**  
  
## <a name="remarks"></a>Comentários  
 Para exibir um relatório que contém várias estatísticas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], incluindo erros de pacote, execute **sp_monitor**.  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [@@PACK_RECEIVED &#40;Transact-SQL&#41;](../../t-sql/functions/pack-received-transact-sql.md)   
 [@@PACK_SENT &#40;Transact-SQL&#41;](../../t-sql/functions/pack-sent-transact-sql.md)   
 [sp_monitor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-monitor-transact-sql.md)   
 [Funções estatísticas do sistema &#40;Transact-SQL&#41;](../../t-sql/functions/system-statistical-functions-transact-sql.md)  
  
  
