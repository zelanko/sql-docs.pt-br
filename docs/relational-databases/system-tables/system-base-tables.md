---
title: Tabelas de Base do Sistema | Microsoft Docs
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
author: stevestein
ms.author: sstein
ms.openlocfilehash: 5ac374b9222f9bd592312f79173859691b495276
ms.sourcegitcommit: 1124b91a3b1a3d30424ae0fec04cfaa4b1f361b6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/01/2020
ms.locfileid: "80531197"
---
# <a name="system-base-tables"></a>Tabelas base do sistema
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Tabelas base do sistema são tabelas subjacentes que, na prática, armazenam metadados em um banco de dados específico. O banco de dados **mestre** é especial neste aspecto porque contém algumas tabelas adicionais que não são encontradas em nenhuma das outras bases de dados. Essas tabelas contêm metadados persistentes com escopo em todo o servidor.  
  
> [!IMPORTANT]  
>  As tabelas base do sistema são só usadas no [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] e não são para uso geral do cliente. Eles estão sujeitos à alteração e não há garantia de compatibilidade.  
  
## <a name="system-base-table-metadata"></a>Metadados da tabela base do sistema  
 Um beneficiário que tenha permissão DE CONTROLE, ALTER ou DEFINIÇÃO DE VISUALIZAÇÃO em um banco de dados pode ver metadados da tabela base do sistema na exibição do catálogo **sys.objects.** O beneficiário também pode resolver os nomes e os IDs de objetos das tabelas base do sistema usando funções incorporadas, como [OBJECT_NAME](../../t-sql/functions/object-name-transact-sql.md) e [OBJECT_ID](../../t-sql/functions/object-id-transact-sql.md).  
  
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
|**sys.sysidxstats**|Existe em todos os bancos de dados. Contém uma linha para cada índice ou estatísticas de tabelas e exibições indexadas<br /><br /> Nota: Cada índice (exceto pilha) está associado a uma estatística que tem o mesmo nome do índice.|  
|**sys.sysiscols**|Existe em todos os bancos de dados. Contém uma linha para cada índice persistente e coluna de estatísticas.|  
|**sys.sysscalartypes**|Existe em todos os bancos de dados. Contém uma linha para cada tipo definido pelo usuário ou sistema.|  
|**sys.sysdbreg**|Existe apenas no banco de dados **mestre.** Contém uma linha para cada banco de dados registrado.|  
|**sys.sysxsrvs**|Existe apenas no banco de dados **mestre.** Contém uma linha para cada servidor local, vinculado ou remoto.|  
|**sys.sysrmtlgns**|Esta tabela base do sistema existe apenas no banco de dados **mestre.** Contém uma linha para cada mapeamento de logon remoto. Isso é usado para mapear logons que dizem estar vindo de um servidor correspondente para um logon local real.|  
|**sys.syslnklgns**|Existe apenas no banco de dados **mestre.** Contém uma linha para cada mapeamento de logon vinculado. Mapeamentos de logon vinculados são usados por chamadas remotas de procedimento e consultas distribuídas que vão de um servidor local para um servidor vinculado correspondente.|  
|**sys.sysxlgns**|Existe apenas no banco de dados **mestre.** Contém uma linha para cada principal de servidor.|  
|**sys.sysdbfiles**|Existe em todos os bancos de dados. Se a **oferta da** coluna for zero, a linha representa um arquivo que pertence a este banco de dados. No banco de dados **mestre,** a **dbid da** coluna pode ser não zero. Quando esse for o caso, a linha representa um arquivo mestre.|  
|**sys.sysusermsg**|Existe apenas no banco de dados **mestre.** Cada linha representa uma mensagem de erro definida pelo usuário.|  
|**sys.sysprivs**|Existe em todos os bancos de dados. Contém uma linha para cada banco de dados - ou permissão em nível do servidor.<br /><br /> Nota: As permissões em nível de servidor são armazenadas no banco de dados **mestre.**|  
|**sys.sysowners**|Existe em todos os bancos de dados. Cada linha representa um principal de banco de dados.|  
|**sys.sysobjkeycrypts**|Existe em todos os bancos de dados. Contém uma linha para cada chave simétrica, criptografia ou propriedade criptográfica associada a um objeto.|  
|**sys.syscerts**|Existe em todos os bancos de dados. Contém uma linha para cada certificado em um banco de dados.|  
|**sys.sysasymkeys**|Existe em todos os bancos de dados. Cada linha representa uma chave assimétrica.|  
|**sys.ftinds**|Existe em todos os bancos de dados. Contém uma linha para cada índice de texto completo no banco de dados.|  
|**sys.sysxprops**|Existe em todos os bancos de dados. Contém uma linha para cada propriedade estendida.|  
|**sys.sysallocunits**|Existe em todos os bancos de dados. Contém uma linha para cada unidade de alocação de armazenamento.|  
|**sys.sysrowsets**|Existe em todos os bancos de dados. Contém uma linha para cada conjunto de linhas de partição para um índice ou um heap.|  
|**sys.sysrowsetrefs**|Existe em todos os bancos de dados. Contém uma linha para cada índice para referência de conjunto de linhas.|  
|**sys.syslogshippers**|Existe apenas no banco de dados **mestre.** Contém uma linha para cada banco de dados de testemunha espelhada.|  
|**sys.sysremsvcbinds**|Existe em todos os bancos de dados. Contém uma linha para cada associação de serviço remoto.|  
|**sys.sysconvgroup**|Existe em todos os bancos de dados. Contém uma linha para cada instância de serviço no Service Broker.|  
|**sys.sysxmitqueue**|Existe em todos os bancos de dados. Contém uma linha para cada fila de transmissão do Service Broker.|  
|**sys.sysdesend**|Existe em todos os bancos de dados. Contém uma linha para cada ponto de extremidade de envio de uma conversa do Service Broker.|  
|**sys.sysdercv**|Existe em todos os bancos de dados. Contém uma linha para cada ponto de extremidade de recebimento de uma conversa do Service Broker.|  
|**sys.sysendpts**|Existe apenas no banco de dados **mestre.** Contém uma linha para cada ponto de extremidade criado no servidor.|  
|**sys.syswebmethods**|Existe apenas no banco de dados **mestre.** Contém uma linha para cada método SOAP definido em um ponto de extremidade HTTP habilitado por SOAP criado no servidor.|  
|**sys.sysqnames**|Existe em todos os bancos de dados. Contém uma linha para cada namespace ou nome qualificado para um token de ID de 4 bytes.|  
|**sys.sysxmlcomponent**|Existe em todos os bancos de dados. Cada linha representa um componente de esquema XML.|  
|**sys.sysxmlfacet**|Existe em todos os bancos de dados. Contém uma linha para cada faceta XML (restrição) de definição de tipo XML.|  
|**sys.sysxmlplacement**|Existe em todos os bancos de dados. Contém uma linha para cada colocação XML de componentes XML.|  
|**sys.syssingleobjrefs**|Existe em todos os bancos de dados. Contém uma linha para cada referência geral N-a-1.|  
|**sys.sysmultiobjrefs**|Existe em todos os bancos de dados. Contém uma linha para cada referência geral N-a-N.|  
|**sys.sysobjvalues**|Existe em todos os bancos de dados. Contém uma linha para cada propriedade de valor geral de uma entidade.|  
|**sys.sysguidrefs**|Existe em todos os bancos de dados. Contém uma linha para cada referência de ID classificada por GUID.|  
  
