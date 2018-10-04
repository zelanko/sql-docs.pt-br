---
title: sp_polybase_join_group | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- sp_polybase_join_group
helpviewer_keywords:
- PolyBase
ms.assetid: 48066431-fed2-4a8a-85af-ac704689e183
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 878afb5f16c988ee98908030695e0f03c7e2f7d5
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47722644"
---
# <a name="sppolybasejoingroup-transact-sql"></a>sp_polybase_join_group (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Adiciona uma instância do SQL Server como um nó de computação a um grupo do PolyBase para computação de escala horizontal.  
  
 A instância do SQL Server deve ter o [PolyBase](../../relational-databases/polybase/polybase-guide.md) recurso instalado.  O PolyBase permite a integração de fontes de dados não SQL Server, como o armazenamento de blob do Hadoop e do Azure. Consulte também [sp_polybase_leave_group &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/polybase-stored-procedures-sp-polybase-leave-group.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
sp_polybase_join_group (@head_node_address = N'head_node_address',  
    @dms_control_channel_port = dms_control_channel_port,  
    @head_node_sql_server_instance_name = head_node_sql_server_instance_name)  
[ ; ]          
```  
  
## <a name="arguments"></a>Argumentos  
 *@head_node_address* = N'*head_node_address*'  
 O nome do computador que hospeda o nó principal do SQL Server do grupo de escala horizontal do PolyBase. *@head_node_address* é nvarchar (255).  
  
 *@dms_control_channel_port* = dms_control_channel_port  
 A porta em que o canal de controle para o serviço de movimentação de dados de PolyBase do nó principal está em execução. *@dms_control_channel_port* é um __int16 sem sinal. O padrão é **16450**.  
  
 *@head_node_sql_server_instance_name* = head_node_sql_server_instance_name  
 O nome da instância do SQL Server do nó principal no grupo de escala horizontal do PolyBase. *@head_node_sql_server_instance_name* é nvarchar(16).  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão CONTROL SERVER.  
  
## <a name="remarks"></a>Comentários  
 Depois de executar o procedimento armazenado, encerrar o mecanismo de PolyBase e reinicie o serviço de movimentação de dados de PolyBase na máquina. Para verificar a executar a seguinte DMV no nó principal: **DM exec_compute_nodes**.  
  
## <a name="example"></a>Exemplo  
 O exemplo une o computador atual como um nó de computação para um grupo do PolyBase.  É o nome do nó principal **HST01** e o nome da instância do SQL Server no nó de cabeçalho é **MSSQLSERVER**.  
  
```  
EXEC sp_polybase_join_group N'HST01', 16450, N'MSSQLSERVER'   
```  
  
## <a name="see-also"></a>Consulte também  
 [Introdução ao PolyBase](../../relational-databases/polybase/get-started-with-polybase.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
