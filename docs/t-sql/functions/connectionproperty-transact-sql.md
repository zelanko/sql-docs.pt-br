---
title: CONNECTIONPROPERTY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
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
ms.openlocfilehash: 51685541435f4ab0192792341d2a29210dc9f504
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33054783"
---
# <a name="connectionproperty-transact-sql"></a>CONNECTIONPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Para uma solicitação chega ao servidor, essa função retorna informações sobre as propriedades de conexão da conexão exclusiva que dá suporte a essa solicitação.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
CONNECTIONPROPERTY ( property )  
```  
  
## <a name="arguments"></a>Argumentos  
*property*  
A propriedade da conexão. *property* pode ser um destes valores:
  
|Valor|Tipo de dados|Description|  
|---|---|---|
|net_transport|**nvarchar(40)**|Retorna o protocolo de transporte físico usado por essa conexão. Esse valor não é anulável. Os valores de retorno possíveis:<br /><br /> **HTTP**<br /> **Pipe nomeado**<br /> **Session**<br /> **Memória compartilhada**<br /> **SSL**<br /> **TCP**<br /><br /> e<br /><br /> **VIA**<br /><br /> Observação: sempre retorna **Session** quando uma conexão tem o MARS (conjunto de resultados ativos múltiplos) habilitado e o pooling de conexões está habilitado.|  
|protocol_type|**nvarchar(40)**|Retorna o tipo de protocolo da carga. Atualmente faz distinção entre TDS (TSQL) e SOAP. Permite valor nulo.|  
|auth_scheme|**nvarchar(40)**|Retorna o esquema de autenticação [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da conexão. O esquema de autenticação é a Autenticação do Windows (NTLM, KERBEROS, DIGEST, BASIC, NEGOTIATE) ou a autenticação [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Não permite valor nulo.|  
|local_net_address|**varchar(48)**|Retorna o endereço IP no servidor a que se destina esta conexão específica. Disponível apenas para conexões que usam o provedor de transporte TCP. Permite valor nulo.|  
|local_tcp_port|**int**|Retornará a porta TCP de servidor destinada a esta conexão se houver uma conexão que use o transporte TCP. Permite valor nulo.|  
|client_net_address|**varchar(48)**|Solicita o endereço do cliente que tenta a conexão a este servidor. Permite valor nulo.|  
|physical_net_transport|**nvarchar(40)**|Retorna o protocolo de transporte físico usado por essa conexão. Preciso quando uma conexão tem vários conjuntos de resultados ativos (MARS) habilitados.|  
|\<Qualquer outra cadeia de caracteres>||Retorna NULL para entrada inválida.|  
  
## <a name="remarks"></a>Remarks  
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
  
  