## <a name="updating-system-base-tables"></a>Atualizando tabelas de base do sistema    
Você pode visualizar os dados nas tabelas do sistema através das visualizações do catálogo do sistema. Para atualizar os metadados em uma tabela base do sistema, use a interface TSQL apropriada (por exemplo, instruções DDL). Você não pode atualizar manualmente as tabelas do sistema. O SQL Server relata as seguintes mensagens quando você executa atualizações diretas nas tabelas do sistema.

### <a name="a-system-table-is-manually-updated"></a>Uma tabela do sistema é atualizada manualmente
Msg 17659: Aviso: O <id> ID da tabela <id> do sistema foi atualizado diretamente no ID do banco de dados e a coerência do cache pode não ter sido mantida. O SQL Server deve ser reiniciado.

### <a name="starting-a-database-with-a-system-table-that-was-manually-updated"></a>Iniciar um banco de dados com uma tabela de sistema que foi atualizada manualmente
Msg 3859: Aviso: O catálogo do sistema foi atualizado diretamente no banco de dados ID 17, mais recentemente em date_time.

### <a name="executing-the-dbcc_checkdb-command-after-a-system-table-is-manually-updated"></a>Executando o comando DBCC_CHECKDB depois que uma tabela do sistema é atualizada manualmente
Msg 3859: Aviso: O catálogo do sistema foi atualizado diretamente no banco de dados ID 17, mais recentemente em date_time.

Se você executar atualizações manuais em uma tabela do sistema e encontrar um problema, você pode ser solicitado a restaurar a partir de um backup ou copiar os dados do banco de dados afetado para um novo banco de dados. Saiba mais sobre [as mensagens de erro de ação do usuário](https://docs.microsoft.com/sql/relational-databases/errors-events/mssqlserver-8992-database-engine-error?view=sql-server-ver15#user-action).
