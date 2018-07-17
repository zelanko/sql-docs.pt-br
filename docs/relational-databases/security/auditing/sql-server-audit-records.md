---
title: Registros de auditoria do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: security
ms.reviewer: ''
ms.suite: sql
ms.technology: security
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- audit records [SQL Server]
ms.assetid: 7a291015-df15-44fe-8d53-c6d90a157118
caps.latest.revision: 19
author: CarlRabeler
ms.author: carlraba
manager: craigg
ms.openlocfilehash: a2461c6da5edd6bb8cd9af720c7600eac2562366
ms.sourcegitcommit: 00ffbc085c5a4b792646ec8657495c83e6b851b5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2018
ms.locfileid: "36941872"
---
# <a name="sql-server-audit-records"></a>SQL Server Audit Records
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  O recurso Auditoria do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] permite examinar grupos de eventos e eventos individuais no nível do servidor e no nível do banco de dados. Para obter mais informações, veja [Auditoria do SQL Server &#40;Mecanismo de Banco de Dados&#41;](../../../relational-databases/security/auditing/sql-server-audit-database-engine.md). [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 Auditorias consistem em zero ou mais itens de ação de auditoria registrados em um *destino*de auditoria. O destino de auditoria pode ser um arquivo binário, o log de eventos de Aplicativo do Windows ou o log de eventos de Segurança do Windows. Os registros enviados ao destino podem conter os elementos descritos na tabela a seguir:  
  
|Nome da coluna|Descrição|Tipo|Sempre disponível|  
|-----------------|-----------------|----------|----------------------|  
|**event_time**|Data/hora em que a ação auditável é acionada.|**datetime2**|Sim|  
|**sequence_no**|Rastreia a sequência de registros dentro de um único registro de auditoria que é muito grande para se ajustar no buffer de gravação das auditorias.|**int**|Sim|  
|**action_id**|ID da ação<br /><br /> Dica: para usar **action_id** como um predicado, ele deve ser convertido de uma cadeia de caracteres para um valor numérico. Para obter mais informações, veja [Filter SQL Server Audit on action_id / class_type predicate](http://blogs.msdn.com/b/sqlsecurity/archive/2012/10/03/filter-sql-server-audit-on-action-id-class-type-predicate.aspx)(Filtrar a Auditoria do SQL Server no predicado action_id / class_type).|**varchar(4)**|Sim|  
|**succeeded**|Indica se a verificação de permissão da ação que aciona o evento de auditoria teve êxito ou falhou. |**bit**<br /> – 1 = Êxito, <br />0 = Falha|Sim|  
|**permission_bitmask**|Quando aplicável, mostra as permissões concedidas, negadas ou revogadas|**bigint**|não|  
|**is_column_permission**|Sinalizador que indica uma permissão no nível da coluna|**bit** <br />– 1 = True, <br />0 = False|não|  
|**session_id**|Identificação da sessão em que ocorreu o evento.|**int**|Sim|  
|**server_principal_id**|ID do contexto de logon em que a ação é executada.|**int**|Sim|  
|**database_principal_id**|ID do contexto do usuário de banco de dados no qual a ação é executada.|**int**|não|  
|**object_id**|ID primária da entidade na qual a auditoria ocorreu. Essa ID pode ser:<br /><br /> objetos do servidor<br /><br /> bancos de dados<br /><br /> objetos de banco de dados<br /><br /> objetos de esquema|**int**|não|  
|**target_server_principal_id**|Entidade de servidor a qual se aplica a ação auditável.|**int**|Sim|  
|**target_database_principal_id**|Entidade de banco de dados a qual se aplica a ação auditável.|**int**|não|  
|**class_type**|Tipo de entidade auditável no qual ocorre a auditoria.|**varchar(2)**|Sim|  
|**session_server_principal_name**|Entidade do servidor da sessão.|**sysname**|Sim|  
|**server_principal_name**|Logon atual.|**sysname**|Sim|  
|**server_principal_sid**|SID do logon atual.|**varbinary**|Sim|  
|**database_principal_name**|Usuário atual.|**sysname**|não|  
|**target_server_principal_name**|Logon de destino da ação.|**sysname**|não|  
|**target_server_principal_sid**|SID do logon de destino.|**varbinary**|não|  
|**target_database_principal_name**|Usuário de destino da ação.|**sysname**|não|  
|**server_instance_name**|Nome da instância de servidor no qual a auditoria ocorreu. Usa o formato máquina\instância padrão.|**nvarchar(120)**|Sim|  
|**database_name**|O contexto do banco de dados no qual a ação aconteceu.|**sysname**|não|  
|**schema_name**|O contexto do esquema no qual a ação aconteceu.|**sysname**|não|  
|**object_name**|O nome da entidade na qual a auditoria ocorreu. Esse nome pode ser:<br /><br /> objetos do servidor<br /><br /> bancos de dados<br /><br /> objetos de banco de dados<br /><br /> objetos de esquema<br /><br /> instrução TSQL (se houver)|**sysname**|não|  
|**instrução**|instrução TSQL (se houver)|**nvarchar(4000)**|não|  
|**additional_information**|Qualquer informação adicional sobre o evento, armazenado em XML.|**nvarchar(4000)**|não|  
  
## <a name="remarks"></a>Remarks  
 Algumas ações não populam o valor de uma coluna porque pode não ser aplicável à ação.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] armazena 4000 caracteres de dados para campos de caractere em um registro de auditoria. Quando os valores **additional_information** e **statement** obtidos de uma ação auditável retornam mais de 4000 caracteres, a coluna **sequence_no** é usada para gravar vários registros no relatório de auditoria para uma única ação de auditoria gravar esses dados. O processo é o seguinte:  
  
-   A coluna **statement** é dividida em 4000 caracteres.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] grava a primeira linha do registro de auditoria com os dados parciais. Todos os outros campos são duplicados em cada linha.  
  
