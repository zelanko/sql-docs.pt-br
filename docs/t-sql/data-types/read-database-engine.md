---
title: Leitura (mecanismo de banco de dados) | Microsoft Docs
ms.custom: 
ms.date: 7/22/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|data-types
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- Read_TSQL
- Read
dev_langs:
- TSQL
helpviewer_keywords:
- Read [Database Engine]
ms.assetid: f2b8207c-b69f-4327-a874-100b3a1f27d8
caps.latest.revision: 13
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 21f27c627a36f747d9e3ecbb52d14d1ac6bc5d28
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="read-database-engine"></a>Read (Mecanismo de Banco de Dados)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Leitura lê a representação binária de **SqlHierarchyId** do passado **BinaryReader** e define o **SqlHierarchyId** objeto para esse valor. Leitura não pode ser chamada usando [!INCLUDE[tsql](../../includes/tsql-md.md)]. Em seu lugar, use CAST ou CONVERT.
  
## <a name="syntax"></a>Sintaxe  
  
```sql
void Read( BinaryReader r )   
```  
  
## <a name="arguments"></a>Argumentos  
*r*  
 O **BinaryReader** objeto que gera um fluxo binário correspondente a uma representação binária de um **hierarchyid** nó.  
  
## <a name="return-types"></a>Tipos de retorno
 **Tipo de retorno CLR: void**  
  
## <a name="remarks"></a>Comentários  
 Leitura não valida sua entrada. Se uma entrada binária inválida for fornecida, leitura pode gerar uma exceção. Ou, ele pode ser bem-sucedida e produzir um inválido **SqlHierarchyId** objeto cujos métodos podem gerar resultados inesperados ou gerar uma exceção.  
  
 Leitura só pode ser chamada em um recém-criado **SqlHierarchyId** objeto.  
  
 Leitura é usada internamente pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] quando for necessário, como ao gravar dados **hierarchyid** coluna. Leitura também é chamada internamente quando é feita uma conversão entre **varbinary** e **hierarchyid**.  
  
## <a name="examples"></a>Exemplos  
  
```sql
Byte[] encoding = new byte[] { 0x58 };  
MemoryStream stream = new MemoryStream(encoding, false /*not writable*/);  
BinaryReader br = new BinaryReader(stream);  
SqlHierarchyId hid = new SqlHierarchyId();  
hid.Read(br);   
```  
  
## <a name="see-also"></a>Consulte também  
[Gravar &#40; mecanismo de banco de dados &#41;](../../t-sql/data-types/write-database-engine.md)  
[ToString &#40; mecanismo de banco de dados &#41;](../../t-sql/data-types/tostring-database-engine.md)  
[CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[Referência de método de tipo de dados hierarchyid](http://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)
  
  

