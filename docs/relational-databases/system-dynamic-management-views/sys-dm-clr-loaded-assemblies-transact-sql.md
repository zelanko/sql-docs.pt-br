---
title: sys.DM clr_loaded_assemblies (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_clr_loaded_assemblies
- sys.dm_clr_loaded_assemblies_TSQL
- dm_clr_loaded_assemblies_TSQL
- sys.dm_clr_loaded_assemblies
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_clr_loaded_assemblies dynamic management view
ms.assetid: 8523d8db-d8a0-4b1f-ae19-6705d633e0a6
caps.latest.revision: 22
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5670bba30bc3d110d362e36c2ee27180ea18847b
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="sysdmclrloadedassemblies-transact-sql"></a>sys.dm_clr_loaded_assemblies (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna uma linha para cada assembly gerenciado pelo usuário, carregada no espaço de endereço do servidor. Use esta exibição para entender e solucionar problemas da integração de CLR gerenciado objetos de banco de dados que estão sendo executados em [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Assemblies são arquivos de código DLL gerenciados, usados para definir e implantar objetos de banco de dados gerenciados em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Sempre que um usuário executa um desses objetos de banco de dados gerenciados, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o CLR carregam o assembly (e suas referências) no qual o objeto de banco de dados gerenciado é definido. O assembly permanece carregado no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para aprimorar o desempenho, de forma que os objetos de banco de dados gerenciados contidos no assembly possam ser chamados no futuro sem a necessidade de recarregar o assembly. O assembly não é descarregado até que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sofra pressão de memória. Para obter mais informações sobre assemblies de integração CLR, consulte [ambiente hospedado pelo CLR](../../relational-databases/clr-integration/clr-integration-architecture-clr-hosted-environment.md). Para obter mais informações sobre objetos de banco de dados gerenciados, consulte [criando objetos de banco de dados com o Common Language Runtime &#40;CLR&#41; integração](../../relational-databases/clr-integration/database-objects/building-database-objects-with-common-language-runtime-clr-integration.md).  

  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**assembly_id**|**Int**|ID do assembly carregado. O **assembly_id** pode ser usado para consultar mais informações sobre o assembly no [sys &#40;Transact-SQL&#41; ](../../relational-databases/system-catalog-views/sys-assemblies-transact-sql.md) exibição do catálogo. Observe que o [!INCLUDE[tsql](../../includes/tsql-md.md)] [sys](../../relational-databases/system-catalog-views/sys-assemblies-transact-sql.md) catálogo mostra os assemblies de banco de dados atual. O **sqs.dm_clr_loaded_assemblies** exibição mostra todos os assemblies carregados no servidor.|  
|**appdomain_address**|**Int**|Endereço do domínio do aplicativo (**AppDomain**) no qual o assembly é carregado. Todos os assemblies de propriedade de um único usuário são sempre carregados no mesmo **AppDomain**. O **appdomain_address** pode ser usado para pesquisar mais informações sobre o **AppDomain** no [sys.DM clr_appdomains](../../relational-databases/system-dynamic-management-views/sys-dm-clr-appdomains-transact-sql.md) exibição.|  
|**load_time**|**datetime**|Hora em que o assembly foi carregado. Observe que o assembly permanece carregado até [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está sob pressão de memória e descarrega o **AppDomain**. Você pode monitorar **load_time** para entender com que frequência [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vem sob pressão de memória e descarrega o **AppDomain**.|  
  
## <a name="permissions"></a>Permissões  
 , é necessário ter permissão VIEW SERVER STATE no servidor.  
  
## <a name="remarks"></a>Remarks  
 O **dm_clr_appdomains** exibição tem uma relação muitos-para-um com **dm_clr_appdomains**. O **dm_clr_loaded_assemblies** exibição tem uma relação um-para-muitos com **assembly_id**.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir mostra como exibir detalhes de todos os assemblies no banco de dados atual atualmente carregados.  
  
```  
 SELECT a.name, a.assembly_id, a.permission_set_desc, a.is_visible, a.create_date, l.load_time   
FROM sys.dm_clr_loaded_assemblies AS l   
INNER JOIN sys.assemblies AS a  
ON l.assembly_id = a.assembly_id;  
```  
  
 O exemplo a seguir mostra como exibir detalhes do **AppDomain** no qual um determinado assembly está carregado.  
  
```  
SELECT appdomain_id, creation_time, db_id, user_id, state  
FROM sys.dm_clr_appdomains AS a  
WHERE appdomain_address =   
(SELECT appdomain_address   
 FROM sys.dm_clr_loaded_assemblies  
 WHERE assembly_id = 555);  
```  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de gerenciamento dinâmico de relacionados do Common Language Runtime &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/common-language-runtime-related-dynamic-management-views-transact-sql.md)  
  
  
