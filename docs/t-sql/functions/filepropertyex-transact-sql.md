---
title: FILEPROPERTYEX (Transact-SQL) | Microsoft Docs
ms.date: 07/23/2019
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- FILEPROPERTYEX_TSQL
- FILEPROPERTYEX
dev_langs:
- TSQL
helpviewer_keywords:
- viewing file properties
- displaying file properties
- file properties [SQL Server]
- FILEPROPERTYEX function
- file names [SQL Server], FILEPROPERTYEX
author: stevestein
ms.author: sstein
ms.openlocfilehash: d0eb763436bc4dd26815879c33c9a8461d9a38d7
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85732320"
---
# <a name="filepropertyex-transact-sql"></a>FILEPROPERTYEX (Transact-SQL)
[!INCLUDE[Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/asdb-asdbmi.md)]

  Retorna o valor da propriedade do arquivo estendido especificado quando são especificados um nome de arquivo no banco de dados atual e um nome de propriedade. Retorna NULL para arquivos que não estão no banco de dados atual ou para propriedades de arquivo estendido que não existem. Atualmente, as propriedades de arquivo estendido se aplicam somente a bancos de dados que estão no Armazenamento de Blobs do Azure.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
FILEPROPERTYEX ( name , property )  
```  
  
## <a name="arguments"></a>Argumentos  
 *name*  
 É uma expressão que contém o nome do arquivo associado ao banco de dados atual para o qual retornar as informações de propriedade. *file_name* é **nchar(128)** .  
  
 *property*  
 É uma expressão que contém o nome da propriedade do arquivo a ser retornada. *property* é **varchar(128)** e pode ser um dos valores a seguir.  


  
|Valor|DESCRIÇÃO|
|-----------|-----------------|  
|**BlobTier**|O nível do blob de páginas do Azure de destino. Aplica-se somente aos bancos de dados Standard e GeneralPurpose que usam o Armazenamento de Blobs de páginas do Azure.|
|**AccountType**|O tipo de conta de armazenamento que indica se o Armazenamento é de Blobs ou de arquivos e se é um armazenamento Premium ou Standard.|
|**IsInferredTier**|Indica se o nível é camada implícito (inferido) que pode aumentar com o tamanho dos dados ou um nível explícito (fixo).|
|**IsPageBlob**|Indica se o blob de destino é um blob de páginas ou não.|
  
## <a name="return-types"></a>Tipos de retorno  
 **sql_variant**  
  
## <a name="remarks"></a>Comentários  
 *file_name* corresponde à coluna **name** da exibição do catálogo **sys.master_files** ou **sys.database_files**.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna a configuração para arquivos de banco de dados:
```sql
SELECT s.file_id,
       s.type_desc,
       s.name,
       FILEPROPERTYEX(s.name, 'BlobTier') AS BlobTier,
       FILEPROPERTYEX(s.name, 'AccountType') AS AccountType,
       FILEPROPERTYEX(s.name, 'IsInferredTier') AS IsInferredTier,
       FILEPROPERTYEX(s.name, 'IsPageBlob') AS IsPageBlob
FROM sys.database_files AS s
WHERE s.type_desc IN ('ROWS', 'LOG');
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
file_id  type_desc  name  BlobTier  AccountType  IsInferredTier  IsPageBlob
--------------------------------------------------------------------------------------
1     ROWS      data_0  P30  PremiumBlobStorage  0   1
2     LOG       log     P30  PremiumBlobStorage  0   1

(2 rows affected)
```  
  
## <a name="see-also"></a>Consulte Também  
 [FILEGROUPPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/filegroupproperty-transact-sql.md)   
 [Funções de metadados &#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [sp_spaceused &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
  
  
