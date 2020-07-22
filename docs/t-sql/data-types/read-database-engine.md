---
title: Read (Mecanismo de Banco de Dados) | Microsoft Docs
ms.custom: ''
ms.date: 04/16/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- Read_TSQL
- Read
dev_langs:
- TSQL
helpviewer_keywords:
- Read [Database Engine]
ms.assetid: f2b8207c-b69f-4327-a874-100b3a1f27d8
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 89739f7e53ddccfc95cb9e84311f1ed18e147de6
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/21/2020
ms.locfileid: "86552581"
---
# <a name="read-database-engine-by-using-csharp"></a>Leia o (Mecanismo de Banco de Dados) usando o CSharp
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

O método Read lê a representação binária de **SqlHierarchyId** do **BinaryReader** passado e define o objeto **SqlHierarchyId** com esse valor. Não é possível chamar Read usando [!INCLUDE[tsql](../../includes/tsql-md.md)]. Em seu lugar, use CAST ou CONVERT.
  
## <a name="syntax"></a>Sintaxe  

<!--
This is not T-SQL, despite the ```sql colorizer specified.
Neither should this be ```syntaxsql.
Rather, this is C# (or C# syntax).  Same for the later code blocks.
I am making this fix now, from ```sql to ```cs, on 2020/04/16.  GeneMi.
-->

```csharp
void Read( BinaryReader r )   
```  

## <a name="arguments"></a>Argumentos
*r*  
 O objeto **BinaryReader** que produz um fluxo binário correspondente a uma representação binária de um nó **hierarchyid**.  
  
## <a name="return-types"></a>Tipos de retorno
 **Tipo de retorno do CLR: nulo**  
  
## <a name="remarks"></a>Comentários  
 O método Read não valida sua entrada. Se uma entrada binária inválida for fornecida, Read poderá gerar uma exceção. Ou poderá ser bem-sucedido e produzir um objeto **SqlHierarchyId** inválido cujos métodos podem gerar resultados imprevisíveis ou uma exceção.  
  
 O método Read pode ser chamado apenas em um objeto **SqlHierarchyId** recém-criado.  
  
 Read é usado internamente por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] quando necessário, como ao gravar dados na coluna **hierarchyid**. Read também é chamado internamente quando é feita uma conversão entre **varbinary** e **hierarchyid**.  
  
## <a name="examples"></a>Exemplos  
  
```csharp
Byte[] encoding = new byte[] { 0x58 };  
MemoryStream stream = new MemoryStream(encoding, false /*not writable*/);  
BinaryReader br = new BinaryReader(stream);  
SqlHierarchyId hid = new SqlHierarchyId();  
hid.Read(br);   
```  
  
## <a name="see-also"></a>Consulte Também  
[Write &#40;Mecanismo de Banco de Dados&#41;](../../t-sql/data-types/write-database-engine.md)  
[ToString &#40;Mecanismo de Banco de Dados&#41;](../../t-sql/data-types/tostring-database-engine.md)  
[CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[Referência de método de tipo de dados hierarchyid](https://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)
  
  
