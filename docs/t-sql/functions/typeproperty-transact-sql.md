---
title: TYPEPROPERTY (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 43
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: aecf422ca2289b2a417147eb402921bb8530d969
ms.openlocfilehash: 8608de51a13d2bc0109b9874b30749b10b65eaea
ms.contentlocale: pt-br
ms.lasthandoff: 10/24/2017

---
# <a name="typeproperty-transact-sql"></a>TYPEPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna informações sobre um tipo de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
TYPEPROPERTY (type , property)  
```  
  
## <a name="arguments"></a>Argumentos  
 *tipo*  
 É o nome do tipo de dados.  
  
 *propriedade*  
 É o tipo das informações a serem retornadas para o tipo de dados. *propriedade* pode ser um dos valores a seguir.  
  
|Propriedade|Description|Valor retornado|  
|--------------|-----------------|--------------------|  
|**AllowsNull**|Tipo de dados permite valores nulos.|1 = True<br /><br /> 0 = False<br /><br /> NULL = Tipo de dados não localizado.|  
|**OwnerId**|Proprietário do tipo.<br /><br /> Observação: O proprietário do esquema não é necessariamente o proprietário de tipo.|Nonnull = A ID de usuário de banco de dados do proprietário do tipo.<br /><br /> NULL = Tipo sem-suporte ou ID de tipo inválida.|  
|**Precisão**|Precisão para o tipo de dados.|O número de dígitos ou caracteres.<br /><br /> -1 = **xml** ou tipo de dados de valor grande<br /><br /> NULL = Tipo de dados não localizado.|  
|**Escala**|Escala para o tipo de dados.|O número de lugares decimais para o tipo de dados.<br /><br /> NULL = não é de tipo de dados **numérico** ou não encontrado.|  
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
  
## <a name="see-also"></a>Consulte também  
 [TYPE_ID &#40; Transact-SQL &#41;](../../t-sql/functions/type-id-transact-sql.md)   
 [TYPE_NAME &#40; Transact-SQL &#41;](../../t-sql/functions/type-name-transact-sql.md)   
 [COLUMNPROPERTY &#40; Transact-SQL &#41;](../../t-sql/functions/columnproperty-transact-sql.md)   
 [Funções de metadados &#40; Transact-SQL &#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [OBJECTPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/objectproperty-transact-sql.md)   
 [ALTER AUTHORIZATION &#40; Transact-SQL &#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [Types &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)  
  
  


