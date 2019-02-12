---
title: DM operation_status (banco de dados SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/05/2017
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- dm_operation_status_TSQL
- dm_operation_status
- sys.dm_operation_status
- sys.dm_operation_status_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dm_operation_status dynamic management view
- sys.dm_operation_status dynamic management view
ms.assetid: cc847784-7f61-4c69-8b78-5f971bb24d61
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 604718c747819517bd323b73f276eb1fcc2a220f
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56024987"
---
# <a name="sysdmoperationstatus-azure-sql-database"></a>sys.dm_operation_status (Banco de Dados SQL do Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]

  Retorna informações sobre as operações executadas em bancos de dados em um servidor do [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
|Nome da coluna|Tipo de Dados|Descrição|  
|-----------------|---------------|-----------------|  
|session_activity_id|**uniqueidentifier**|Identificador da operação. Não nulo.|  
|resource_type|**int**|Indica o tipo de recurso no qual a operação é executada. Não nulo. Na versão atual, essa exibição controla as operações executadas no [!INCLUDE[ssSDS](../../includes/sssds-md.md)] somente, e o valor inteiro correspondente é 0.|  
|resource_type_desc|**nvarchar(2048)**|Descrição do tipo de recurso no qual a operação é executada. Na versão atual, essa exibição controla as operações executadas somente no [!INCLUDE[ssSDS](../../includes/sssds-md.md)].|  
|major_resource_id|**sql_variant**|Nome do [!INCLUDE[ssSDS](../../includes/sssds-md.md)] no qual a operação é realizada. Não nulo.|  
|minor_resource_id|**sql_variant**|Somente para uso interno. Não nulo.|  
|operação|**nvarchar(60)**|Operação executada em um [!INCLUDE[ssSDS](../../includes/sssds-md.md)], tal como CREATE ou ALTER.|  
|state|**tinyint**|O estado da operação.<br /><br /> 0 = Pendente<br />1 = em andamento<br />2 = Concluído<br />3 = Falha<br />4 = Cancelado|  
|state_desc|**nvarchar(120)**|PENDING = a operação está esperando a disponibilidade do recurso ou da cota.<br /><br /> IN_PROGRESS = a operação foi iniciada e está em andamento.<br /><br /> COMPLETED = a operação foi concluída com êxito.<br /><br /> FAILED = falha na operação. Consulte a **error_desc** coluna para obter detalhes.<br /><br /> CANCELLED = operação interrompida na solicitação do usuário.|  
|percent_complete|**int**|O percentual da operação que foi concluído. Valores não são contínuos e os valores válidos estão listados abaixo. Não nulo.<br/><br/>0 = a operação não foi iniciada<br/>50 = operação em andamento<br/>100 = operação concluída|  
|error_code|**int**|Código indicando o erro que ocorreu durante uma operação com falha. Se o valor for 0, indica que a operação foi concluída com êxito.|  
|error_desc|**nvarchar(2048)**|Descrição do erro que ocorreu durante uma operação com falha.|  
|error_severity|**int**|Nível de severidade do erro que ocorreu durante uma operação com falha. Para obter mais informações sobre severidades de erro, consulte [severidade de erro de mecanismo de banco de dados](https://go.microsoft.com/fwlink/?LinkId=251052).|  
|error_state|**int**|Reservado para uso futuro. A compatibilidade futura não está garantida.|  
|start_time|**datetime**|O carimbo de data/hora do início da operação.|  
|last_modify_time|**datetime**|Carimbo de data/hora quando o registro foi modificado pela última vez para uma operação demorada. No caso de operações concluídas bem-sucedidas, este campo exibe o carimbo de data/hora quando a operação foi concluída.|  
  
## <a name="permissions"></a>Permissões  
 Essa exibição só está disponível na **mestre** banco de dados para o logon principal no nível do servidor.  
  
## <a name="remarks"></a>Comentários  
 Para usar este modo de exibição, você deve estar conectado para o **mestre** banco de dados. Use o `sys.dm_operation_status` exibir na **mestre** banco de dados do [!INCLUDE[ssSDS](../../includes/sssds-md.md)] servidor para acompanhar o status das seguintes operações executadas em um [!INCLUDE[ssSDS](../../includes/sssds-md.md)]:  
  
-   Criar banco de dados  
  
-   Copiar banco de dados. Copiar Banco de Dados cria um registro nessa exibição nos servidores de origem e de destino.  
  
-   Alterar banco de dados  
  
-   Altere o nível de desempenho de uma camada de serviço  
  
-   Altere a camada de serviço de um banco de dados, como alterar de Basic para Standard.  
  
-   Configurando um relacionamento de Replicação Geográfica  
  
-   Finalizando um relacionamento de Replicação Geográfica  
  
-   Restaurar Banco de Dados  
  
-   Excluir banco de dados  
  
## <a name="example"></a>Exemplo  
 Mostra as operações de replicação geográfica mais recentes associadas com o banco de dados 'mydb'.  
  
```  
SELECT * FROM sys.dm_ operation_status   
   WHERE major_resource_id = 'myddb'   
   ORDER BY start_time DESC;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Funções e exibições de gerenciamento dinâmico de replicação geográfica &#40;banco de dados SQL do Azure&#41;](../../relational-databases/system-dynamic-management-views/geo-replication-dynamic-management-views-and-functions-azure-sql-database.md)   
 [DM geo_replication_link_status &#40;banco de dados SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-geo-replication-link-status-azure-sql-database.md)   
 [sys. geo_replication_links &#40;banco de dados SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-geo-replication-links-azure-sql-database.md)   
 [ALTER DATABASE &#40;Banco de Dados SQL do Azure&#41;](../../t-sql/statements/alter-database-azure-sql-database.md)  
  
  
