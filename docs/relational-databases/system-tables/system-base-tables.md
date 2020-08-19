---
description: Tabelas base do sistema
title: Tabelas base do sistema | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- system base tables [SQL Server]
- hobt [SQL Server]
- base tables
ms.assetid: 31f2df90-651f-4699-8067-19f59b60904f
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: c60aad12977f5260cc108697e52245bc8a37d9d3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88446530"
---
# <a name="system-base-tables"></a>Tabelas base do sistema
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Tabelas base do sistema são tabelas subjacentes que, na prática, armazenam metadados em um banco de dados específico. O banco de dados **mestre** é especial nesse sentido porque contém algumas tabelas adicionais que não são encontradas em nenhum dos outros bancos de dados. Essas tabelas contêm metadados persistentes com escopo em todo o servidor.  
  
> [!IMPORTANT]  
>  As tabelas base do sistema são só usadas no [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] e não são para uso geral do cliente. Eles estão sujeitos à alteração e não há garantia de compatibilidade.  
  
## <a name="system-base-table-metadata"></a>Metadados da tabela base do sistema  
 Um entidade autorizada que tem a permissão CONTROL, ALTER ou VIEW DEFINITION em um banco de dados pode ver os metadados da tabela base do sistema na exibição do catálogo **Sys. Objects** . O entidade autorizada também pode resolver os nomes e as IDs de objeto das tabelas base do sistema usando funções internas, como [object_name](../../t-sql/functions/object-name-transact-sql.md) e [object_id](../../t-sql/functions/object-id-transact-sql.md).  
  
 Para fazer uma associação a uma tabela base do sistema, o usuário deve se conectar à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], usando uma conexão de administrador dedicada (DAC). Um erro é gerado ao tentar executar uma consulta SELECT de uma tabela base do sistema sem fazer a conexão usando DAC.  
  
> [!IMPORTANT]  
>  O acesso a tabelas base do sistema por DAC é projetado apenas para pessoal do [!INCLUDE[msCoName](../../includes/msconame-md.md)] e não é um cenário de cliente com suporte.  
  
## <a name="system-base-tables"></a>Tabelas base do sistema  
 A tabela a seguir lista e descreve cada tabela base do sistema no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Tabela base|Descrição|  
