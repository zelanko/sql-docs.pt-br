---
title: sys. dm_clr_loaded_assemblies (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
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
author: stevestein
ms.author: sstein
ms.openlocfilehash: 1cd677e516048aa52badec7fc9875e5a5b13f25a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68138664"
---
# <a name="sysdm_clr_loaded_assemblies-transact-sql"></a>sys.dm_clr_loaded_assemblies (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna uma linha para cada assembly gerenciado pelo usuário, carregada no espaço de endereço do servidor. Use esta exibição para entender e solucionar problemas dos objetos de banco de dados gerenciados da integração CLR que estão sendo executados no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Assemblies são arquivos de código DLL gerenciados, usados para definir e implantar objetos de banco de dados gerenciados em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Sempre que um usuário executa um desses objetos de banco de dados gerenciados, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o CLR carregam o assembly (e suas referências) no qual o objeto de banco de dados gerenciado é definido. O assembly permanece carregado no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para aprimorar o desempenho, de forma que os objetos de banco de dados gerenciados contidos no assembly possam ser chamados no futuro sem a necessidade de recarregar o assembly. O assembly não é descarregado até que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sofra pressão de memória. Para obter mais informações sobre assemblies e integração CLR, consulte [ambiente hospedado do CLR](../../relational-databases/clr-integration/clr-integration-architecture-clr-hosted-environment.md). Para obter mais informações sobre objetos de banco de dados gerenciado, consulte [criando objetos de banco de dados com tempo de execução de linguagem comum &#40;integração de&#41; CLR](../../relational-databases/clr-integration/database-objects/building-database-objects-with-common-language-runtime-clr-integration.md).  

  
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|**assembly_id**|**int**|ID do assembly carregado. O **assembly_id** pode ser usado para pesquisar mais informações sobre o assembly na exibição de catálogo de [&#41;de assemblies &#40;Transact-SQL](../../relational-databases/system-catalog-views/sys-assemblies-transact-sql.md) . Observe que o [!INCLUDE[tsql](../../includes/tsql-md.md)] catálogo [Sys. assemblies](../../relational-databases/system-catalog-views/sys-assemblies-transact-sql.md) mostra os assemblies somente no banco de dados atual. A exibição **SQS. dm_clr_loaded_assemblies** mostra todos os assemblies carregados no servidor.|  
|**appdomain_address**|**int**|Endereço do domínio do aplicativo (**AppDomain**) no qual o assembly é carregado. Todos os assemblies pertencentes a um único usuário sempre são carregados no mesmo **AppDomain**. O **appdomain_address** pode ser usado para pesquisar mais informações sobre o **AppDomain** na exibição [Sys. dm_clr_appdomains](../../relational-databases/system-dynamic-management-views/sys-dm-clr-appdomains-transact-sql.md) .|  
|**load_time**|**datetime**|Hora em que o assembly foi carregado. Observe que o assembly permanece carregado até [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que esteja sob pressão de memória e descarregue o **AppDomain**. Você pode monitorar **load_time** para entender com que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] frequência a demanda de memória é descarregada e descarrega o **AppDomain**.|  
  
## <a name="permissions"></a>Permissões  
 , é necessário ter permissão VIEW SERVER STATE no servidor.  
  
## <a name="remarks"></a>Comentários  
 A exibição **dm_clr_loaded_assemblies. appdomain_address** tem uma relação muitos para um com **dm_clr_appdomains. appdomain_address**. A exibição **dm_clr_loaded_assemblies. assembly_id** tem uma relação um-para-muitos com **Sys. assemblies. assembly_id**.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir mostra como exibir detalhes de todos os assemblies no banco de dados atual atualmente carregados.  
  
```  
 SELECT a.name, a.assembly_id, a.permission_set_desc, a.is_visible, a.create_date, l.load_time   
FROM sys.dm_clr_loaded_assemblies AS l   
INNER JOIN sys.assemblies AS a  
ON l.assembly_id = a.assembly_id;  
```  
  
 O exemplo a seguir mostra como exibir detalhes do **AppDomain** no qual um determinado assembly é carregado.  
  
```  
SELECT appdomain_id, creation_time, db_id, user_id, state  
FROM sys.dm_clr_appdomains AS a  
WHERE appdomain_address =   
(SELECT appdomain_address   
 FROM sys.dm_clr_loaded_assemblies  
 WHERE assembly_id = 555);  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de gerenciamento dinâmico relacionadas ao Common Language Runtime &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/common-language-runtime-related-dynamic-management-views-transact-sql.md)  
  
  