-   O valor **sequence_no** é incrementado.  
  
-   Este processo é repetido até que todos os dados sejam registrados.  
  
 É possível conectar os dados lendo as linhas na sequência usando o valor **sequence_no** e as colunas **event_Time**, **action_id** e **session_id** para identificar a ação.  
  
## <a name="related-content"></a>Conteúdo relacionado  
 [CREATE SERVER AUDIT &#40;Transact-SQL&#41;](../../../t-sql/statements/create-server-audit-transact-sql.md)  
  
 [ALTER SERVER AUDIT &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-server-audit-transact-sql.md)  
  
 [DROP SERVER AUDIT &#40;Transact-SQL&#41;](../../../t-sql/statements/drop-server-audit-transact-sql.md)  
  
 [CREATE SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../../t-sql/statements/create-server-audit-specification-transact-sql.md)  
  
 [ALTER SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-server-audit-specification-transact-sql.md)  
  
 [DROP SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../../t-sql/statements/drop-server-audit-specification-transact-sql.md)  
  
 [CREATE DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../../t-sql/statements/create-database-audit-specification-transact-sql.md)  
  
 [ALTER DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-database-audit-specification-transact-sql.md)  
  
 [DROP DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../../t-sql/statements/drop-database-audit-specification-transact-sql.md)  
  
 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-authorization-transact-sql.md)  
  
 [sys.fn_get_audit_file &#40;Transact-SQL&#41;](../../../relational-databases/system-functions/sys-fn-get-audit-file-transact-sql.md)  
  
 [sys.server_audits &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-server-audits-transact-sql.md)  
  
 [sys.server_file_audits &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-server-file-audits-transact-sql.md)  
  
 [sys.server_audit_specifications &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-server-audit-specifications-transact-sql.md)  
  
 [sys.server_audit_specification_details &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-server-audit-specification-details-transact-sql.md)  
  
 [sys.database_audit_specifications &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-database-audit-specifications-transact-sql.md)  
  
 [sys.database_audit_specification_details &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-database-audit-specification-details-transact-sql.md)  
  
 [sys.dm_server_audit_status &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-server-audit-status-transact-sql.md)  
  
 [sys.dm_audit_actions &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-audit-actions-transact-sql.md)  
  
 [sys.dm_audit_class_type_map &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-audit-class-type-map-transact-sql.md)  
  
  
