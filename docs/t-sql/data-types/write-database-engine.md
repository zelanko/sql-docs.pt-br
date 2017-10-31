---
title: Write (mecanismo de banco de dados) | Microsoft Docs
ms.custom: 
ms.date: 7/23/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- Write_TSQL
- Write
dev_langs:
- TSQL
helpviewer_keywords:
- Write [Database Engine]
ms.assetid: 7c554334-d2d9-4eae-a4ae-097aa4020e1a
caps.latest.revision: 13
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 60707b57671c2ad607bd85b0fedececccd478038
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="write-database-engine"></a>Write (Mecanismo de Banco de Dados)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Gravar grava uma representação binária de **SqlHierarchyId** para transmitido **BinaryWriter**. Gravação não pode ser chamada usando [!INCLUDE[tsql](../../includes/tsql-md.md)]. Em seu lugar, use CAST ou CONVERT.
  
## <a name="syntax"></a>Sintaxe  
  
```sql
void Write( BinaryWriter w )   
```  
  
## <a name="arguments"></a>Argumentos  
*w*  
Um **BinaryWriter** objeto ao qual a representação binária desse **hierarchyid** nó será gravado.
  
## <a name="return-types"></a>Tipos de retorno  
**Tipo de retorno CLR: void**
  
## <a name="remarks"></a>Comentários  
Gravação é usada internamente pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] quando é necessário, por exemplo, ao carregar dados de um **hierarchyid** coluna. Gravação também é chamada internamente quando é feita uma conversão entre **hierarchyid** e **varbinary**.
  
## <a name="examples"></a>Exemplos  
  
```sql
MemoryStream stream = new MemoryStream();  
BinaryWriter bw = new BinaryWriter(stream);  
hid.Write(bw);  
byte[] encoding = stream.ToArray();  
  
```  
  
## <a name="see-also"></a>Consulte também
[Leitura &#40; mecanismo de banco de dados &#41;](../../t-sql/data-types/read-database-engine.md)  
[ToString &#40; mecanismo de banco de dados &#41;](../../t-sql/data-types/tostring-database-engine.md)  
[CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[Referência de método de tipo de dados hierarchyid](http://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)
  
  

