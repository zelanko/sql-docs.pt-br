---
title: sp_unbindrule (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_unbindrule_TSQL
- sp_unbindrule
dev_langs:
- TSQL
helpviewer_keywords:
- sp_unbindrule
ms.assetid: f54ee155-c3c9-4f1a-952e-632a8339f0cc
caps.latest.revision: 34
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 9844048e1dc45e61c87d4598f2f03b4865c68e11
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="spunbindrule-transact-sql"></a>sp_unbindrule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Desvincula uma regra de uma coluna ou de um tipo de dados de alias no banco de dados atual.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)] É recomendável criar definições padrão usando a palavra-chave DEFAULT no [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) ou [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md) instruções em vez disso.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_unbindrule [ @objname = ] 'object_name'   
     [ , [ @futureonly = ] 'futureonly_flag' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@objname=** ] **'***object_name***'**  
 É o nome da tabela e da coluna ou o tipo de dados do alias do qual a regra é desassociada. *object_name* é **nvarchar(776)**, sem padrão. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tenta resolver identificadores de duas partes primeiro para nomes das colunas e, em seguida, para tipos de dados do alias. Ao desvincular uma regra de um tipo de dados de alias, as colunas do tipo de dados que tiverem a mesma regra também serão desvinculadas. As colunas desse tipo de dados com regras vinculadas diretamente não serão afetadas.  
  
> [!NOTE]  
>  *object_name* pode conter colchetes **[]** como caracteres de identificador delimitados. Para obter mais informações, consulte [Database Identifiers](../../relational-databases/databases/database-identifiers.md).  
  
 [  **@futureonly=** ] **'***futureonly_flag***'**  
 É usado apenas ao desvincular uma regra de um tipo de dados de alias. *futureonly_flag* é **varchar(15)**, com um padrão NULL. Quando *futureonly_flag* é **futureonly**, as colunas existentes desse tipo de dados não perdem a regra especificada.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Remarks  
 Para exibir o texto de uma regra, execute **sp_helptext** com o nome da regra como o parâmetro.  
  
 Quando uma regra é desvinculada, as informações sobre a associação são removidas do **Columns** tabela se a regra foi associada de uma coluna e o **Types** se a regra foi associada a um tipo de dados de alias de tabela.  
  
 Quando uma regra é desvinculada de um tipo de dados de alias, ela também é desvinculada das colunas com esse tipo de dados de alias. A regra ainda pode ser associada a colunas cujos tipos de dados tenham sido alterados posteriormente pela cláusula ALTER COLUMN de uma instrução ALTER TABLE, desvincular especificamente a regra dessas colunas usando **sp_unbindrule** e especificando o nome da coluna.  
  
## <a name="permissions"></a>Permissões  
 Para desvincular uma regra de uma coluna de tabela, é necessário ter a permissão ALTER na tabela. Para desvincular uma regra de um tipo de dados de alias, é necessário ter a permissão CONTROL no tipo ou a permissão ALTER no esquema ao qual o tipo pertence.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-unbinding-a-rule-from-a-column"></a>A. Desvinculando uma regra de uma coluna  
 O exemplo a seguir desvincula a regra da coluna `startdate` de uma tabela `employees`.  
  
```  
EXEC sp_unbindrule 'employees.startdate';  
```  
  
### <a name="b-unbinding-a-rule-from-an-alias-data-type"></a>B. Desvinculando uma regra de um tipo de dados de alias  
 O exemplo a seguir desvincula a regra do tipo de dados de alias `ssn`. Ele desvincula a regra de colunas desse tipo, existentes e futuras.  
  
```  
EXEC sp_unbindrule ssn;  
```  
  
### <a name="c-using-futureonlyflag"></a>C. Usando futureonly_flag  
 O exemplo a seguir desvincula a regra do tipo de dados de alias `ssn` sem afetar as colunas `ssn` existentes.  
  
```  
EXEC sp_unbindrule 'ssn', 'futureonly';  
```  
  
### <a name="d-using-delimited-identifiers"></a>D. Usando identificadores delimitados  
 O exemplo a seguir mostra o uso de identificadores delimitados no *object_name* parâmetro.  
  
```  
CREATE TABLE [t.4] (c1 int); -- Notice the period as part of the table   
-- name.  
GO  
CREATE RULE rule2 AS @value > 100;  
GO  
EXEC sp_bindrule rule2, '[t.4].c1' -- The object contains two   
-- periods; the first is part of the table name and the second   
-- distinguishes the table name from the column name.  
GO  
EXEC sp_unbindrule '[t.4].c1';  
```  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Procedimentos armazenados do mecanismo de banco de dados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [CREATE RULE &#40;Transact-SQL&#41;](../../t-sql/statements/create-rule-transact-sql.md)   
 [DROP RULE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-rule-transact-sql.md)   
 [sp_bindrule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-bindrule-transact-sql.md)   
 [sp_helptext &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
