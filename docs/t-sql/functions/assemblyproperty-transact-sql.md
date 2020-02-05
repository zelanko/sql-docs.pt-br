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
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: ac25131e24aa89253abfc13eac69a4a60d0b7aee
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68040293"
---
# <a name="assemblyproperty-transact-sql"></a>ASSEMBLYPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Essa função retorna informações sobre uma propriedade de um assembly.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
ASSEMBLYPROPERTY('assembly_name', 'property_name')  
```  
  
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
  
  
