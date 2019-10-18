---
title: sys. fn_get_audit_file (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
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
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 7fa19a06d3743e91665ee2355eb5f6c380df413d
ms.sourcegitcommit: 8cb26b7dd40280a7403d46ee59a4e57be55ab462
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/17/2019
ms.locfileid: "72542229"
---
# <a name="sysfn_get_audit_file-transact-sql"></a>sys. fn_get_audit_file (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna informações de um arquivo de auditoria criado por uma auditoria de servidor no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, consulte [SQL Server &#40;Audit&#41;mecanismo de banco de dados](../../relational-databases/security/auditing/sql-server-audit-database-engine.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [convenções de sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
fn_get_audit_file ( file_pattern,   
    { default | initial_file_name | NULL },   
    { default | audit_record_offset | NULL } )  
```  
  
## <a name="arguments"></a>argumentos  
 *file_pattern*  
 Especifica o diretório ou caminho e nome de arquivo para o conjunto de arquivos de auditoria a ser lido. O tipo é **nvarchar (260)** . 
 
 - **SQL Server**:
    
    Esse argumento deve incluir um caminho (letra da unidade ou compartilhamento de rede) e um nome de arquivo que pode incluir um curinga. Um único asterisco (*) pode ser usado para coletar vários arquivos de um conjunto de arquivos de auditoria. Por exemplo:  
  
    -   **\<path > \\ \*** -coletar todos os arquivos de auditoria no local especificado.  
  
    -   **\<path > \LoginsAudit_{GUID}** -coleta todos os arquivos de auditoria que têm o nome e o par GUID especificados.  
  
    -   **\<path > \LoginsAudit_{GUID}_00_29384.sqlaudit** -coleta um arquivo de auditoria específico.  
  
 - **Banco de dados SQL do Azure**:
 
    Esse argumento é usado para especificar uma URL de BLOB (incluindo o ponto de extremidade de armazenamento e o contêiner). Embora não ofereça suporte a um curinga de asterisco, você pode usar um prefixo de nome de arquivo parcial (BLOB) (em vez do nome de blob completo) para coletar vários arquivos (BLOBs) que começam com esse prefixo. Por exemplo:
 
      - **\<Storage_endpoint \> / \<Container \> / \<ServerName \> / 0DatabaseName 1** 2-coleta todos os arquivos de auditoria (BLOBs) do banco de dados específico.    
      
      - **\<Storage_endpoint \> / \<Container \> / \<ServerName \> / 0DatabaseName 1 2 3AuditName 4 5 6CreationDate 7 8 9FileName 0. xel** -coleta um arquivo de auditoria específico (BLOB).
  
> [!NOTE]  
>  Passar um caminho sem um padrão de nome de arquivo gerará um erro.  
  
 *initial_file_name*  
 Especifica o caminho e o nome de um arquivo específico no conjunto de arquivos de auditoria para começar a ler registros de auditoria. O tipo é **nvarchar (260)** .  
  
> [!NOTE]  
>  O argumento *initial_file_name* deve conter entradas válidas ou deve conter o padrão | Valor nulo.  
  
 *audit_record_offset*  
 Especifica um local conhecido com o arquivo especificado para o initial_file_name. Quando esse argumento for usado, a função começará a ler no primeiro registro do buffer imediatamente após o deslocamento especificado.  
  
> [!NOTE]  
>  O argumento *audit_record_offset* deve conter entradas válidas ou deve conter o padrão | Valor nulo. O tipo é **bigint**.  
  
## <a name="tables-returned"></a>Tabelas retornadas  
 A tabela a seguir descreve o conteúdo do arquivo de auditoria que pode ser retornado por essa função.  
  
| Nome da coluna | Escreva | Description |  
|-------------|------|-------------|  
| action_id | **varchar (4)** | ID da ação. Não permite valor nulo. |  
| additional_information | **nvarchar (4000)** | Informações exclusivas que se aplicam apenas a um único evento são retornadas como XML. Um pequeno número de ações auditáveis contém esse tipo de informação.<br /><br /> Um nível de pilha TSQL será exibido em formato XML para ações que têm a pilha TSQL associada a eles. O formato XML será:<br /><br /> `<tsql_stack><frame nest_level = '%u' database_name = '%.*s' schema_name = '%.*s' object_name = '%.*s' /></tsql_stack>`<br /><br /> Frame nest_level indica o nível de aninhamento atual do quadro. O nome do módulo é representado em formato de três partes (database_name, schema_name e object_name).  O nome do módulo será analisado para escapar caracteres XML inválidos, como `'\<'`, `'>'`, `'/'` `'_x'`. Eles serão ignorados como `_xHHHH\_`. O HHHH significa o código UCS-2 hexadecimal de quatro dígitos para o caractere<br /><br /> Permite valor nulo. Retorna NULL quando não há informações adicionais relatadas pelo evento. |
| affected_rows | **bigint** | **Aplica-se a**: somente BD SQL do Azure<br /><br /> Número de linhas afetadas pela instrução executada. |  
| application_name | **nvarchar(128** | **Aplica-se a**: BD SQL do Azure + SQL Server (a partir de 2017)<br /><br /> Nome do aplicativo cliente que executou a instrução que causou o evento de auditoria |  
| audit_file_offset | **bigint** | **Aplica-se a**: somente SQL Server<br /><br /> O deslocamento do buffer no arquivo que contém o registro de auditoria. Não permite valor nulo. |  
| audit_schema_version | **inteiro** | Sempre 1 |  
| class_type | **varchar (2)** | O tipo de entidade auditável na qual a auditoria ocorre. Não permite valor nulo. |  
| client_ip | **nvarchar(128** | **Aplica-se a**: BD SQL do Azure + SQL Server (a partir de 2017)<br /><br />    IP de origem do aplicativo cliente |  
| connection_id | VOLUME | **Aplica-se a**: banco de BD SQL do Azure e instância gerenciada<br /><br /> ID da conexão no servidor |
| data_sensitivity_information | nvarchar (4000) | **Aplica-se a**: somente BD SQL do Azure<br /><br /> Tipos de informações e rótulos de sensibilidade retornados pela consulta auditada, com base nas colunas classificadas no banco de dados. Saiba mais sobre a [descoberta e a classificação de dados do banco SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-data-discovery-and-classification) |
| database_name | **sysname** | O contexto do banco de dados no qual a ação ocorreu. Permite valor nulo. Retorna NULL para auditorias que ocorrem no nível do servidor. |  
| database_principal_id | **inteiro** |ID do contexto de usuário do banco de dados no qual a ação é executada. Não permite valor nulo. Retornará 0 se isso não se aplicar. Por exemplo, uma operação de servidor.|
| database_principal_name | **sysname** | Usuário atual. Permite valor nulo. Retornará NULL se não estiver disponível. |  
| duration_milliseconds | **bigint** | **Aplica-se a**: banco de BD SQL do Azure e instância gerenciada<br /><br /> Duração da execução da consulta em milissegundos |
| event_time | **datetime2** | Data e hora em que a ação auditável é acionada. Não permite valor nulo. |  
| nome_do_arquivo | **varchar (260)** | O caminho e o nome do arquivo de log de auditoria do qual o registro veio. Não permite valor nulo. |
| is_column_permission | **parte** | Sinalizador que indica se esta é uma permissão de nível de coluna. Não permite valor nulo. Retorna 0 quando permission_bitmask = 0.<br /> 1 = verdadeiro<br /> 0 = falso |
| object_id | **inteiro** | A ID da entidade na qual a auditoria ocorreu. Isso inclui o seguinte:<br /> Objetos de servidor<br /> Bancos<br /> Objetos de banco de dados<br /> Objetos de esquema<br /> Não permite valor nulo. Retornará 0 se a entidade for o próprio servidor ou se a auditoria não for executada em um nível de objeto. Por exemplo, autenticação. |  
| object_name | **sysname** | O nome da entidade na qual a auditoria ocorreu. Isso inclui o seguinte:<br /> Objetos de servidor<br /> Bancos<br /> Objetos de banco de dados<br /> Objetos de esquema<br /> Permite valor nulo. Retornará NULL se a entidade for o próprio servidor ou se a auditoria não for executada em um nível de objeto. Por exemplo, autenticação. |
| permission_bitmask | **varbinary (16)** | Em algumas ações, essas são as permissões que foram concedidas, negadas ou revogadas. |
| response_rows | **bigint** | **Aplica-se a**: banco de BD SQL do Azure e instância gerenciada<br /><br /> Número de linhas retornadas no conjunto de resultados. |  
| schema_name | **sysname** | O contexto do esquema no qual a ação aconteceu. Permite valor nulo. Retorna NULL para auditorias que ocorrem fora de um esquema. |  
| sequence_group_id | **varbinary** | **Aplica-se a**: somente SQL Server (começando com 2016)<br /><br />  Identificador exclusivo |  
| sequence_number | **inteiro** | Rastreia a sequência de registros dentro de um único registro de auditoria que é muito grande para se ajustar no buffer de gravação das auditorias. Não permite valor nulo. |  
| server_instance_name | **sysname** | Nome da instância do servidor em que ocorreu a auditoria. O formato padrão servidor \ instância é usado. |  
| server_principal_id | **inteiro** | ID do contexto de logon no qual a ação é executada. Não permite valor nulo. |  
| server_principal_name | **sysname** | Logon atual. Permite valor nulo. |  
| server_principal_sid | **varbinary** | SID do logon atual. Permite valor nulo. |  
| session_id | **smallint** | ID da sessão na qual o evento ocorreu. Não permite valor nulo. |  
| session_server_principal_name | **sysname** | Entidade de segurança do servidor para sessão. Permite valor nulo. |  
| privacidade | **nvarchar (4000)** | Instrução TSQL, se existir. Permite valor nulo. Retorna NULL se não aplicável. |  
| foi | **parte** | Indica se a ação que disparou o evento foi bem-sucedida. Não permite valor nulo. Para todos os eventos que não sejam eventos de logon, isso apenas relata se a verificação de permissão foi bem-sucedida ou falhou, não a operação.<br /> 1 = êxito<br /> 0 = falha |
| target_database_principal_id | **inteiro** | A entidade de banco de dados que a operação GRANT/DENY/REVOKE é executada em. Não permite valor nulo. Retorna 0 se não aplicável. |  
| target_database_principal_name | **sysname** | Usuário de destino da ação. Permite valor nulo. Retorna NULL se não aplicável. |  
| target_server_principal_id | **inteiro** | Entidade de segurança do servidor na qual a operação de concessão/NEGAção/REVOGAção é executada. Não permite valor nulo. Retorna 0 se não aplicável. |  
| target_server_principal_name | **sysname** | Logon de destino da ação. Permite valor nulo. Retorna NULL se não aplicável. |  
| target_server_principal_sid | **varbinary** | SID do logon de destino. Permite valor nulo. Retorna NULL se não aplicável. |  
| transaction_id | **bigint** | **Aplica-se a**: somente SQL Server (começando com 2016)<br /><br /> Identificador exclusivo para identificar vários eventos de auditoria em uma transação |  
| user_defined_event_id | **smallint** | **Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], banco de BD SQL do Azure e instância gerenciada<br /><br /> ID do evento definido pelo usuário passada como um argumento para **sp_audit_write**. **NULL** para eventos do sistema (padrão) e diferente de zero para o evento definido pelo usuário. Para obter mais informações, [consulte &#40;Transact-SQL&#41;sp_audit_write](../../relational-databases/system-stored-procedures/sp-audit-write-transact-sql.md). |  
| user_defined_information | **nvarchar (4000)** | **Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], banco de BD SQL do Azure e instância gerenciada<br /><br /> Usado para registrar informações adicionais que o usuário deseja registrar no log de auditoria usando o procedimento armazenado **sp_audit_write** . |  

  
## <a name="remarks"></a>Remarks  
 Se o argumento *file_pattern* passado para **fn_get_audit_file** fizer referência a um caminho ou arquivo que não existe, ou se o arquivo não for um arquivo de auditoria, a mensagem de erro **MSG_INVALID_AUDIT_FILE** será retornada.  
  
## <a name="permissions"></a>Permissões

- **SQL Server**: requer a permissão **Control Server** .  
- **Banco de dados SQL do Azure**: requer a permissão **Control Database** .     
  - Os administradores de servidor podem acessar os logs de auditoria de todos os bancos de dados no servidor.
  - Os administradores de servidor não podem acessar somente os logs de auditoria do banco de dados atual.
  - Os blobs que não atenderem aos critérios acima serão ignorados (uma lista de BLOBs ignorados será exibida na mensagem de saída da consulta) e a função retornará logs somente de BLOBs para os quais o acesso é permitido.  
  
## <a name="examples"></a>Disso

- **SQL Server**

  Este exemplo lê de um arquivo chamado `\\serverName\Audit\HIPAA_AUDIT.sqlaudit`.  
  
  ```  
  SELECT * FROM sys.fn_get_audit_file ('\\serverName\Audit\HIPAA_AUDIT.sqlaudit',default,default);  
  GO  
  ```  

- **Banco de dados SQL do Azure**

  Este exemplo lê de um arquivo chamado `ShiraServer/MayaDB/SqlDbAuditing_Audit/2017-07-14/10_45_22_173_1.xel`:  
  
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

  Este exemplo lê todos os logs de auditoria de servidores que começam com `Sh`: 
  
  ```  
  SELECT * FROM sys.fn_get_audit_file ('https://mystorage.blob.core.windows.net/sqldbauditlogs/Sh',default,default);
  GO  
  ```

Para obter um exemplo completo sobre como criar uma auditoria, consulte [SQL Server mecanismo de banco de dados &#40;&#41;de auditoria](../../relational-databases/security/auditing/sql-server-audit-database-engine.md).

Para obter informações sobre como configurar a auditoria do banco de dados SQL do Azure, consulte Introdução [à auditoria do banco de dados SQL](https://docs.microsoft.com/azure/sql-database/sql-database-auditing).
  
## <a name="see-also"></a>Consulte também  
 [Criar   de &#40;auditoria de servidor&#41; Transact-SQL](../../t-sql/statements/create-server-audit-transact-sql.md)  
 [ALTER Server Audit &#40;Transact-SQL&#41; ](../../t-sql/statements/alter-server-audit-transact-sql.md)    
 [Descartar &#40;  de auditoria&#41; do servidor Transact-SQL](../../t-sql/statements/drop-server-audit-transact-sql.md)  
 [Criar &#40;especificação de auditoria de servidor Transact&#41; -SQL](../../t-sql/statements/create-server-audit-specification-transact-sql.md)    
 [Instrução ALTER Server Audit de Transact-SQL&#41; &#40;](../../t-sql/statements/alter-server-audit-specification-transact-sql.md)  
 [Descartar   &#40;de especificação de&#41; auditoria de servidor Transact-SQL](../../t-sql/statements/drop-server-audit-specification-transact-sql.md)  
 [Criar &#40;especificação de auditoria de banco de&#41; dados Transact-SQL](../../t-sql/statements/create-database-audit-specification-transact-sql.md)    
 [Especificação &#40;de auditoria de ALTER DATABASE  &#41; Transact-SQL](../../t-sql/statements/alter-database-audit-specification-transact-sql.md)  
 @No__t_3 [descartar &#40;especificação de auditoria&#41; de banco de dados Transact-SQL](../../t-sql/statements/drop-database-audit-specification-transact-sql.md)  
 [ALTER AUTHORIZATION &#40;Transact-SQL&#41; ](../../t-sql/statements/alter-authorization-transact-sql.md)    
   [de Transact &#40;-SQL&#41; sys. server_audits](../../relational-databases/system-catalog-views/sys-server-audits-transact-sql.md)  
   [de Transact &#40;-SQL&#41; sys. server_file_audits](../../relational-databases/system-catalog-views/sys-server-file-audits-transact-sql.md)  
   [de Transact &#40;-SQL&#41; sys. server_audit_specifications](../../relational-databases/system-catalog-views/sys-server-audit-specifications-transact-sql.md)  
   [de Transact &#40;-SQL&#41; sys. server_audit_specification_details](../../relational-databases/system-catalog-views/sys-server-audit-specification-details-transact-sql.md)  
   [de Transact &#40;-SQL&#41; sys. database_audit_specifications](../../relational-databases/system-catalog-views/sys-database-audit-specifications-transact-sql.md)  
   [de Transact &#40;-SQL&#41; sys. database_audit_specification_details](../../relational-databases/system-catalog-views/sys-database-audit-specification-details-transact-sql.md)  
   [de Transact- &#40;SQL&#41; sys. dm _server_audit_status](../../relational-databases/system-dynamic-management-views/sys-dm-server-audit-status-transact-sql.md)  
   [de Transact- &#40;SQL&#41; sys. dm _audit_actions](../../relational-databases/system-dynamic-management-views/sys-dm-audit-actions-transact-sql.md)  
   [de Transact- &#40;SQL&#41; sys. dm _audit_class_type_map](../../relational-databases/system-dynamic-management-views/sys-dm-audit-class-type-map-transact-sql.md)  
 [Criar uma auditoria de servidor e uma especificação de auditoria de servidor](../../relational-databases/security/auditing/create-a-server-audit-and-server-audit-specification.md)  
  
  
