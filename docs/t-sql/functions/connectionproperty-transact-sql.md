---
title: CONNECTIONPROPERTY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- CONNECTIONPROPERTY_TSQL
- CONNECTIONPROPERTY
dev_langs:
- TSQL
helpviewer_keywords:
- CONNECTIONPROPERTY statement
ms.assetid: 6bd9ccae-af77-4a05-b97f-f8ab41cfde42
caps.latest.revision: 25
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 95c95ad472c5b5d4cb5420fa3b0da8f88053c0c5
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="connectionproperty-transact-sql"></a>CONNECTIONPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Retorna informações sobre as propriedades da conexão exclusiva por meio da qual uma solicitação chegou.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
CONNECTIONPROPERTY ( property )  
```  
  
## <a name="arguments"></a>Argumentos  
*property*  
É a propriedade da conexão. *property* pode ser um dos valores a seguir.
  
|Valor|Tipo de dados|Description|  
|---|---|---|
|net_transport|**nvarchar(40)**|Retorna o protocolo de transporte físico usado por essa conexão. Não permite valor nulo.<br /><br /> Os valores retornados são: **HTTP**, **Named pipe**, **Session**, **Shared memory**, **SSL**, **TCP** e **VIA**.<br /><br /> Observação: sempre retorna **Session** quando uma conexão tem o MARS (conjunto de resultados ativos múltiplos) habilitado e o pooling de conexões está habilitado.|  
|protocol_type|**nvarchar(40)**|Retorna o tipo de protocolo da carga. Atualmente faz distinção entre TDS (TSQL) e SOAP. Permite valor nulo.|  
|auth_scheme|**nvarchar(40)**|Retorna o esquema de Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de uma conexão. O esquema de autenticação é a Autenticação do Windows (NTLM, KERBEROS, DIGEST, BASIC, NEGOTIATE) ou a autenticação [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Não permite valor nulo.|  
|local_net_address|**varchar(48)**|Retorna o endereço IP no servidor a que se destina esta conexão. Disponível apenas para conexões que usam o provedor de transporte TCP. Permite valor nulo.|  
|local_tcp_port|**int**|Retornará a porta TCP de servidor destinada a esta conexão se houver uma conexão que use o transporte TCP. Permite valor nulo.|  
|client_net_address|**varchar(48)**|Solicita o endereço do cliente que está efetuando conexão neste servidor. Permite valor nulo.|  
|physical_net_transport|**nvarchar(40)**|Retorna o protocolo de transporte físico usado por essa conexão. Preciso quando uma conexão tem vários conjuntos de resultados ativos (MARS) habilitados.|  
|\<Qualquer outra cadeia de caracteres>||Retornará NULL se a entrada não for válida.|  
  
## <a name="remarks"></a>Remarks  
**local_net_address** e **local_tcp_port** retornam NULL no [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].
  
Os valores retornados são os mesmos das opções mostradas para as colunas correspondentes na exibição de gerenciamento dinâmico [sys.dm_exec_connections](../../relational-databases/system-dynamic-management-views/sys-dm-exec-connections-transact-sql.md). Por exemplo:
  
```sql
SELECT   
ConnectionProperty('net_transport') AS 'Net transport',   
ConnectionProperty('protocol_type') AS 'Protocol type';  
```  
  
## <a name="see-also"></a>Confira também
[sys.dm_exec_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)  
[sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)
  
  
