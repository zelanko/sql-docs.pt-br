---
title: DROP AVAILABILITY GROUP (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 613841598b153dbe502f0267ed85197973bf706a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67898301"
---
# <a name="drop-availability-group-transact-sql"></a>DROP AVAILABILITY GROUP (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Remove o grupo de disponibilidade especificado e todas as suas réplicas. Se uma instância de servidor que hospeda uma das réplicas de disponibilidade estiver offline quando você exclui um grupo de disponibilidade, ela removerá a réplica de disponibilidade local quando estiver online novamente. O cancelamento de um grupo de disponibilidade também exclui o ouvinte de grupo de disponibilidade associado, se houver.  
  
> [!IMPORTANT]  
>  Se possível, remova o grupo de disponibilidade somente quando ele estiver conectado à instância do servidor que hospeda a réplica primária. Quando o grupo de disponibilidade é removido da réplica primária, são permitidas alterações nos bancos de dados primários antigos (sem proteção de alta disponibilidade). Quando um grupo de disponibilidade é excluído de uma réplica secundária, a réplica primária fica no estado **RESTORING**, e as alterações não são permitidas nos bancos de dados.  
  
 Para obter informações sobre maneiras alternativas de remover um grupo de disponibilidade, consulte [Remover um grupo de disponibilidade &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/remove-an-availability-group-sql-server.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DROP AVAILABILITY GROUP group_name   
[ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *group_name*  
 Especifica o nome do grupo de disponibilidade a ser cancelado.  
  
## <a name="limitations-and-recommendations"></a>Limitações e recomendações  
  
-   A execução de **DROP AVAILABILITY GROUP** exige que o recurso de Grupos de Disponibilidade AlwaysOn seja habilitado na instância de servidor. Para obter mais informações, veja [Habilitar e desabilitar Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md).  
  
-   **DROP AVAILABILITY GROUP** não pode ser executado como parte de lotes ou dentro de transações. Além disso, expressões e variáveis não têm suporte.  
  
-   Você pode remover um grupo de disponibilidade de qualquer nó WSFC (Windows Server Failover Clustering) que processa as credenciais de segurança corretas para o grupo de disponibilidade. Isso permite excluir um grupo de disponibilidade quando nenhuma de suas réplicas de disponibilidade permanece.  
  
    > [!IMPORTANT]  
    >  Evite remover um grupo de disponibilidade quando o cluster WSFC (Windows Server Failover Clustering) não tem quorum. Caso seja necessário remover um grupo de disponibilidade enquanto o cluster perde quorum, o grupo de disponibilidade de metadados armazenado no cluster não será removido. Depois que o cluster recuperar o quorum, será necessário remover novamente o grupo de disponibilidade para removê-lo do cluster WSFC.  
  
-   Em uma réplica secundária, **DROP AVAILABILITY GROUP** apenas deve ser usado para fins de emergência. Isso ocorre porque, ao remover um grupo de disponibilidade, você o coloca offline. Se você remover o grupo de disponibilidade de uma réplica secundária, a réplica primária não poderá determinar se o estado **OFFLINE** ocorreu devido à perda de quorum, a um failover forçado ou a um comando **DROP AVAILABILITY GROUP**. A réplica primária passa para o estado **RESTORING** para evitar uma possível situação de separação. Para obter mais informações, confira [Como funciona: Como funcionam os comportamentos de DROP AVAILABILITY GROUP](https://blogs.msdn.com/b/psssql/archive/2012/06/13/how-it-works-drop-availability-group-behaviors.aspx) (blog CSS SQL Server Engineers).  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
 Exige a permissão **ALTER AVAILABILITY GROUP** no grupo de disponibilidade, a permissão **CONTROL AVAILABILITY GROUP**, a permissão **ALTER ANY AVAILABILITY GROUP** ou a permissão **CONTROL SERVER**. Para remover um grupo de disponibilidade que não é hospedado pela instância de servidor local, você precisará da permissão **CONTROL SERVER** ou **CONTROL** nesse grupo de disponibilidade.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cancela o grupo de disponibilidade `AccountsAG`.  
  
```  
DROP AVAILABILITY GROUP AccountsAG;  
```  
  
##  <a name="RelatedContent"></a> Conteúdo relacionado  
  
-   [Como funciona: Como funcionam os comportamentos de DROP AVAILABILITY GROUP](https://blogs.msdn.com/b/psssql/archive/2012/06/13/how-it-works-drop-availability-group-behaviors.aspx) (blog CSS SQL Server Engineers)  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-availability-group-transact-sql.md)   
 [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-availability-group-transact-sql.md)   
 [Remover um grupo de disponibilidade &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/remove-an-availability-group-sql-server.md)  
  
  
