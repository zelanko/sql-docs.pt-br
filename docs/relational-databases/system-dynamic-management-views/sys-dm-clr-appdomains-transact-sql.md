---
title: sys.DM clr_appdomains (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
caps.latest.revision: 24
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 80fb9b49b7750d03ace2646af069284b9ff9875b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmclrappdomains-transact-sql"></a>sys.dm_clr_appdomains (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna uma linha para cada domínio de aplicativo no servidor. Domínio de aplicativo (**AppDomain**) é uma construção no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] common language runtime (CLR) que é a unidade de isolamento para um aplicativo. Você pode usar esta exibição para entender e solucionar problemas de objetos de integração de CLR que estão em execução no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Há vários tipos de objetos de banco de dados gerenciados de integração CLR. Para obter informações gerais sobre esses objetos, consulte [criando objetos de banco de dados com integração de Common Language Runtime (CLR)](../../relational-databases/clr-integration/database-objects/building-database-objects-with-common-language-runtime-clr-integration.md). Sempre que esses objetos são executados, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cria um **AppDomain** sob o qual ele pode carregar e executar o código exigido. O nível de isolamento para um **AppDomain** é um **AppDomain** por banco de dados por proprietário. Ou seja, todos os objetos de propriedade de um usuário são sempre executados no mesmo **AppDomain** por banco de dados (se um usuário registra objetos de banco de dados CLR em bancos de dados diferentes, o banco de dados CLR objetos serão executado em diferentes domínios de aplicativo). Um **AppDomain** não é destruído depois que o código de conclusão da execução. Em vez disso, ele é colocado na memória para execuções futuras. Isso melhora o desempenho.  
  
 Para obter mais informações, consulte [domínios de aplicativo](http://go.microsoft.com/fwlink/p/?LinkId=299658).  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**appdomain_address**|**varbinary(8)**|Endereço do **AppDomain**. Banco de dados gerenciado todos os objetos pertencentes a um usuário são sempre carregados no mesmo **AppDomain**. Você pode usar essa coluna para pesquisar todos os assemblies carregados no momento neste **AppDomain** na **sys.DM clr_loaded_assemblies**.|  
|**appdomain_id**|**Int**|ID do **AppDomain**. Cada **AppDomain** tem uma ID exclusiva.|  
|**appdomain_name**|**varchar(386)**|Nome do **AppDomain** conforme atribuído pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**creation_time**|**datetime**|Hora em que o **AppDomain** foi criado. Porque **AppDomains** são armazenadas em cache e reutilizado para melhor desempenho, **creation_time** não é necessariamente a hora em que o código foi executado.|  
|**db_id**|**Int**|ID do banco de dados no qual este **AppDomain** foi criado. Código armazenado em dois bancos de dados diferentes não pode compartilhar um **AppDomain**.|  
|**user_id**|**Int**|ID do usuário cujos objetos podem ser executados neste **AppDomain**.|  
|**state**|**nvarchar(128)**|Um descritor para o estado atual do **AppDomain**. Um AppDomain pode estar em estados diferentes, da criação até a exclusão. Consulte a seção Comentários deste tópico para obter mais informações.|  
|**strong_refcount**|**Int**|Número de referências fortes para este **AppDomain**. Isso reflete o número de lotes executados atualmente que usam **AppDomain**. Observe que a execução dessa exibição criará uma **strong refcount**; mesmo se nenhum código em execução, **strong_refcount** terá um valor de 1.|  
|**weak_refcount**|**Int**|Número de referências fracas para este **AppDomain**. Isso indica quantos objetos dentro do **AppDomain** são armazenados em cache. Quando você executa um objeto de banco de dados gerenciado, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] armazena em cache dentro de **AppDomain** para reutilização futura. Isso melhora o desempenho.|  
|**cost**|**Int**|Custo de **AppDomain**. Quanto maior o custo, maior a probabilidade isso **AppDomain** seja descarregado sob pressão de memória. Custo normalmente depende de quanta memória é necessária para recriar esse **AppDomain**.|  
|**value**|**Int**|O valor da **AppDomain**. Quanto menor o valor, maior a probabilidade isso **AppDomain** seja descarregado sob pressão de memória. Valor normalmente depende de quantas conexões ou lotes estão usando esse **AppDomain**.|  
|**total_processor_time_ms**|**bigint**|Tempo total do processador, em milissegundos, usado por todos os threads em execução no domínio do aplicativo atual desde que o processo foi iniciado. Isso é equivalente a **System.AppDomain.MonitoringTotalProcessorTime**.|  
|**total_allocated_memory_kb**|**bigint**|Tamanho total, em quilobytes, de todas as alocações de memória que foram feitas pelo domínio do aplicativo desde que foi criado, sem subtrair a memória coletada. Isso é equivalente a **System.AppDomain.MonitoringTotalAllocatedMemorySize**.|  
|**survived_memory_kb**|**bigint**|Número de quilobytes que sobreviveram a última coleção de bloqueio completa e que são conhecidos por serem referenciados pelo domínio do aplicativo atual. Isso é equivalente a **System.AppDomain.MonitoringSurvivedMemorySize**.|  
  
## <a name="remarks"></a>Remarks  
 Há uma relação um para muitos entre **dm_clr_appdomains** e **dm_clr_appdomains**.  
  
 As tabelas a seguir listam possíveis **estado** valores, suas descrições e quando ocorrem no **AppDomain** ciclo de vida. Você pode usar essas informações a seguir o ciclo de vida de um **AppDomain** e observar suspeitas ou repetidas **AppDomain** instâncias descarregar, sem a necessidade de analisar o Log de eventos do Windows.  
  
## <a name="appdomain-initialization"></a>Inicialização de AppDomain  
  
|Estado|Description|  
|-----------|-----------------|  
|E_APPDOMAIN_CREATING|O **AppDomain** está sendo criado.|  
  
## <a name="appdomain-usage"></a>Uso de AppDomain  
  
|Estado|Description|  
|-----------|-----------------|  
|E_APPDOMAIN_SHARED|O tempo de execução **AppDomain** está pronto para uso por vários usuários.|  
|E_APPDOMAIN_SINGLEUSER|O **AppDomain** está pronto para uso em operações de DDL. Estes diferem de E_APPDOMAIN_SHARED porque os AppDomains compartilhados são usados para execuções de integração de CLR em vez de operações DDL. Esses AppDomains são isolados de outras operações simultâneas.|  
|E_APPDOMAIN_DOOMED|O **AppDomain** está programado para ser descarregado, mas há threads de execução.|  
  
## <a name="appdomain-cleanup"></a>Limpeza de AppDomain  
  
|Estado|Description|  
|-----------|-----------------|  
|E_APPDOMAIN_UNLOADING|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] solicitou que o CLR descarregue o **AppDomain**, normalmente porque o assembly que contém os objetos de banco de dados gerenciados foi alterado ou descartado.|  
|E_APPDOMAIN_UNLOADED|O CLR descarregou o **AppDomain**. Isso é geralmente o resultado de um procedimento de escalonamento devido a **ThreadAbort**, **OutOfMemory**, ou uma exceção sem tratamento no código do usuário.|  
|E_APPDOMAIN_ENQUEUE_DESTROY|O **AppDomain** foi descarregado em CLR e configurado para ser destruído pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|E_APPDOMAIN_DESTROY|O **AppDomain** está no processo de destruição por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|E_APPDOMAIN_ZOMBIE|O **AppDomain** foi destruído por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]; no entanto, nem todas as referências para o **AppDomain** foram limpos.|  
  
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
  
## <a name="see-also"></a>Consulte também  
 [sys.dm_clr_loaded_assemblies &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-clr-loaded-assemblies-transact-sql.md)   
 [Exibições de gerenciamento dinâmico de relacionados do Common Language Runtime &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/common-language-runtime-related-dynamic-management-views-transact-sql.md)  
  
  
