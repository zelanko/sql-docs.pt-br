---
title: sp_polybase_join_group | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sp_polybase_join_group
helpviewer_keywords:
- PolyBase
ms.assetid: 48066431-fed2-4a8a-85af-ac704689e183
caps.latest.revision: 12
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 65a15600d51a5fffa474dbf2824f4e9b85b57efe
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sppolybasejoingroup-transact-sql"></a>sp_polybase_join_group (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Adiciona uma instância do SQL Server como um nó de computação a um grupo de PolyBase para a computação de expansão.  
  
 A instância do SQL Server deve ter o [PolyBase](../../relational-databases/polybase/polybase-guide.md) recurso instalado.  O PolyBase permite a integração de fontes de dados do SQL Server, como o armazenamento de blob de Hadoop e o Azure. Consulte também [sp_polybase_leave_group &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/polybase-stored-procedures-sp-polybase-leave-group.md).  
  
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
 O nome da máquina que hospeda o nó principal do SQL Server do grupo de escala horizontal do PolyBase. *@head_node_address* é nvarchar (255).  
  
 *@dms_control_channel_port* = dms_control_channel_port  
 A porta em que o canal de controle para o nó principal do serviço de movimentação de dados de PolyBase está em execução. *@dms_control_channel_port* é um Int16 não assinados. O padrão é **16450**.  
  
 *@head_node_sql_server_instance_name* = head_node_sql_server_instance_name  
 O nome da instância do SQL Server do nó principal no grupo de escala horizontal do PolyBase. *@head_node_sql_server_instance_name* é nvarchar(16).  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão CONTROL SERVER.  
  
## <a name="remarks"></a>Remarks  
 Depois de executar o procedimento armazenado, desligue o mecanismo de PolyBase e reinicie o serviço de movimentação de dados de PolyBase na máquina. Para verificar a executar a seguinte DMV no nó principal: **sys.DM exec_compute_nodes**.  
  
## <a name="example"></a>Exemplo  
 O exemplo se une a máquina atual como um nó de computação a um grupo de PolyBase.  O nome do nó principal é **HST01** e o nome da instância do SQL Server no nó principal é **MSSQLSERVER**.  
  
```  
EXEC sp_polybase_join_group N'HST01', 16450, N'MSSQLSERVER'   
```  
  
## <a name="see-also"></a>Consulte também  
 [Introdução ao PolyBase](../../relational-databases/polybase/get-started-with-polybase.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
