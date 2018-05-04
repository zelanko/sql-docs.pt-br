---
title: Tabelas Base do sistema | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- system base tables [SQL Server]
- hobt [SQL Server]
- base tables
ms.assetid: 31f2df90-651f-4699-8067-19f59b60904f
caps.latest.revision: 24
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 68d23efa64d1e67678fb27dc00916aa03dc89ab7
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="system-base-tables"></a>Tabelas base do sistema
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Tabelas base do sistema são tabelas subjacentes que, na prática, armazenam metadados em um banco de dados específico. O **mestre** banco de dados é especial neste aspecto porque contém algumas tabelas adicionais que não são encontradas em qualquer um dos outros bancos de dados. Essas tabelas contêm metadados persistentes com escopo em todo o servidor.  
  
> [!IMPORTANT]  
>  As tabelas base do sistema são só usadas no [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] e não são para uso geral do cliente. Eles estão sujeitos à alteração e não há garantia de compatibilidade.  
  
## <a name="system-base-table-metadata"></a>Metadados da tabela base do sistema  
 Um usuário autorizado que tem a permissão CONTROL, ALTER ou VIEW DEFINITION em um banco de dados pode ver os metadados de tabela base do sistema no **sys. Objects** exibição do catálogo. O usuário autorizado também pode resolver os nomes e IDs de tabelas base do sistema do objeto usando funções internas, como [OBJECT_NAME](../../t-sql/functions/object-name-transact-sql.md) e [OBJECT_ID](../../t-sql/functions/object-id-transact-sql.md).  
  
 Para fazer uma associação a uma tabela base do sistema, o usuário deve se conectar à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], usando uma conexão de administrador dedicada (DAC). Um erro é gerado ao tentar executar uma consulta SELECT de uma tabela base do sistema sem fazer a conexão usando DAC.  
  
> [!IMPORTANT]  
>  O acesso a tabelas base do sistema por DAC é projetado apenas para pessoal do [!INCLUDE[msCoName](../../includes/msconame-md.md)] e não é um cenário de cliente com suporte.  
  
## <a name="system-base-tables"></a>Tabelas base do sistema  
 A tabela a seguir lista e descreve cada tabela base do sistema no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Tabela base|Description|  
