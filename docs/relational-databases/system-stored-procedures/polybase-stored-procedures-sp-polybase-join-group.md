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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: aa3b52dbc2f08e9cb504263afeb672956e4972d2
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82826359"
---
# <a name="sp_polybase_join_group-transact-sql"></a>sp_polybase_join_group (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Adiciona uma instância de SQL Server como um nó de computação a um grupo de polybase para cálculo de expansão.  
  
 A instância de SQL Server deve ter o recurso [polybase](../../relational-databases/polybase/polybase-guide.md) instalado.  O polybase permite a integração de fontes de dados não SQL Server, como o Hadoop e o armazenamento de BLOBs do Azure. Consulte também [sp_polybase_leave_group &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/polybase-stored-procedures-sp-polybase-leave-group.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
sp_polybase_join_group (@head_node_address = N'head_node_address',  
    @dms_control_channel_port = dms_control_channel_port,  
    @head_node_sql_server_instance_name = head_node_sql_server_instance_name)  
[ ; ]          
```  
  
## <a name="arguments"></a>Argumentos  
 * \@ head_node_address* = N '*head_node_address*'  
 O nome do computador que hospeda o nó de cabeçalho de SQL Server do grupo de escala horizontal do polybase. * \@ head_node_address* é nvarchar (255).  
  
 * \@ dms_control_channel_port* = dms_control_channel_port  
 A porta em que o canal de controle para o nó de cabeçalho Movimentação de Dados PolyBase serviço está em execução. * \@ dms_control_channel_port* é uma __int16 não assinada. O padrão é **16450**.  
  
 * \@ head_node_sql_server_instance_name* = head_node_sql_server_instance_name  
 O nome do nó de cabeçalho SQL Server instância no grupo de escala horizontal do polybase. * \@ head_node_sql_server_instance_name* é nvarchar (16).  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão CONTROL SERVER.  
  
## <a name="remarks"></a>Comentários  
 Depois de executar o procedimento armazenado, desligue o mecanismo do polybase e reinicie o serviço de Movimentação de Dados PolyBase no computador. Para verificar, execute o seguinte DMV no nó principal: **Sys. dm_exec_compute_nodes**.  
  
## <a name="example"></a>Exemplo  
 O exemplo une o computador atual como um nó de computação a um grupo do polybase.  O nome do nó de cabeçalho é **HST01** e o nome da instância de SQL Server no nó de cabeçalho é **MSSQLSERVER**.  
  
```  
EXEC sp_polybase_join_group N'HST01', 16450, N'MSSQLSERVER'   
```  
  
## <a name="see-also"></a>Consulte Também  
 [Introdução ao polybase](../../relational-databases/polybase/get-started-with-polybase.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
