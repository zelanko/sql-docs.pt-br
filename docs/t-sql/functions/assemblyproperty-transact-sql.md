---
title: ASSEMBLYPROPERTY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ASSEMBLYPROPERTY_TSQL
- ASSEMBLYPROPERTY
dev_langs:
- TSQL
helpviewer_keywords:
- ASSEMBLYPROPERTY statement
- assemblies [CLR integration], properties
ms.assetid: cf03d1b1-724c-48bf-a8df-3fe2586b150a
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 50fd500a3ce7248b60e423df662b5d9eeda2cef5
ms.sourcegitcommit: 768f046107642f72693514f51bf2cbd00f58f58a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2020
ms.locfileid: "87113134"
---
# <a name="assemblyproperty-transact-sql"></a>ASSEMBLYPROPERTY (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Essa função retorna informações sobre uma propriedade de um assembly.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
ASSEMBLYPROPERTY('assembly_name', 'property_name')  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
*assembly_name*  
O nome do assembly.
  
*property_name*  
O nome de uma propriedade sobre a qual recuperar informações. *property_name* pode ter um dos valores a seguir:
  
|Valor|DESCRIÇÃO|  
|---|---|
|**CultureInfo**|Localidade do assembly.|  
|**PublicKey**|Chave pública ou token de chave pública do assembly.|  
|**MvID**|Número de identificação de versão completo do assembly gerado por compilador.|  
|**VersionMajor**|Componente principal (primeira parte) do número de identificação de versão de quatro partes do assembly.|  
|**VersionMinor**|Componente secundário (segunda parte) do número de identificação de versão de quatro partes do assembly.|  
|**VersionBuild**|Componente de compilação (terceira parte) do número de identificação de versão de quatro partes do assembly.|  
|**VersionRevision**|Componente de revisão (quarta parte) do número de identificação de versão de quatro partes do assembly.|  
|**SimpleName**|É o nome simples do assembly.|  
|**Arquitetura**|Arquitetura de processador do assembly.|  
|**CLRName**|Cadeia de caracteres canônica que codifica o nome simples, o número de versão, a cultura, a chave pública e a arquitetura do assembly. Esse valor identifica exclusivamente o assembly no lado CLR (Common Language Runtime).|  
  
## <a name="return-type"></a>Tipo de retorno
**sql_variant**
  
## <a name="examples"></a>Exemplos  
Este exemplo presume que um assembly de `HelloWorld` esteja registrado no banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]. Para obter mais informações, confira [Exemplo de Olá, Mundo](https://msdn.microsoft.com/library/fed6c358-f5ee-4d4c-9ad6-089778383ba7).
  
```sql
USE AdventureWorks2012;  
GO  
SELECT ASSEMBLYPROPERTY ('HelloWorld' , 'PublicKey');  
```  
  
## <a name="see-also"></a>Confira também
[CREATE ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/create-assembly-transact-sql.md)  
[DROP ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-assembly-transact-sql.md)
  
  
