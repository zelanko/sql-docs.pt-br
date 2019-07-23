---
title: CURRENT_TIMEZONE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/09/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CURRENT_TIMEZONE
- CURRENT_TIMEZONE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- current time zone [SQL Server]
- current timezone [SQL Server]
- system time zone [SQL Server]
- system timezone [SQL Server]
- functions [SQL Server], time zone
- functions [SQL Server], timezone
- timezone [SQL Server], functions
- time zone [SQL Server], functions
- CURRENT_TIMEZONE function [SQL Server]
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 6c29cfba3f47506cb88860763d6650cfb3ecab7f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68026392"
---
# <a name="currenttimezone-transact-sql"></a>CURRENT_TIMEZONE (Transact-SQL)

[!INCLUDE[tsql-appliesto-ssver15-asdb-xxxx-xxx](../../includes/tsql-appliesto-ssver15-asdb-xxxx-xxx.md)]

Essa função retorna o nome do fuso horário observado por um servidor ou uma instância. Para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]`CURRENT_TIMEZONE` é derivado o valor retornado do sistema operacional do computador em que a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é executada. Para a Instância Gerenciada do Banco de Dados SQL, o valor retornado se baseia no fuso horário da própria instância, atribuído durante sua criação e não no fuso horário do sistema operacional subjacente.
  
> [!NOTE]  
> Para os Banco de Dados SQL únicos e em pool, o fuso horário é sempre definido como UTC e `CURRENT_TIMEZONE` retorna o nome do fuso horário UTC.
  
## <a name="syntax"></a>Sintaxe  
  
```sql
CURRENT_TIMEZONE ( )  
```
  
## <a name="arguments"></a>Argumentos

Essa função não utiliza argumentos.
  
## <a name="return-type"></a>Tipo de retorno  

**varchar**
  
## <a name="remarks"></a>Remarks  

`CURRENT_TIMEZONE` é uma função não determinística. Exibições e expressões que fazem referência a esta coluna não podem ser indexadas.
  
## <a name="example"></a>Exemplo

Observe que o valor retornado refletirá o fuso horário real e as configurações de idioma do servidor ou da instância.

```sql
SELECT CURRENT_TIMEZONE();  
/* Returned:  
(UTC+01:00) Amsterdam, Berlin, Bern, Rome, Stockholm, Vienna 
*/
```  
  
## <a name="see-also"></a>Confira também

[Fuso Horário da Instância Gerenciada do Banco de Dados SQL](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-timezone)
