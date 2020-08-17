---
description: sys.fn_get_audit_file (Transact-SQL)
title: sys.fn_get_audit_file (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/19/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fn_get_audit_file_TSQL
- sys.fn_get_audit_file_TSQL
- fn_get_audit_file
- sys.fn_get_audit_file
dev_langs:
- TSQL
helpviewer_keywords:
- sys.fn_get_audit_file function
- fn_get_audit_file function
ms.assetid: d6a78d14-bb1f-4987-b7b6-579ddd4167f5
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current||=azure-sqldw-latest
ms.openlocfilehash: cda66aed0e3ddea4bcb14bc30ca5805bf943afb4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88321792"
---
# <a name="sysfn_get_audit_file-transact-sql"></a>sys.fn_get_audit_file (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]    

  Retorna informações de um arquivo de auditoria criado por uma auditoria de servidor no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, veja [Auditoria do SQL Server &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
fn_get_audit_file ( file_pattern,   
    { default | initial_file_name | NULL },   
    { default | audit_record_offset | NULL } )  
```  
  
## <a name="arguments"></a>Argumentos  
 *file_pattern*  
 Especifica o diretório ou caminho e o nome de arquivo do conjunto de arquivos de auditoria que será lido. O tipo é **nvarchar (260)**. 
 
 - **SQL Server**:
    
    Esse argumento deve incluir um caminho (letra de unidade ou compartilhamento de rede) e um nome de arquivo, podendo conter um caractere curinga. Um único asterisco (*) pode ser usado para coletar vários arquivos de um conjunto de arquivos de auditoria. Por exemplo:   
  
    -   **\<path>\\\*** -Coletar todos os arquivos de auditoria no local especificado.  
  
    -   ** \<path> \ LOGINSAUDIT_ {GUID}***-coletar todos os arquivos de auditoria que têm o nome e o par GUID especificados.  
  
    -   ** \<path> \ LOGINSAUDIT_ {GUID} _00_29384. sqlaudit** -coleta um arquivo de auditoria específico.  
  
 - **Banco de dados SQL do Azure**:
 
    Esse argumento é usado para especificar uma URL de BLOB (incluindo o ponto de extremidade de armazenamento e o contêiner). Embora não ofereça suporte a um curinga de asterisco, você pode usar um prefixo de nome de arquivo parcial (BLOB) (em vez do nome de blob completo) para coletar vários arquivos (BLOBs) que começam com esse prefixo. Por exemplo: 
 
      - **\<Storage_endpoint\>/\<Container\>/\<ServerName\>/\<DatabaseName\>/** -coleta todos os arquivos de auditoria (BLOBs) para o banco de dados específico.    
      
      - ** \<Storage_endpoint\> / \<Container\> / \<ServerName\> / \<DatabaseName\> / \<AuditName\> / \<CreationDate\> / \<FileName\> . xel** -coleta um arquivo de auditoria específico (BLOB).
  
> [!NOTE]  
>  Indicar um caminho sem um padrão de nome de arquivo irá gerar um erro.  
  
 *initial_file_name*  
 Especifica o caminho e o nome de um arquivo especificado no conjunto de arquivos de auditoria a partir do qual iniciar a leitura dos registros de auditoria. O tipo é **nvarchar (260)**.  
  
> [!NOTE]  
>  O argumento *initial_file_name* deve conter entradas válidas ou deve conter o padrão | Valor nulo.  
  
 *audit_record_offset*  
 Especifica um local conhecido com o arquivo especificado para o initial_file_name. Quando esse argumento for usado, a função começará a leitura a partir do primeiro registro do buffer imediatamente após o deslocamento especificado.  
  
> [!NOTE]  
>  O argumento *audit_record_offset* deve conter entradas válidas ou deve conter o padrão | Valor nulo. O tipo é **bigint**.  
  
## <a name="tables-returned"></a>Tabelas retornadas  
 A tabela a seguir descreve o conteúdo do arquivo de auditoria que pode ser retornado por essa função.  
  
| Nome da coluna | Type | Descrição |  
|-------------|------|-------------|  
| action_id | **varchar(4)** | A identificação da ação. Não permite valor nulo. |  
| additional_information | **nvarchar(4000)** | Informações exclusivas que se aplicam somente a um evento são retornadas como XML. Um número pequeno de ações auditável contém esse tipo de informação.<br /><br /> Um nível de pilha TSQL será exibido em formato XML para ações que tenham pilha TSQL associada a elas. O formato XML será:<br /><br /> `<tsql_stack><frame nest_level = '%u' database_name = '%.*s' schema_name = '%.*s' object_name = '%.*s' /></tsql_stack>`<br /><br /> O nest_level do quadro indica o nível de aninhamento atual do quadro. O nome do Módulo é representado em formato de três partes (database_name, schema_name e object_name).  O nome do módulo será analisado para escapar caracteres XML inválidos como `'\<'` , `'>'` , `'/'` , `'_x'` . Eles serão ignorados como `_xHHHH\_` . O HHHH representa o código UCS-2 hexadecimal de quatro dígitos do caractere<br /><br /> Permite valor nulo. Retornará NULL quando o evento não reportar informações adicionais. |
| affected_rows | **bigint** | **Aplica-se a**: somente banco de dados SQL do Azure<br /><br /> Número de linhas afetadas pela instrução executada. |  
| application_name | **nvarchar(128)** | **Aplica-se a**: banco de dados SQL do Azure + SQL Server (a partir de 2017)<br /><br /> Nome do aplicativo cliente que executou a instrução que causou o evento de auditoria |  
| audit_file_offset | **bigint** | **Aplica-se a**: somente SQL Server<br /><br /> O deslocamento de buffer no arquivo que contém o registro de auditoria. Não permite valor nulo. |  
| audit_schema_version | **int** | Sempre 1 |  
| class_type | **varchar(2)** | O tipo de entidade auditável no qual a auditoria ocorre. Não permite valor nulo. |  
| client_ip | **nvarchar(128)** | **Aplica-se a**: banco de dados SQL do Azure + SQL Server (a partir de 2017)<br /><br />  IP de origem do aplicativo cliente |  
| connection_id | GUID | **Aplica-se a**: banco de dados SQL do Azure e SQL instância gerenciada<br /><br /> ID da conexão no servidor |
| data_sensitivity_information | nvarchar(4000) | **Aplica-se a**: somente banco de dados SQL do Azure<br /><br /> Tipos de informações e rótulos de sensibilidade retornados pela consulta auditada, com base nas colunas classificadas no banco de dados. Saiba mais sobre a [descoberta e a classificação de dados do banco SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-data-discovery-and-classification) |
| database_name | **sysname** | O contexto do banco de dados no qual a ação aconteceu. Permite valor nulo. Retorna NULL para auditorias que ocorrem no nível do servidor. |  
| database_principal_id | **int** |ID do contexto do usuário de banco de dados no qual a ação é executada. Não permite valor nulo. Retornará 0 se isso não se aplicar. Por exemplo, uma operação de servidor.|
| database_principal_name | **sysname** | Usuário atual. Permite valor nulo. Retorna NULL se não disponível. |  
| duration_milliseconds | **bigint** | **Aplica-se a**: banco de dados SQL do Azure e SQL instância gerenciada<br /><br /> Duração da execução da consulta em milissegundos |
| event_time | **datetime2** | Data e hora em que a ação auditável é acionada. Não permite valor nulo. |  
| file_name | **varchar(260)** | O caminho e nome do arquivo de log de auditoria que deu origem ao registro. Não permite valor nulo. |
| is_column_permission | **bit** | Sinalizador que indica se esta é uma permissão no nível de coluna. Não permite valor nulo. Retorna 0 quando permission_bitmask = 0.<br /> 1 = true<br /> 0 = false |
| object_id | **int** | A ID da entidade na qual a auditoria ocorreu. Isso inclui o seguinte:<br /> Objetos do servidor<br /> Bancos de dados<br /> Objetos de banco de dados<br /> Objetos de esquema<br /> Não permite valor nulo. Retornará 0 se a entidade for o próprio Servidor ou se a auditoria não for realizada no nível de um objeto. Por exemplo, Autenticação. |  
| object_name | **sysname** | O nome da entidade na qual a auditoria ocorreu. Isso inclui o seguinte:<br /> Objetos do servidor<br /> Bancos de dados<br /> Objetos de banco de dados<br /> Objetos de esquema<br /> Permite valor nulo. Retornará NULL se a entidade for o próprio Servidor ou se a auditoria não for realizada no nível de um objeto. Por exemplo, Autenticação. |
| permission_bitmask | **varbinary(16)** | Em algumas ações, são as permissões que foram concedidas, negadas ou revogadas. |
| response_rows | **bigint** | **Aplica-se a**: banco de dados SQL do Azure e SQL instância gerenciada<br /><br /> Número de linhas retornadas no conjunto de resultados. |  
| schema_name | **sysname** | O contexto do esquema no qual a ação aconteceu. Permite valor nulo. Retorna NULL para auditorias que ocorrem fora de um esquema. |  
| sequence_group_id | **varbinary** | **Aplica-se a**: somente SQL Server (começando com 2016)<br /><br />  Identificador exclusivo |  
| sequence_number | **int** | Rastreia a sequência de registros dentro de um único registro de auditoria que é muito grande para se ajustar no buffer de gravação das auditorias. Não permite valor nulo. |  
| server_instance_name | **sysname** | Nome da instância de servidor no qual a auditoria ocorreu. O formato servidor\instância padrão é usado. |  
| server_principal_id | **int** | ID do contexto de logon em que a ação é executada. Não permite valor nulo. |  
| server_principal_name | **sysname** | Logon atual. Permite valor nulo. |  
| server_principal_sid | **varbinary** | SID do logon atual. Permite valor nulo. |  
| session_id | **smallint** | Identificação da sessão em que ocorreu o evento. Não permite valor nulo. |  
| session_server_principal_name | **sysname** | Entidade de segurança do servidor para sessão. Permite valor nulo. |  
| instrução | **nvarchar(4000)** | Instrução TSQL, se existir. Permite valor nulo. Retorna NULL se não aplicável. |  
| bem-sucedido | **bit** | Indica se a ação que disparou o evento foi bem-sucedida. Não permite valor nulo. Para todos os demais eventos que não são eventos de logon, reporta somente se a verificação de permissões foi bem-sucedida ou não, e não a operação.<br /> 1 = Êxito<br /> 0 = falha |
| target_database_principal_id | **int** | O banco de dados principal no qual a operação GRANT/DENY/REVOKE é executada. Não permite valor nulo. Retorna 0 se não aplicável. |  
| target_database_principal_name | **sysname** | Usuário de destino da ação. Permite valor nulo. Retorna NULL se não aplicável. |  
| target_server_principal_id | **int** | Diretor de Servidor que o GRANT/operação do DENY/REVOKE é executada em. Não permite valor nulo. Retorna 0 se não aplicável. |  
| target_server_principal_name | **sysname** | Logon de destino da ação. Permite valor nulo. Retorna NULL se não aplicável. |  
| target_server_principal_sid | **varbinary** | SID do logon de destino. Permite valor nulo. Retorna NULL se não aplicável. |  
| transaction_id | **bigint** | **Aplica-se a**: somente SQL Server (começando com 2016)<br /><br /> Identificador exclusivo para identificar vários eventos de auditoria em uma transação |  
| user_defined_event_id | **smallint** | **Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior, banco de dados SQL do Azure e SQL instância gerenciada<br /><br /> ID do evento definido pelo usuário passada como um argumento para **sp_audit_write**. **NULL** para eventos do sistema (padrão) e diferente de zero para o evento definido pelo usuário. Para obter mais informações, consulte [sp_audit_write &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-audit-write-transact-sql.md). |  
| user_defined_information | **nvarchar(4000)** | **Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior, banco de dados SQL do Azure e SQL instância gerenciada<br /><br /> Usado para registrar informações adicionais que o usuário deseja registrar no log de auditoria usando o procedimento armazenado **sp_audit_write** . |  

  
## <a name="remarks"></a>Comentários  
 Se o argumento de *file_pattern* passado para **fn_get_audit_file** fizer referência a um caminho ou arquivo que não existe, ou se o arquivo não for um arquivo de auditoria, a mensagem de erro **MSG_INVALID_AUDIT_FILE** será retornada.  
  
## <a name="permissions"></a>Permissões

- **SQL Server**: requer a permissão **Control Server** .  
- **Banco de dados SQL do Azure**: requer a permissão **Control Database** .     
  - Os administradores de servidor podem acessar os logs de auditoria de todos os bancos de dados no servidor.
  - Os administradores de servidor não podem acessar somente os logs de auditoria do banco de dados atual.
  - Os blobs que não atenderem aos critérios acima serão ignorados (uma lista de BLOBs ignorados será exibida na mensagem de saída da consulta) e a função retornará logs somente de BLOBs para os quais o acesso é permitido.  
  
## <a name="examples"></a>Exemplos

- **SQL Server**

  Este exemplo lê de um arquivo chamado `\\serverName\Audit\HIPAA_AUDIT.sqlaudit`.  
  
  ```  
  SELECT * FROM sys.fn_get_audit_file ('\\serverName\Audit\HIPAA_AUDIT.sqlaudit',default,default);  
  GO  
  ```  

- **Banco de Dados SQL do Azure**

  Este exemplo lê de um arquivo chamado `ShiraServer/MayaDB/SqlDbAuditing_Audit/2017-07-14/10_45_22_173_1.xel` :  
  
  ```  
  SELECT * FROM sys.fn_get_audit_file ('https://mystorage.blob.core.windows.net/sqldbauditlogs/ShiraServer/MayaDB/SqlDbAuditing_Audit/2017-07-14/10_45_22_173_1.xel',default,default);
  GO  
  ```  

  Este exemplo lê o mesmo arquivo acima, mas com cláusulas T-SQL adicionais (**Top**, **order by**e cláusula **Where** para filtrar os registros de auditoria retornados pela função):
  
  ```  
  SELECT TOP 10 * FROM sys.fn_get_audit_file ('https://mystorage.blob.core.windows.net/sqldbauditlogs/ShiraServer/MayaDB/SqlDbAuditing_Audit/2017-07-14/10_45_22_173_1.xel',default,default)
  WHERE server_principal_name = 'admin1'
  ORDER BY event_time
  GO
  ```  

  Este exemplo lê todos os logs de auditoria de servidores que começam com `Sh` : 
  
  ```  
  SELECT * FROM sys.fn_get_audit_file ('https://mystorage.blob.core.windows.net/sqldbauditlogs/Sh',default,default);
  GO  
  ```

Para obter um exemplo completo de como criar uma auditoria, consulte [Auditoria do SQL Server &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md).

Para obter informações sobre como configurar a auditoria do banco de dados SQL do Azure, consulte Introdução [à auditoria do banco de dados SQL](https://docs.microsoft.com/azure/sql-database/sql-database-auditing).
  
## <a name="see-also"></a>Consulte Também  
 [CRIAR auditoria de servidor &#40;&#41;Transact-SQL ](../../t-sql/statements/create-server-audit-transact-sql.md)   
 [ALTER SERVER AUDIT &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-audit-transact-sql.md)   
 [DROP SERVER AUDIT &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-audit-transact-sql.md)   
 [CREATE SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/create-server-audit-specification-transact-sql.md)   
 [ALTER SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-audit-specification-transact-sql.md)   
 [DROP SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-audit-specification-transact-sql.md)   
 [CREATE DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/create-database-audit-specification-transact-sql.md)   
 [ALTER DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-audit-specification-transact-sql.md)   
 [DROP DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-audit-specification-transact-sql.md)   
 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [sys.server_audits &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-audits-transact-sql.md)   
 [sys.server_file_audits &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-file-audits-transact-sql.md)   
 [sys.server_audit_specifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-audit-specifications-transact-sql.md)   
 [sys.server_audit_specification_details &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-audit-specification-details-transact-sql.md)   
 [sys.database_audit_specifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-audit-specifications-transact-sql.md)   
 [sys.database_audit_specification_details &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-audit-specification-details-transact-sql.md)   
 [sys.dm_server_audit_status &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-server-audit-status-transact-sql.md)   
 [sys.dm_audit_actions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-actions-transact-sql.md)   
 [sys.dm_audit_class_type_map &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-class-type-map-transact-sql.md)   
 [Criar uma auditoria de servidor e uma especificação de auditoria de servidor](../../relational-databases/security/auditing/create-a-server-audit-and-server-audit-specification.md)  
  
  