|----------------|-----------------|  
|**sys.sysschobjs**|Existe em todos os bancos de dados. Cada linha representa um objeto no banco de dados.|  
|**sys.sysbinobjs**|Existe em todos os bancos de dados. Contém uma linha para cada entidade do Service Broker no banco de dados. Entidades do Service Broker incluem o seguinte:<br /><br /> Tipo de mensagem<br /><br /> Contrato de serviço<br /><br /> Serviço<br /><br /> Os nomes e tipos usam agrupamento binário que é fixo.|  
|**sys.sysclsobjs**|Existe em todos os bancos de dados. Contém uma linha para cada entidade classificada que compartilha as mesmas propriedades comuns que incluem o seguinte:<br /><br /> Assembly<br /><br /> Dispositivo de backup<br /><br /> Catálogo de texto completo<br /><br /> Função de partição<br /><br /> Esquema de partição<br /><br /> Grupo de arquivos<br /><br /> Chave de ofuscação|  
|**sys.sysnsobjs**|Existe em todos os bancos de dados. Contém uma linha para cada entidade no escopo de namespace. Esta tabela é usada para armazenar entidades de coleção XML.|  
|**sys.syscolpars**|Existe em todos os bancos de dados. Contém uma linha para cada coluna de uma tabela, exibição ou função com valor de tabela. Também contém linhas para cada parâmetro de um procedimento ou função.|  
|**sys.systypedsubobjs**|Existe em todos os bancos de dados. Contém uma linha para cada subentidade digitada. Apenas parâmetros de função de partição entram nessa categoria.|  
|**sys.sysidxstats**|Existe em todos os bancos de dados. Contém uma linha para cada índice ou estatísticas de tabelas e exibições indexadas<br /><br /> Observação: Cada índice (exceto o heap) é associado uma estatística que tem o mesmo nome que o índice.|  
|**sys.sysiscols**|Existe em todos os bancos de dados. Contém uma linha para cada índice persistente e coluna de estatísticas.|  
|**sys.sysscalartypes**|Existe em todos os bancos de dados. Contém uma linha para cada tipo definido pelo usuário ou sistema.|  
|**sys.sysdbreg**|Existe o **mestre** somente de banco de dados. Contém uma linha para cada banco de dados registrado.|  
|**sys.sysxsrvs**|Existe o **mestre** somente de banco de dados. Contém uma linha para cada servidor local, vinculado ou remoto.|  
|**sys.sysrmtlgns**|Esta tabela do sistema base existe no **mestre** somente de banco de dados. Contém uma linha para cada mapeamento de logon remoto. Isso é usado para mapear logons que dizem estar vindo de um servidor correspondente para um logon local real.|  
|**sys.syslnklgns**|Existe o **mestre** somente de banco de dados. Contém uma linha para cada mapeamento de logon vinculado. Mapeamentos de logon vinculados são usados por chamadas remotas de procedimento e consultas distribuídas que vão de um servidor local para um servidor vinculado correspondente.|  
|**sys.sysxlgns**|Existe o **mestre** somente de banco de dados. Contém uma linha para cada principal de servidor.|  
|**sys.sysdbfiles**|Existe em todos os bancos de dados. Se a coluna **dbid** for zero, a linha representa um arquivo que pertence a esse banco de dados. No **mestre** banco de dados, a coluna **dbid** pode ser diferente de zero. Quando esse for o caso, a linha representa um arquivo mestre.|  
|**sys.sysusermsg**|Existe o **mestre** somente de banco de dados. Cada linha representa uma mensagem de erro definida pelo usuário.|  
|**sys.sysprivs**|Existe em todos os bancos de dados. Contém uma linha para cada banco de dados - ou permissão em nível do servidor.<br /><br /> Observação: Permissões de nível de servidor são armazenadas no **mestre** banco de dados.|  
|**sys.sysowners**|Existe em todos os bancos de dados. Cada linha representa um principal de banco de dados.|  
|**sys.sysobjkeycrypts**|Existe em todos os bancos de dados. Contém uma linha para cada chave simétrica, criptografia ou propriedade criptográfica associada a um objeto.|  
|**sys.syscerts**|Existe em todos os bancos de dados. Contém uma linha para cada certificado em um banco de dados.|  
|**sys.sysasymkeys**|Existe em todos os bancos de dados. Cada linha representa uma chave assimétrica.|  
|**sys.ftinds**|Existe em todos os bancos de dados. Contém uma linha para cada índice de texto completo no banco de dados.|  
|**sys.sysxprops**|Existe em todos os bancos de dados. Contém uma linha para cada propriedade estendida.|  
|**sys.sysallocunits**|Existe em todos os bancos de dados. Contém uma linha para cada unidade de alocação de armazenamento.|  
|**sys.sysrowsets**|Existe em todos os bancos de dados. Contém uma linha para cada conjunto de linhas de partição para um índice ou um heap.|  
|**sys.sysrowsetrefs**|Existe em todos os bancos de dados. Contém uma linha para cada índice para referência de conjunto de linhas.|  
|**sys.syslogshippers**|Existe o **mestre** somente de banco de dados. Contém uma linha para cada banco de dados de testemunha espelhada.|  
|**sys.sysremsvcbinds**|Existe em todos os bancos de dados. Contém uma linha para cada associação de serviço remoto.|  
|**sys.sysconvgroup**|Existe em todos os bancos de dados. Contém uma linha para cada instância de serviço no Service Broker.|  
|**sys.sysxmitqueue**|Existe em todos os bancos de dados. Contém uma linha para cada fila de transmissão do Service Broker.|  
|**sys.sysdesend**|Existe em todos os bancos de dados. Contém uma linha para cada ponto de extremidade de envio de uma conversa do Service Broker.|  
|**sys.sysdercv**|Existe em todos os bancos de dados. Contém uma linha para cada ponto de extremidade de recebimento de uma conversa do Service Broker.|  
|**sys.sysendpts**|Existe o **mestre** somente de banco de dados. Contém uma linha para cada ponto de extremidade criado no servidor.|  
|**sys.syswebmethods**|Existe o **mestre** somente de banco de dados. Contém uma linha para cada método SOAP definido em um ponto de extremidade HTTP habilitado por SOAP criado no servidor.|  
|**sys.sysqnames**|Existe em todos os bancos de dados. Contém uma linha para cada namespace ou nome qualificado para um token de ID de 4 bytes.|  
|**sys.sysxmlcomponent**|Existe em todos os bancos de dados. Cada linha representa um componente de esquema XML.|  
|**sys.sysxmlfacet**|Existe em todos os bancos de dados. Contém uma linha para cada faceta XML (restrição) de definição de tipo XML.|  
|**sys.sysxmlplacement**|Existe em todos os bancos de dados. Contém uma linha para cada colocação XML de componentes XML.|  
|**sys.syssingleobjrefs**|Existe em todos os bancos de dados. Contém uma linha para cada referência geral N-a-1.|  
|**sys.sysmultiobjrefs**|Existe em todos os bancos de dados. Contém uma linha para cada referência geral N-a-N.|  
|**sys.sysobjvalues**|Existe em todos os bancos de dados. Contém uma linha para cada propriedade de valor geral de uma entidade.|  
|**sys.sysguidrefs**|Existe em todos os bancos de dados. Contém uma linha para cada referência de ID classificada por GUID.|  
  
  
