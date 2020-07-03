---
title: sys. dm_clr_appdomains (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_clr_appdomains
- sys.dm_clr_appdomains
- dm_clr_appdomains_TSQL
- sys.dm_clr_appdomains_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_clr_appdomains dynamic management dynamic management view
ms.assetid: 9fe0d4fd-950a-4274-a493-85e776278045
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 2c3c0351bd541738e2540cc1a0624cf0ca9836c5
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85893981"
---
# <a name="sysdm_clr_appdomains-transact-sql"></a>sys.dm_clr_appdomains (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Retorna uma linha para cada domínio de aplicativo no servidor. O**AppDomain**(domínio do aplicativo) é um constructo no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] Common Language Runtime (CLR) que é a unidade de isolamento de um aplicativo. Você pode usar essa exibição para entender e solucionar problemas dos objetos de integração CLR que estão sendo executados no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Há vários tipos de objetos de banco de dados gerenciados de integração CLR. Para obter informações gerais sobre esses objetos, consulte [criando objetos de banco de dados com integração CLR (Common Language Runtime)](../../relational-databases/clr-integration/database-objects/building-database-objects-with-common-language-runtime-clr-integration.md). Sempre que esses objetos são executados, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o cria um **AppDomain** sob o qual ele pode carregar e executar o código necessário. O nível de isolamento para um **AppDomain** é um **AppDomain** por banco de dados por proprietário. Ou seja, todos os objetos CLR pertencentes a um usuário são sempre executados no mesmo **AppDomain** por banco de dados (se um usuário registrar objetos de banco de dados CLR em diferentes bancos de dados, os objetos de banco de dados CLR serão executados em domínios de aplicativo diferentes). Um **AppDomain** não é destruído depois que o código conclui a execução. Em vez disso, ele é colocado na memória para execuções futuras. Isso melhora o desempenho.  
  
 Para obter mais informações, consulte [domínios de aplicativo](https://go.microsoft.com/fwlink/p/?LinkId=299658).  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**appdomain_address**|**varbinary (8)**|Endereço do **AppDomain**. Todos os objetos de banco de dados gerenciados pertencentes a um usuário são sempre carregados no mesmo **AppDomain**. Você pode usar esta coluna para pesquisar todos os assemblies carregados atualmente neste **AppDomain** em **Sys. dm_clr_loaded_assemblies**.|  
|**appdomain_id**|**int**|ID do **AppDomain**. Cada **AppDomain** tem uma ID exclusiva.|  
|**appdomain_name**|**varchar (386)**|Nome do **AppDomain** como atribuído por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|**creation_time**|**datetime**|Hora em que o **AppDomain** foi criado. Como os **AppDomains** são armazenados em cache e reutilizados para melhorar o desempenho, **CREATION_TIME** não é necessariamente o momento em que o código foi executado.|  
|**db_id**|**int**|ID do banco de dados no qual este **AppDomain** foi criado. O código armazenado em dois bancos de dados diferentes não pode compartilhar um **AppDomain**.|  
|**user_id**|**int**|ID do usuário cujos objetos podem ser executados neste **AppDomain**.|  
|**state**|**nvarchar(128)**|Um descritor para o estado atual do **AppDomain**. Um AppDomain pode estar em estados diferentes, da criação até a exclusão. Consulte a seção Comentários deste tópico para obter mais informações.|  
|**strong_refcount**|**int**|Número de referências fortes a este **AppDomain**. Isso reflete o número de lotes em execução no momento que usam este **AppDomain**. Observe que a execução dessa exibição criará um **Refcount forte**; mesmo que não haja nenhum código em execução no momento, **strong_refcount** terá um valor de 1.|  
|**weak_refcount**|**int**|Número de referências fracas a este **AppDomain**. Isso indica quantos objetos dentro do **AppDomain** são armazenados em cache. Quando você executa um objeto de banco de dados gerenciado, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] armazena em cache dentro do **AppDomain** para reutilização futura. Isso melhora o desempenho.|  
|**cost**|**int**|Custo do **AppDomain**. Quanto maior o custo, mais provável que esse **AppDomain** seja descarregado sob pressão de memória. Geralmente, o custo depende da quantidade de memória necessária para recriar esse **AppDomain**.|  
|**value**|**int**|Valor do **AppDomain**. Quanto menor o valor, mais provável que esse **AppDomain** seja descarregado sob pressão de memória. Geralmente, o valor depende de quantas conexões ou lotes estão usando esse **AppDomain**.|  
|**total_processor_time_ms**|**bigint**|Tempo total do processador, em milissegundos, usado por todos os threads em execução no domínio do aplicativo atual desde que o processo foi iniciado. Isso é equivalente a **System. AppDomain. MonitoringTotalProcessorTime**.|  
|**total_allocated_memory_kb**|**bigint**|Tamanho total, em quilobytes, de todas as alocações de memória que foram feitas pelo domínio do aplicativo desde que foi criado, sem subtrair a memória coletada. Isso é equivalente a **System. AppDomain. MonitoringTotalAllocatedMemorySize**.|  
|**survived_memory_kb**|**bigint**|Número de quilobytes que sobreviveram a última coleção de bloqueio completa e que são conhecidos por serem referenciados pelo domínio do aplicativo atual. Isso é equivalente a **System. AppDomain. MonitoringSurvivedMemorySize**.|  
  
## <a name="remarks"></a>Comentários  
 Há uma relação um-para-um entre **dm_clr_appdomains. appdomain_address** e **dm_clr_loaded_assemblies. appdomain_address**.  
  
 As tabelas a seguir listam possíveis valores de **estado** , suas descrições e quando ocorrem no ciclo de vida do **AppDomain** . Você pode usar essas informações para seguir o Lifecyle de um **AppDomain** e para observar a descarregamento de instâncias **AppDomain** suspeitas ou repetitivas, sem precisar analisar o log de eventos do Windows.  
  
## <a name="appdomain-initialization"></a>Inicialização de AppDomain  
  
|Estado|Descrição|  
|-----------|-----------------|  
|E_APPDOMAIN_CREATING|O **AppDomain** está sendo criado.|  
  
## <a name="appdomain-usage"></a>Uso de AppDomain  
  
|Estado|Descrição|  
|-----------|-----------------|  
|E_APPDOMAIN_SHARED|O **AppDomain** de tempo de execução está pronto para ser usado por vários usuários.|  
|E_APPDOMAIN_SINGLEUSER|O **AppDomain** está pronto para uso em operações DDL. Estes diferem de E_APPDOMAIN_SHARED porque os AppDomains compartilhados são usados para execuções de integração de CLR em vez de operações DDL. Esses AppDomains são isolados de outras operações simultâneas.|  
|E_APPDOMAIN_DOOMED|O **AppDomain** está agendado para ser descarregado, mas há threads sendo executados nele.|  
  
## <a name="appdomain-cleanup"></a>Limpeza de AppDomain  
  
|Estado|Descrição|  
|-----------|-----------------|  
|E_APPDOMAIN_UNLOADING|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]solicitou que o CLR descarrega o **AppDomain**, geralmente porque o assembly que contém os objetos de banco de dados gerenciado foi alterado ou descartado.|  
|E_APPDOMAIN_UNLOADED|O CLR descarregou o **AppDomain**. Normalmente, isso é o resultado de um procedimento de escalonamento devido à **ThreadAbortException**, à **OutOfMemory**ou a uma exceção sem tratamento no código do usuário.|  
|E_APPDOMAIN_ENQUEUE_DESTROY|O **AppDomain** foi descarregado no CLR e foi definido para ser destruído pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|E_APPDOMAIN_DESTROY|O **AppDomain** está no processo de ser destruído pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|E_APPDOMAIN_ZOMBIE|O **AppDomain** foi destruído por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ; no entanto, nem todas as referências ao **AppDomain** foram limpas.|  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão VIEW SERVER STAT no banco de dados.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir mostra como exibir os detalhes de um **AppDomain** para um determinado assembly:  
  
```  
select appdomain_id, creation_time, db_id, user_id, state  
from sys.dm_clr_appdomains a  
where appdomain_address =   
(select appdomain_address   
 from sys.dm_clr_loaded_assemblies  
   where assembly_id = 500);  
```  
  
 O exemplo a seguir mostra como exibir todos os assemblies em um determinado **AppDomain**:  
  
```  
select a.name, a.assembly_id, a.permission_set_desc, a.is_visible, a.create_date, l.load_time   
from sys.dm_clr_loaded_assemblies as l   
inner join sys.assemblies as a  
on l.assembly_id = a.assembly_id  
where l.appdomain_address =   
(select appdomain_address   
from sys.dm_clr_appdomains  
where appdomain_id = 15);  
```  
  
## <a name="see-also"></a>Consulte Também  
 [sys. dm_clr_loaded_assemblies &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-clr-loaded-assemblies-transact-sql.md)   
 [Exibições de gerenciamento dinâmico relacionadas ao Common Language Runtime &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/common-language-runtime-related-dynamic-management-views-transact-sql.md)  
  
  
