---
title: DESCARTE o grupo de disponibilidade (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP_AVAILABILITY_GROUP_TSQL
- DROP AVAILABILITY GROUP
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], removing
- Availability Groups [SQL Server], Transact-SQL statements
- DROP AVAILABILITY GROUP statement
- Availability Groups [SQL Server], dropping
ms.assetid: c1600289-c990-454a-b279-dba0ebd5d63e
caps.latest.revision: 44
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c1cd1e16d7d25810d571f940aaf1dece825406c3
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="drop-availability-group-transact-sql"></a>DROP AVAILABILITY GROUP (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Remove o grupo de disponibilidade especificado e todas as suas réplicas. Se uma instância de servidor que hospeda uma das réplicas de disponibilidade estiver offline quando você exclui um grupo de disponibilidade, ela removerá a réplica de disponibilidade local quando estiver online novamente. O cancelamento de um grupo de disponibilidade também exclui o ouvinte de grupo de disponibilidade associado, se houver.  
  
> [!IMPORTANT]  
>  Se possível, remova o grupo de disponibilidade somente quando ele estiver conectado à instância do servidor que hospeda a réplica primária. Quando o grupo de disponibilidade é removido da réplica primária, são permitidas alterações nos bancos de dados primários antigos (sem proteção de alta disponibilidade). Excluir um grupo de disponibilidade de uma réplica secundária deixa a réplica primária no **RESTORING** estado e as alterações não são permitidas nos bancos de dados.  
  
 Para obter informações sobre modos alternativos para descartar um grupo de disponibilidade, consulte [remover um grupo de disponibilidade &#40; SQL Server &#41; ](../../database-engine/availability-groups/windows/remove-an-availability-group-sql-server.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DROP AVAILABILITY GROUP group_name   
[ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *nome_do_grupo*  
 Especifica o nome do grupo de disponibilidade a ser cancelado.  
  
## <a name="limitations-and-recommendations"></a>Limitações e recomendações  
  
-   Executar **DROP AVAILABILITY GROUP** requer que o recurso de grupos de disponibilidade AlwaysOn está habilitado na instância do servidor. Para obter mais informações, veja [Habilitar e desabilitar Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md).  
  
-   **DROP AVAILABILITY GROUP** não pode ser executado como parte de lotes ou dentro de transações. Além disso, expressões e variáveis não têm suporte.  
  
-   Você pode remover um grupo de disponibilidade de qualquer nó WSFC (Windows Server Failover Clustering) que processa as credenciais de segurança corretas para o grupo de disponibilidade. Isso permite excluir um grupo de disponibilidade quando nenhuma de suas réplicas de disponibilidade permanece.  
  
    > [!IMPORTANT]  
    >  Evite remover um grupo de disponibilidade quando o cluster WSFC (Windows Server Failover Clustering) não tem quorum. Caso seja necessário remover um grupo de disponibilidade enquanto o cluster perde quorum, o grupo de disponibilidade de metadados armazenado no cluster não será removido. Depois que o cluster recuperar o quorum, será necessário remover novamente o grupo de disponibilidade para removê-lo do cluster WSFC.  
  
-   Em uma réplica secundária, **DROP AVAILABILITY GROUP** só deve ser usado apenas para fins de emergência. Isso ocorre porque, ao remover um grupo de disponibilidade, você o coloca offline. Se você remover o grupo de disponibilidade de uma réplica secundária, a réplica primária não pode determinar se o **OFFLINE** estado ocorreu devido à perda de quorum, um failover forçado, ou um **DROP AVAILABILITY GROUP**comando. A réplica primária passa para o **RESTORING** estado para evitar uma possível situação de separação. Para obter mais informações, consulte [How It Works: DROP AVAILABILITY GROUP Behaviors](http://blogs.msdn.com/b/psssql/archive/2012/06/13/how-it-works-drop-availability-group-behaviors.aspx) (Como funcionam os comportamentos de DROP AVAILABILITY GROUP) (blog CSS SQL Server Engineers).  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
 Requer **ALTER AVAILABILITY GROUP** permissão no grupo de disponibilidade, **CONTROL AVAILABILITY GROUP** permissão, **ALTER ANY AVAILABILITY GROUP** permissão, ou **CONTROL SERVER** permissão. Para remover um grupo de disponibilidade que não é hospedado pela instância do servidor local, você precisa **CONTROL SERVER** permissão ou **controle** nesse grupo de disponibilidade.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cancela o grupo de disponibilidade `AccountsAG`.  
  
```  
DROP AVAILABILITY GROUP AccountsAG;  
```  
  
##  <a name="RelatedContent"></a> Conteúdo relacionado  
  
-   [How It Works: DROP AVAILABILITY GROUP Behaviors](http://blogs.msdn.com/b/psssql/archive/2012/06/13/how-it-works-drop-availability-group-behaviors.aspx) (Como funcionam os comportamentos de DROP AVAILABILITY GROUP) (blog CSS SQL Server Engineers)  
  
## <a name="see-also"></a>Consulte também  
 [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-availability-group-transact-sql.md)   
 [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-availability-group-transact-sql.md)   
 [Remover um grupo de disponibilidade &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/remove-an-availability-group-sql-server.md)  
  
  

