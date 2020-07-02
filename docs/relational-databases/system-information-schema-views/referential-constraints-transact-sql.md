---
title: REFERENTIAL_CONSTRAINTS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- REFERENTIAL_CONSTRAINTS
- REFERENTIAL_CONSTRAINTS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- INFORMATION_SCHEMA.REFERENTIAL_CONSTRAINTS view
- REFERENTIAL_CONSTRAINTS view
ms.assetid: 5d358f18-0a85-4b55-af4b-98d5f4cd1020
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 89f9db258d03c44452fc05701b25f56a972fe54e
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85784860"
---
# <a name="referential_constraints-transact-sql"></a>REFERENTIAL_CONSTRAINTS (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Retorna uma fila para cada restrição FOREIGN KEY no banco de dados atual. Esta exibição de esquema de informações retorna informações sobre os objetos para os quais o usuário atual tem permissões.  
  
 Para recuperar informações dessas exibições, especifique o nome totalmente qualificado de **INFORMATION_SCHEMA.** _view_name_.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**CONSTRAINT_CATALOG**|**nvarchar (** 128 **)**|Qualificador da restrição.|  
|**CONSTRAINT_SCHEMA**|**nvarchar (** 128 **)**|Nome do esquema que contém a restrição.<br /><br /> **&#42;&#42; importantes &#42;&#42;** Não use INFORMATION_SCHEMA exibições para determinar o esquema de um objeto. INFORMATION_SCHEMA exibições representam apenas um subconjunto dos metadados de um objeto. O único modo seguro de localizar o esquema de um objeto é consultar a exibição de catálogo sys.objects.|  
|**CONSTRAINT_NAME**|**sysname**|Nome da restrição.|  
|**UNIQUE_CONSTRAINT_CATALOG**|**nvarchar (** 128 **)**|Qualificador de restrição UNIQUE.|  
|**UNIQUE_CONSTRAINT_SCHEMA**|**nvarchar (** 128 **)**|Nome do esquema que contém a restrição UNIQUE.<br /><br /> **&#42;&#42; importantes &#42;&#42;** Não use INFORMATION_SCHEMA exibições para determinar o esquema de um objeto. INFORMATION_SCHEMA exibições representam apenas um subconjunto dos metadados de um objeto. O único modo seguro de localizar o esquema de um objeto é consultar a exibição de catálogo sys.objects.|  
|**UNIQUE_CONSTRAINT_NAME**|**sysname**|Restrição UNIQUE.|  
|**MATCH_OPTION**|**varchar (** 7 **)**|Condições de correspondência de restrição referenciais. Sempre retorna SIMPLE. Isso significa que nenhuma correspondência está definida. A condição é considerada uma correspondência quando uma das seguintes condições for verdadeira:<br /><br /> Pelo menos um valor na coluna de chave estrangeira é NULL.<br /><br /> Todos os valores na coluna de chave estrangeira não são NULL e há uma linha na tabela de chave primária que tem a mesma chave.|  
|**UPDATE_RULE**|**varchar (** 11 **)**|Ação tomada quando uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] viola a integridade referencial definida por esta restrição. Retorna uma destas opções: <br />NO ACTION<br />CASCADE<br />SET NULL<br />SET DEFAULT<br /><br /> Se NO ACTION for especificado em ON UPDATE para esta restrição, a atualização da chave primária referenciada na restrição não será propagada para a chave estrangeira. Se essa atualização de uma chave primária causar uma violação de integridade referencial porque pelo menos uma chave estrangeira contém o mesmo valor, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não fará nenhuma alteração nas tabelas pai e de referência. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] também gerará um erro.<br /><br /> Se CASCADE for especificado em ON UPDATE para esta restrição, qualquer mudança para o valor de chave primária será propagado automaticamente para o valor da chave estrangeira.|  
|**DELETE_RULE**|**varchar (** 11 **)**|A ação tomada quando uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] viola a integridade referencial definida por esta restrição. Retorna uma destas opções: <br />NO ACTION<br />CASCADE<br />SET NULL<br />SET DEFAULT<br /><br /> Se NO ACTION for especificado em ON DELETE para essa restrição, a exclusão da chave primária referenciada na restrição não será propagada para a chave estrangeira. Se essa exclusão de uma chave primária causar uma violação de integridade referencial porque pelo menos uma chave estrangeira contém o mesmo valor, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não fará nenhuma alteração nas tabelas pai e de referência. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] também gerará um erro.<br /><br /> Se CASCADE for especificado em ON DELETE para esta restrição, qualquer mudança para o valor de chave primária será propagado automaticamente para o valor da chave estrangeira.|  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições do sistema &#40;&#41;Transact-SQL](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [Exibições do esquema de informações &#40;&#41;Transact-SQL](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys. Indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys. Objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys. foreign_keys &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-foreign-keys-transact-sql.md)  
  
  
