---
description: CURRENT_TIMEZONE (Transact-SQL)
title: CURRENT_TIMEZONE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/28/2020
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
ms.openlocfilehash: 647ba1436995028580b6c1ed7ed40a8cd7849ab5
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/14/2020
ms.locfileid: "92036839"
---
# <a name="current_timezone-transact-sql"></a>CURRENT_TIMEZONE (Transact-SQL)

[!INCLUDE[Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/asdb-asdbmi.md)]

Essa função retorna o nome do fuso horário observado por um servidor ou uma instância. Para a Instância Gerenciada de SQL, o valor retornado se baseia no fuso horário da própria instância atribuído durante a criação dela, não no fuso horário do sistema operacional subjacente.
  
> [!NOTE]  
> Para o Banco de Dados SQL, o fuso horário é sempre definido como UTC e `CURRENT_TIMEZONE` retorna o nome do fuso horário UTC.
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
CURRENT_TIMEZONE ( )  
```
  
## <a name="arguments"></a>Argumentos

Essa função não utiliza argumentos.
  
## <a name="return-type"></a>Tipo de retorno  

**varchar**
  
## <a name="remarks"></a>Comentários  

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

[Fuso horário da Instância Gerenciada de SQL](/azure/sql-database/sql-database-managed-instance-timezone)

[CURRENT_TIMEZONE_ID()](./current-timezone-id-transact-sql.md)