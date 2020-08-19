---
description: CONNECTIONPROPERTY (Transact-SQL)
title: CONNECTIONPROPERTY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CONNECTIONPROPERTY_TSQL
- CONNECTIONPROPERTY
dev_langs:
- TSQL
helpviewer_keywords:
- CONNECTIONPROPERTY statement
ms.assetid: 6bd9ccae-af77-4a05-b97f-f8ab41cfde42
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 8d630d5c0cf4b51776bbfc6c6936267f11304557
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88367032"
---
# <a name="connectionproperty-transact-sql"></a>CONNECTIONPROPERTY (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Para uma solicitação chega ao servidor, essa função retorna informações sobre as propriedades de conexão da conexão exclusiva que dá suporte a essa solicitação.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
CONNECTIONPROPERTY ( property )  
```  

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
*property*  
A propriedade da conexão. *property* pode ser um destes valores:
  
|Valor|Tipo de dados|Descrição|  
|---|---|---|
|net_transport|**nvarchar(40)**|Retorna o protocolo de transporte físico usado por essa conexão. Esse valor não é anulável. Os valores de retorno possíveis:<br /><br /> **HTTP**<br /> **Pipe nomeado**<br /> **Sessão**<br /> **Memória compartilhada**<br /> **SSL**<br /> **TCP**<br /><br /> e<br /><br /> **VIA**<br /><br /> Observação: Sempre retorna **Session** quando uma conexão tem o MARS (conjunto de resultados ativos múltiplos) habilitado e o pooling de conexões está habilitado.|  
|protocol_type|**nvarchar(40)**|Retorna o tipo de protocolo da carga. Atualmente faz distinção entre TDS (TSQL) e SOAP. Permite valor nulo.|  
|auth_scheme|**nvarchar(40)**|Retorna o esquema de autenticação [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da conexão. O esquema de autenticação é a Autenticação do Windows (NTLM, KERBEROS, DIGEST, BASIC, NEGOTIATE) ou a autenticação [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Não permite valor nulo.|  
|local_net_address|**varchar(48)**|Retorna o endereço IP no servidor a que se destina esta conexão específica. Disponível apenas para conexões que usam o provedor de transporte TCP. Permite valor nulo.|  
|local_tcp_port|**int**|Retornará a porta TCP de servidor destinada a esta conexão se houver uma conexão que use o transporte TCP. Permite valor nulo.|  
|client_net_address|**varchar(48)**|Solicita o endereço do cliente que tenta a conexão a este servidor. Permite valor nulo.|  
|physical_net_transport|**nvarchar(40)**|Retorna o protocolo de transporte físico usado por essa conexão. Preciso quando uma conexão tem vários conjuntos de resultados ativos (MARS) habilitados.|  
|\<Any other string>||Retorna NULL para entrada inválida.|  
  
## <a name="remarks"></a>Comentários  
**local_net_address** e **local_tcp_port** retornam NULL no [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].
  
Os valores retornados correspondem às opções mostradas para as colunas correspondentes na exibição de gerenciamento dinâmico [sys.dm_exec_connections](../../relational-databases/system-dynamic-management-views/sys-dm-exec-connections-transact-sql.md). Por exemplo:
  
```sql
SELECT   
ConnectionProperty('net_transport') AS 'Net transport',   
ConnectionProperty('protocol_type') AS 'Protocol type';  
```  
  
## <a name="see-also"></a>Confira também
[sys.dm_exec_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)  
[sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)
  
  
