---
title: sys. change_tracking_databases (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/08/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- change_tracking_databases
- sys.change_tracking_databases_TSQL
- sys.change_tracking_databases
- change_tracking_databases_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.change_tracking_databases
- change tracking [SQL Server], sys.change_tracking_databases
ms.assetid: bb233baa-2991-4904-a0eb-3772b81121a4
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 9d3f2f92e9be7b6d4f38edff7cb36aa67e055788
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68136536"
---
# <a name="change-tracking-catalog-views---syschange_tracking_databases"></a>Controle de Alterações exibições do catálogo-sys. change_tracking_databases
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  Retorna uma linha para cada banco de dados com o controle de alterações habilitado.  

|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|database_id|**int**|ID do banco de dados. Exclusivo na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|is_auto_cleanup_on|**bit**|Indica se os dados do controle de alterações devem ser limpos automaticamente após o período de retenção configurado:<br /><br /> 0 = Desativado<br /><br /> 1 = Ativado|  
|retention_period|**int**|Se a limpeza automática estiver sendo usada, o período de retenção especificará por quanto tempo os dados de controle de alterações serão mantidos no banco de dados.|  
|retention_period_units_desc|**nvarchar(60)**|Especifica a descrição do período de retenção:<br /><br /> minutos<br /><br /> Horas<br /><br /> Days (dias)|  
|retention_period_units|**tinyint**|Unidade de tempo do período de retenção:<br /><br /> 1 = Minutos<br /><br /> 2 = Horas<br /><br /> 3 = Dias|  
  
## <a name="permissions"></a>Permissões  
 As mesmas verificações de permissão são feitas para sys.change_tracking_databases e para sys.databases. Se o chamador sys.change_tracking_databases não for o proprietário do banco de dados, as permissões mínimas necessárias para verificar a linha correspondente serão ALTER ANY DATABASE ou VIEW ANY DATABASE em nível de servidor ou CREATE DATABASE no banco de dados mestre ou atual.  
  
## <a name="see-also"></a>Consulte Também  
 [Controle de Alterações exibições de catálogo &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/6e8fd949-5560-4b34-879f-4e25aa24b183)   
 [Controle de alterações de dados &#40;SQL Server&#41;](../../relational-databases/track-changes/track-data-changes-sql-server.md)  
  
  