|----------------|-----------------|  
|**sys.sysschobjs**|Existe em todos os bancos de dados. Cada linha representa um objeto no banco de dados.|  
|**sys.sysschobjs**|Existe em todos os bancos de dados. Contém uma linha para cada entidade do Service Broker no banco de dados. Entidades do Service Broker incluem o seguinte:<br /><br /> Tipo de mensagem<br /><br /> Contrato de serviço<br /><br /> Serviço<br /><br /> Os nomes e tipos usam ordenação primária que é fixa.|  
|**sys.sysclsobjs**|Existe em todos os bancos de dados. Contém uma linha para cada entidade classificada que compartilha as mesmas propriedades comuns que incluem o seguinte:<br /><br /> Assembly<br /><br /> Dispositivo de backup<br /><br /> Catálogo de texto completo<br /><br /> Função de partição<br /><br /> Esquema de partição<br /><br /> Grupo de arquivos<br /><br /> Chave de ofuscação|  
|**sys.sysnsobjs**|Existe em todos os bancos de dados. Contém uma linha para cada entidade no escopo de namespace. Esta tabela é usada para armazenar entidades de coleção XML.|  
|**sys.syscolpars**|Existe em todos os bancos de dados. Contém uma linha para cada coluna de uma tabela, exibição ou função com valor de tabela. Também contém linhas para cada parâmetro de um procedimento ou função.|  
|**sys.systypedsubobjs**|Existe em todos os bancos de dados. Contém uma linha para cada subentidade digitada. Apenas parâmetros de função de partição entram nessa categoria.|  
|**sys.sysidxstats**|Existe em todos os bancos de dados. Contém uma linha para cada índice ou estatísticas de tabelas e exibições indexadas<br /><br /> Observação: cada índice (exceto heap) é associado a uma estatística que tem o mesmo nome que o índice.|  
|**sys.sysiscols**|Existe em todos os bancos de dados. Contém uma linha para cada índice persistente e coluna de estatísticas.|  
|**sys.sysscalartypes**|Existe em todos os bancos de dados. Contém uma linha para cada tipo definido pelo usuário ou sistema.|  
|**sys.sysdbreg**|Existe somente no banco de dados **mestre** . Contém uma linha para cada banco de dados registrado.|  
|**sys.sysxsrvs**|Existe somente no banco de dados **mestre** . Contém uma linha para cada servidor local, vinculado ou remoto.|  
|**sys.sysrmtlgns**|Esta tabela base do sistema existe somente no banco de dados **mestre** . Contém uma linha para cada mapeamento de logon remoto. Isso é usado para mapear logons que dizem estar vindo de um servidor correspondente para um logon local real.|  
|**sys.syslnklgns**|Existe somente no banco de dados **mestre** . Contém uma linha para cada mapeamento de logon vinculado. Mapeamentos de logon vinculados são usados por chamadas remotas de procedimento e consultas distribuídas que vão de um servidor local para um servidor vinculado correspondente.|  
|**sys.sysxlgns**|Existe somente no banco de dados **mestre** . Contém uma linha para cada principal de servidor.|  
|**sys.sysdbfiles**|Existe em todos os bancos de dados. Se a coluna **DBID** for zero, a linha representará um arquivo que pertence a esse banco de dados. No banco de dados **mestre** , a coluna **DBID** pode ser diferente de zero. Quando esse for o caso, a linha representa um arquivo mestre.|  
|**sys.sysusermsg**|Existe somente no banco de dados **mestre** . Cada linha representa uma mensagem de erro definida pelo usuário.|  
|**sys.sysprivs**|Existe em todos os bancos de dados. Contém uma linha para cada banco de dados - ou permissão em nível do servidor.<br /><br /> Observação: permissões de nível de servidor são armazenadas no banco de dados **mestre** .|  
|**sys.sysowners**|Existe em todos os bancos de dados. Cada linha representa um principal de banco de dados.|  
|**sys.sysobjkeycrypts**|Existe em todos os bancos de dados. Contém uma linha para cada chave simétrica, criptografia ou propriedade criptográfica associada a um objeto.|  
|**sys.syscerts**|Existe em todos os bancos de dados. Contém uma linha para cada certificado em um banco de dados.|  
|**sys.sysasymkeys**|Existe em todos os bancos de dados. Cada linha representa uma chave assimétrica.|  
|**sys.ftinds**|Existe em todos os bancos de dados. Contém uma linha para cada índice de texto completo no banco de dados.|  
|**sys.sysxprops**|Existe em todos os bancos de dados. Contém uma linha para cada propriedade estendida.|  
|**sys.sysallocunits**|Existe em todos os bancos de dados. Contém uma linha para cada unidade de alocação de armazenamento.|  
|**sys.sysrowsets**|Existe em todos os bancos de dados. Contém uma linha para cada conjunto de linhas de partição para um índice ou um heap.|  
|**sys.sysrowsetrefs**|Existe em todos os bancos de dados. Contém uma linha para cada índice para referência de conjunto de linhas.|  
|**sys.syslogshippers**|Existe somente no banco de dados **mestre** . Contém uma linha para cada banco de dados de testemunha espelhada.|  
|**sys.sysremsvcbinds**|Existe em todos os bancos de dados. Contém uma linha para cada associação de serviço remoto.|  
|**sys.sysconvgroup**|Existe em todos os bancos de dados. Contém uma linha para cada instância de serviço no Service Broker.|  
|**sys.sysxmitqueue**|Existe em todos os bancos de dados. Contém uma linha para cada fila de transmissão do Service Broker.|  
|**sys.sysdesend**|Existe em todos os bancos de dados. Contém uma linha para cada ponto de extremidade de envio de uma conversa do Service Broker.|  
|**sys.sysdercv**|Existe em todos os bancos de dados. Contém uma linha para cada ponto de extremidade de recebimento de uma conversa do Service Broker.|  
|**sys.sysendpts**|Existe somente no banco de dados **mestre** . Contém uma linha para cada ponto de extremidade criado no servidor.|  
|**sys.syswebmethods**|Existe somente no banco de dados **mestre** . Contém uma linha para cada método SOAP definido em um ponto de extremidade HTTP habilitado por SOAP criado no servidor.|  
|**sys.sysqnames**|Existe em todos os bancos de dados. Contém uma linha para cada namespace ou nome qualificado para um token de ID de 4 bytes.|  
|**sys.sysxmlcomponent**|Existe em todos os bancos de dados. Cada linha representa um componente de esquema XML.|  
|**sys.sysxmlfacet**|Existe em todos os bancos de dados. Contém uma linha para cada faceta XML (restrição) de definição de tipo XML.|  
|**sys.sysxmlplacement**|Existe em todos os bancos de dados. Contém uma linha para cada colocação XML de componentes XML.|  
|**sys.syssingleobjrefs**|Existe em todos os bancos de dados. Contém uma linha para cada referência geral N-a-1.|  
|**sys.sysmultiobjrefs**|Existe em todos os bancos de dados. Contém uma linha para cada referência geral N-a-N.|  
|**sys.sysobjvalues**|Existe em todos os bancos de dados. Contém uma linha para cada propriedade de valor geral de uma entidade.|  
|**sys.sysguidrefs**|Existe em todos os bancos de dados. Contém uma linha para cada referência de ID classificada por GUID.|  
  
## <a name="updating-system-base-tables"></a>Atualizando tabelas base do sistema    
Você pode exibir os dados nas tabelas do sistema por meio das exibições do catálogo do sistema. Para atualizar os metadados em uma tabela base do sistema, use a interface TSQL apropriada (por exemplo, instruções DDL). Você não pode atualizar manualmente as tabelas do sistema. SQL Server relata as mensagens a seguir ao executar atualizações diretas em tabelas do sistema.

### <a name="a-system-table-is-manually-updated"></a>Uma tabela do sistema é atualizada manualmente
Msg 17659: Aviso: a ID da tabela do sistema <id> foi atualizada diretamente na ID do banco de dados <id> e a coerência de cache talvez não tenha sido mantida. O SQL Server deve ser reiniciado.

### <a name="starting-a-database-with-a-system-table-that-was-manually-updated"></a>Iniciando um banco de dados com uma tabela do sistema que foi atualizada manualmente
MSG 3859: aviso: o catálogo do sistema foi atualizado diretamente na ID de banco de dados 17, mais recentemente em date_time.

### <a name="executing-the-dbcc_checkdb-command-after-a-system-table-is-manually-updated"></a>Executando o comando DBCC_CHECKDB depois que uma tabela do sistema é atualizada manualmente
MSG 3859: aviso: o catálogo do sistema foi atualizado diretamente na ID de banco de dados 17, mais recentemente em date_time.

Se você executar atualizações manuais em uma tabela do sistema e encontrar um problema, você poderá ser solicitado a restaurar a partir de um backup ou copiar os dados do banco de dado afetado para um novo banco. Saiba mais sobre [mensagens de erro de ação do usuário](https://docs.microsoft.com/sql/relational-databases/errors-events/mssqlserver-8992-database-engine-error?view=sql-server-ver15#user-action).
