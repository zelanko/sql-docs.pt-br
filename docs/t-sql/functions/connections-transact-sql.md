---
title: '@@CONNECTIONS (Transact-SQL) | Microsoft Docs'
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
- '@@CONNECTIONS'
- '@@CONNECTIONS_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@CONNECTIONS function'
- connections [SQL Server], number of
- connections [SQL Server], attempted
- number of connection attempts
- attempted connections
ms.assetid: c59836a8-443c-4b9a-8b96-8863ada97ac7
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8422da0d4e550c99fac6c9659f771ab98196cb4a
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="x40x40connections-transact-sql"></a>&#x40;&#x40;CONEXÕES (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Retorna o número de tentativas de conexão, bem-sucedidas ou não, desde a última inicialização do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
@@CONNECTIONS  
```  
  
## <a name="return-types"></a>Tipos de retorno
**inteiro**
  
## <a name="remarks"></a>Comentários  
Conexões são diferentes de usuários. Por exemplo, aplicativos podem abrir várias conexões em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sem que o usuário perceba.
  
Para exibir um relatório que contém várias [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estatísticas, inclusive tentativas de conexão, executadas **sp_monitor**.
  
@@MAX_CONNECTIONS é o número máximo de conexões permitidas simultaneamente no servidor. @@CONNECTIONS é incrementado com cada tentativa de logon, portanto @@CONNECTIONS pode ser maior que @@MAX_CONNECTIONS .
  
## <a name="examples"></a>Exemplos  
O exemplo a seguir mostra o retorno do número de tentativas de logon a partir da data e hora atuais.
  
```sql
SELECT GETDATE() AS 'Today''s Date and Time',   
@@CONNECTIONS AS 'Login Attempts';  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
  
Today's Date and Time  Login Attempts  
---------------------- --------------  
12/5/2006 10:32:45 AM  211023         
```  
  
## <a name="see-also"></a>Consulte também
[Funções estatísticas do sistema &#40;Transact-SQL&#4#41;](../../t-sql/functions/system-statistical-functions-transact-sql.md)  
[sp_monitor &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-monitor-transact-sql.md)
  
  
