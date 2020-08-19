---
description: Write (Mecanismo de Banco de Dados)
title: Write (Mecanismo de Banco de Dados) | Microsoft Docs
ms.custom: ''
ms.date: 07/23/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- Write_TSQL
- Write
dev_langs:
- TSQL
helpviewer_keywords:
- Write [Database Engine]
ms.assetid: 7c554334-d2d9-4eae-a4ae-097aa4020e1a
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 08f593fc3123e6f99f3e44473d75101eacd406e7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88368072"
---
# <a name="write-database-engine"></a>Write (Mecanismo de Banco de Dados)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

O método Write grava uma representação binária de **SqlHierarchyId** no **BinaryWriter** passado. Não é possível chamar Write usando [!INCLUDE[tsql](../../includes/tsql-md.md)]. Em seu lugar, use CAST ou CONVERT.
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
void Write( BinaryWriter w )
```  

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
*w*  
Um objeto **BinaryWriter** no qual a representação binária deste nó **hierarchyid** será gravada.
  
## <a name="return-types"></a>Tipos de retorno  
**Tipo de retorno do CLR: nulo**
  
## <a name="remarks"></a>Comentários  
Write é usado internamente por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] quando necessário, como ao carregar dados de uma coluna **hierarchyid**. Write também é chamado internamente quando é feita uma conversão entre **hierarchyid** e **varbinary**.
  
## <a name="examples"></a>Exemplos  
  
```sql
MemoryStream stream = new MemoryStream();  
BinaryWriter bw = new BinaryWriter(stream);  
hid.Write(bw);  
byte[] encoding = stream.ToArray();  
  
```  
  
## <a name="see-also"></a>Confira também
[Read &#40;Mecanismo de Banco de Dados&#41;](../../t-sql/data-types/read-database-engine.md)  
[ToString &#40;Mecanismo de Banco de Dados&#41;](../../t-sql/data-types/tostring-database-engine.md)  
[CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[Referência de método de tipo de dados hierarchyid](https://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)
  
  
