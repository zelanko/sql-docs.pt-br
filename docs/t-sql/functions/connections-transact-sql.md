---
title: '@@CONNECTIONS (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 09/18/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1e6bad19f98ce0775c45c2f12f851bac05ea0813
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47844704"
---
# <a name="x40x40connections-transact-sql"></a>&#x40;&#x40;CONNECTIONS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Essa função retorna o número de tentativas de conexão, bem-sucedidas ou não, desde a última inicialização do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
@@CONNECTIONS  
```  
  
## <a name="return-types"></a>Tipos de retorno
**inteiro**
  
## <a name="remarks"></a>Remarks  
Conexões são diferentes de usuários. Por exemplo, um aplicativo pode abrir várias conexões em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sem que o usuário perceba.
  
Execute **sp_monitor** para exibir um relatório que contém várias estatísticas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], incluindo tentativas de contagem de conexão.
  
@@MAX_CONNECTIONS é o número máximo permitido de conexões simultâneas com o servidor. @@CONNECTIONS é incrementado a cada tentativa de logon e, portanto, @@CONNECTIONS pode exceder @@MAX_CONNECTIONS.
  
## <a name="examples"></a>Exemplos  
Este exemplo retorna a contagem de tentativas de logon a partir de data e da hora atuais.
  
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
  
## <a name="see-also"></a>Confira também
[Funções estatísticas do sistema &#40;Transact-SQL&#41;](../../t-sql/functions/system-statistical-functions-transact-sql.md)  
[sp_monitor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-monitor-transact-sql.md)
  
  
