---
title: Registros de auditoria do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- audit records [SQL Server]
ms.assetid: 7a291015-df15-44fe-8d53-c6d90a157118
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: d3462266279ed80e94871db4831918ad70b444be
ms.sourcegitcommit: 37a3e2c022c578fc3a54ebee66d9957ff7476922
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/07/2020
ms.locfileid: "82922142"
---
# <a name="sql-server-audit-records"></a>SQL Server Audit Records
  O recurso Auditoria do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] permite examinar grupos de eventos e eventos individuais no nível do servidor e no nível do banco de dados. Para obter mais informações, veja [Auditoria do SQL Server &#40;Mecanismo de Banco de Dados&#41;](sql-server-audit-database-engine.md). [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 Auditorias consistem em zero ou mais itens de ação de auditoria registrados em um *destino*de auditoria. O destino de auditoria pode ser um arquivo binário, o log de eventos de Aplicativo do Windows ou o log de eventos de Segurança do Windows. Os registros enviados ao destino podem conter os elementos descritos na tabela a seguir.  
  
|Nome da coluna|DESCRIÇÃO|Type|Sempre disponível|  
|-----------------|-----------------|----------|----------------------|  
|**event_time**|Data/hora em que a ação auditável é acionada.|`datetime2`|Yes|  
|**sequence_no**|Rastreia a sequência de registros dentro de um único registro de auditoria que é muito grande para se ajustar no buffer de gravação das auditorias.|`int`|Yes|  
|**action_id**|ID da ação<br /><br /> Dica: para usar **action_id** como um predicado, ele deve ser convertido de uma cadeia de caracteres para um valor numérico. Para obter mais informações, veja [Filter SQL Server Audit on action_id / class_type predicate](https://docs.microsoft.com/archive/blogs/sqlsecurity/filter-sql-server-audit-on-action_id-class_type-predicate)(Filtrar a Auditoria do SQL Server no predicado action_id / class_type).|`varchar(4)`|Yes|  
|**bem-sucedido**|Indica se a ação que acionou o evento foi realizada com êxito|`bit`-1 = êxito, 0 = falha|Yes|  
|**permission_bitmask**|Quando aplicável, mostra as permissões concedidas, negadas ou revogadas|`bigint`|No|  
|**is_column_permission**|Sinalizador que indica uma permissão no nível da coluna|`bit`-1 = true, 0 = false|No|  
|**session_id**|Identificação da sessão em que ocorreu o evento.|`int`|Yes|  
|**server_principal_id**|ID do contexto de logon em que a ação é executada.|`int`|Yes|  
|**database_principal_id**|ID do contexto do usuário de banco de dados no qual a ação é executada.|`int`|No|  
|**ID de object_**|ID primária da entidade na qual a auditoria ocorreu. Isso inclui:<br /><br /> objetos do servidor<br /><br /> bancos de dados<br /><br /> objetos de banco de dados<br /><br /> objetos de esquema|`int`|No|  
|**target_server_principal_id**|Entidade de servidor a qual se aplica a ação auditável.|`int`|Yes|  
|**target_database_principal_id**|Entidade de banco de dados a qual se aplica a ação auditável.|`int`|No|  
|**class_type**|Tipo de entidade auditável no qual ocorre a auditoria.|`varchar(2)`|Yes|  
|**session_server_principal_name**|Entidade do servidor da sessão.|`sysname`|Yes|  
|**server_principal_name**|Logon atual.|`sysname`|Yes|  
|**server_principal_sid**|SID do logon atual.|`varbinary`|Yes|  
|**database_principal_name**|Usuário atual.|`sysname`|No|  
|**target_server_principal_name**|Logon de destino da ação.|`sysname`|No|  
|**target_server_principal_sid**|SID do logon de destino.|`varbinary`|No|  
|**target_database_principal_name**|Usuário de destino da ação.|`sysname`|No|  
|**server_instance_name**|Nome da instância de servidor no qual a auditoria ocorreu. Usa o formato máquina\instância padrão.|`nvarchar(120)`|Yes|  
|**database_name**|O contexto do banco de dados no qual a ação aconteceu.|`sysname`|No|  
|**schema_name**|O contexto do esquema no qual a ação aconteceu.|`sysname`|Não|  
|**object_name**|O nome da entidade na qual a auditoria ocorreu. Isso inclui:<br /><br /> objetos do servidor<br /><br /> bancos de dados<br /><br /> objetos de banco de dados<br /><br /> objetos de esquema<br /><br /> instrução TSQL (se houver)|`sysname`|No|  
|**privacidade**|instrução TSQL (se houver)|`nvarchar(4000)`|Não|  
|**additional_information**|Qualquer informação adicional sobre o evento, armazenado em XML.|`nvarchar(4000)`|No|  
  
## <a name="remarks"></a>Comentários  
 Algumas ações não populam o valor de uma coluna porque pode não ser aplicável à ação.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] armazena 4000 caracteres de dados para campos de caractere em um registro de auditoria. Quando os valores **additional_information** e **statement** obtidos de uma ação auditável retornam mais de 4000 caracteres, a coluna **sequence_no** é usada para gravar vários registros no relatório de auditoria para uma única ação de auditoria gravar esses dados. O processo é o seguinte:  
  
-   A coluna **statement** é dividida em 4000 caracteres.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] grava a primeira linha do registro de auditoria com os dados parciais. Todos os outros campos são duplicados em cada linha.  
  
-   O valor **sequence_no** é incrementado.  
  
-   Este processo é repetido até que todos os dados sejam registrados.  
  
 É possível conectar os dados lendo as linhas na sequência usando o valor **sequence_no** e as colunas **event_Time**, **action_id** e **session_id** para identificar a ação.  
  
## <a name="related-content"></a>Conteúdo relacionado  
 [CREATE SERVER AUDIT &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-server-audit-transact-sql)  
  
 [ALTER SERVER AUDIT &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-server-audit-specification-transact-sql)  
  
 [DROP SERVER AUDIT &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-server-audit-transact-sql)  
  
 [CREATE SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-server-audit-specification-transact-sql)  
  
 [ALTER SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-server-audit-transact-sql)  
  
 [DROP SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-server-audit-specification-transact-sql)  
  
 [CREATE DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-database-audit-specification-transact-sql)  
  
 [ALTER DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-audit-specification-transact-sql)  
  
 [DROP DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-database-encryption-key-transact-sql)  
  
 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-authorization-transact-sql)  
  
 [sys.fn_get_audit_file &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/sys-fn-get-audit-file-transact-sql)  
  
 [sys.server_audits &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-audits-transact-sql)  
  
 [sys.server_file_audits &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-file-audits-transact-sql)  
  
 [sys.server_audit_specifications &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-audit-specifications-transact-sql)  
  
 [sys.server_audit_specification_details &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-audit-specification-details-transact-sql)  
  
 [sys.database_audit_specifications &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-audit-specifications-transact-sql)  
  
 [sys.database_audit_specification_details &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-audit-specification-details-transact-sql)  
  
 [sys.dm_server_audit_status &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-server-audit-status-transact-sql)  
  
 [sys.dm_audit_actions &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-audit-actions-transact-sql)  
  
 [sys.dm_audit_class_type_map &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-audit-class-type-map-transact-sql)  
  
  
