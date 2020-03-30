---
title: xml_schema_namespace (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/27/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- xml_schema_namespace_TSQL
- xml_schema_namespace
dev_langs:
- TSQL
helpviewer_keywords:
- XML schema collections [SQL Server], reconstructing schemas
- xml_schema_namespace function
- reconstructing schemas
- schemas [SQL Server], XML
- schema collections [SQL Server], reconstructing schemas
ms.assetid: ee9873d8-dd3a-4bff-a10c-68bbadbdf1a6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bb3b19e67a4a85ef3f7a26d7ad792e7e39459302
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "67948025"
---
# <a name="xml_schema_namespace"></a>xml_schema_namespace
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Reconstrói todos os esquemas ou um esquema específico na coleção de esquema XML especificada. Essa função retorna uma instância de tipo de dados **xml** .  
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
xml_schema_namespace( Relational_schema , XML_schema_collection_name , [ Namespace ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Relational_schema*  
 É o nome do esquema relacional. *Relational_schema* é **sysname**.  
  
 *XML_schema_collection_name*  
 É o nome da coleção de esquemas XML a ser reconstruída. *XML_schema_collection_name* é **sysname**.  
  
 *Namespace*  
 É o namespace URI do esquema XML que deseja reconstruir. É limitado a 1.000 caracteres. Se o URI do namespace não for fornecido, a coleção inteira de esquemas XML será reconstruída. *Namespace* é **nvarchar(4000)** .  
  
## <a name="return-types"></a>Tipos de retorno  
 **xml**  
  
## <a name="remarks"></a>Comentários  
 Quando você importa os componentes do esquema XML no banco de dados usando [CREATE XML SCHEMA COLLECTION](../../t-sql/statements/create-xml-schema-collection-transact-sql.md) ou [ALTER XML SCHEMA COLLECTION](../../t-sql/statements/alter-xml-schema-collection-transact-sql.md), os aspectos do esquema usados para validação são preservados. Portanto, o esquema reconstruído pode não ser lexicalmente igual ao documento de esquema original. Especificamente, comentários, espaços em branco e anotações são perdidos; as informações de tipo implícitas são explicitadas. Por exemplo, \<xs:element name="e1" /> se torna \<xs:element name="e1" type="xs:anyType"/>. Além disso, prefixos de namespace não são preservados.  
  
 Se um parâmetro de namespace for especificado, o documento de esquema resultante conterá definições para todos os componentes de esquema no namespace, mesmo que eles tenham sido adicionados em documentos de esquema diferentes, em etapas DDL ou em ambos.  
  
 Não é possível usar esta função para construir documentos de esquema XML usando a coleção de esquemas XML **sys.sys**.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir recupera a coleção de esquema XML `ProductDescriptionSchemaCollection` do esquema relacional de produção no banco de dados `AdventureWorks`.  
  
```  
USE AdventureWorks;  
GO  
SELECT xml_schema_namespace(N'production',N'ProductDescriptionSchemaCollection');  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Exibir uma coleção de esquemas XML armazenados](../../relational-databases/xml/view-a-stored-xml-schema-collection.md)   
 [Coleções de esquemas XML &#40;SQL Server&#41;](../../relational-databases/xml/xml-schema-collections-sql-server.md)  
  
  
