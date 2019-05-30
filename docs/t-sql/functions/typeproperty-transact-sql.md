---
title: TYPEPROPERTY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- TYPEPROPERTY
- TYPEPROPERTY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- status information [SQL Server], data types
- data types [SQL Server], status information
- TYPEPROPERTY function
ms.assetid: bc311c80-bac5-46ab-a5c8-68b1c6bbf24a
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 796de66b6fdce95be5fe235219208a504cc8095e
ms.sourcegitcommit: 83f061304fedbc2801d8d6a44094ccda97fdb576
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/20/2019
ms.locfileid: "65946830"
---
# <a name="typeproperty-transact-sql"></a>TYPEPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna informações sobre um tipo de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
TYPEPROPERTY (type , property)  
```  
  
## <a name="arguments"></a>Argumentos  
 *type*  
 É o nome do tipo de dados.  
  
 *property*  
 É o tipo das informações a serem retornadas para o tipo de dados. *property* pode ser um dos valores a seguir.  
  
|Propriedade|Descrição|Valor retornado|  
|--------------|-----------------|--------------------|  
|**AllowsNull**|Tipo de dados permite valores nulos.|1 = True<br /><br /> 0 = False<br /><br /> NULL = Tipo de dados não localizado.|  
|**OwnerId**|Proprietário do tipo.<br /><br /> Observação: O proprietário do esquema não é necessariamente o proprietário do tipo.|Nonnull = A ID de usuário de banco de dados do proprietário do tipo.<br /><br /> NULL = Tipo sem-suporte ou ID de tipo inválida.|  
|**Precisão**|Precisão para o tipo de dados.|O número de dígitos ou caracteres.<br /><br /> -1 = **xml** ou um tipo de dados de valor grande<br /><br /> NULL = Tipo de dados não localizado.|  
|**Escala**|Escala para o tipo de dados.|O número de lugares decimais para o tipo de dados.<br /><br /> NULL = o tipo de dados não é **numeric** ou não foi encontrado.|  
|**UsesAnsiTrim**|Configuração de preenchimento ANSI era ON quando o tipo de dados foi criado.|1 = True<br /><br /> 0 = False<br /><br /> NULL = Tipo de dados não localizado ou não é um tipo de dados binário ou de cadeia de caracteres.|  
  
## <a name="return-types"></a>Tipos de retorno  
 **int**  
  
## <a name="exceptions"></a>Exceções  
 Retornará NULL em caso de erro ou se um chamador não tiver permissão para exibir o objeto.  
  
 No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], um usuário só pode exibir os metadados de itens protegíveis de sua propriedade ou para os quais ele tenha permissão concedida. Isso significa que as funções internas emissoras de metadados, como TYPEPROPERTY, podem retornar NULL se o usuário não tiver nenhuma permissão no objeto. Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-identifying-the-owner-of-a-data-type"></a>A. Identificando o proprietário de um tipo de dados  
 O exemplo a seguir retorna o proprietário de um tipo de dados.  
  
```  
SELECT TYPEPROPERTY(SCHEMA_NAME(schema_id) + '.' + name, 'OwnerId') AS owner_id, name, system_type_id, user_type_id, schema_id  
FROM sys.types;  
```  
  
### <a name="b-returning-the-precision-of-the-tinyint-data-type"></a>B. Retornando a precisão do tipo de dados tinyint  
 O exemplo a seguir retorna a precisão ou o número de dígitos para o tipo de dados `tinyint`.  
  
```  
SELECT TYPEPROPERTY( 'tinyint', 'PRECISION');  
```  
  
## <a name="see-also"></a>Consulte Também  
 [TYPE_ID &#40;Transact-SQL&#41;](../../t-sql/functions/type-id-transact-sql.md)   
 [TYPE_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/type-name-transact-sql.md)   
 [COLUMNPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/columnproperty-transact-sql.md)   
 [Funções de metadados &#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [OBJECTPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/objectproperty-transact-sql.md)   
 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [sys.types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)  
  
  

