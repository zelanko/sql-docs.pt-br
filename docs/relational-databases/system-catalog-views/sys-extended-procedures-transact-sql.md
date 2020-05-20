---
title: sys. extended_procedures (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- extended_procedures
- sys.extended_procedures
- sys.extended_procedures_TSQL
- extended_procedures_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.extended_procedures catalog view
ms.assetid: 310e0f87-0044-4fdf-bd12-51a723a74ce6
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 42ecb7a4199bd42c6f522e447f260c37e3ba3368
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82831960"
---
# <a name="sysextended_procedures-transact-sql"></a>sys.extended_procedures (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém uma linha para cada objeto que é um procedimento armazenado estendido, com **Sys. Objects. Type** = X. Como os procedimentos armazenados estendidos são instalados no banco de dados **mestre** , eles ficam visíveis apenas desse contexto de banco de dados. A seleção da exibição **Sys. extended_procedures** em qualquer outro contexto de banco de dados retornará um conjunto de resultados vazio.  

  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**\<Colunas herdadas de sys. Objects>**||Para obter uma lista de colunas que essa exibição herda, consulte [Sys. objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md).|  
|**dll_name**|**nvarchar(260)**|Nome da DLL, incluindo caminho, para este procedimento armazenado estendido.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de catálogo de objetos &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
