---
title: CREATE RULE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- RULE_TSQL
- CREATE RULE
- CREATE_RULE_TSQL
- RULE
dev_langs:
- TSQL
helpviewer_keywords:
- list rules [SQL Server]
- unbinding rules
- pattern rules [SQL Server]
- range rules [SQL Server]
- alias data types [SQL Server], rules
- CREATE RULE statement
- reports [SQL Server], rules
- status information [SQL Server], rules
- rules [SQL Server], precedence
- binding rules [SQL Server]
- rules [SQL Server], creating
ms.assetid: b016a289-3a74-46b1-befc-a13183be51e4
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 0e0a46138b9e6c4ccaff09c1ab5261f739deb6b5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68006497"
---
# <a name="create-rule-transact-sql"></a>CREATE RULE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cria um objeto chamado regra. Quando associada a uma coluna ou a um tipo de dados de alias, a regra especifica os valores aceitáveis que podem ser inseridos naquela coluna.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Recomenda-se o uso de restrições de verificação. As restrições de verificação são criadas pelo uso da palavra-chave CHECK de CREATE TABLE ou ALTER TABLE. Para obter mais informações, consulte [Unique Constraints and Check Constraints](../../relational-databases/tables/unique-constraints-and-check-constraints.md).  
  
 Uma coluna ou tipo de dados de alias só pode ter uma regra associada. No entanto, uma coluna pode ter uma regra e uma ou mais restrições de verificação associadas. Quando isso ocorrer, todas as restrições serão avaliadas.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
CREATE RULE [ schema_name . ] rule_name   
AS condition_expression  
[ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *schema_name*  
 É o nome do esquema ao qual a regra pertence.  
  
 *rule_name*  
 É o nome da nova regra. Nomes de regras precisam ser compatíveis com as regras para [identificadores](../../relational-databases/databases/database-identifiers.md). A especificação do nome do proprietário da regra é opcional.  
  
 *condition_expression*  
 É a condição ou condições que definem a regra. Uma regra pode ser qualquer expressão válida em uma cláusula WHERE e pode incluir elementos, como operadores aritméticos, operadores relacionais e predicados (por exemplo, IN, LIKE, BETWEEN). Uma regra não pode fazer referência a colunas ou a outros objetos de banco de dados. É possível incluir funções internas que não fazem referência a objetos de banco de dados. As funções definidas pelo usuário não podem ser usadas.  
  
 *condition_expression* inclui uma variável. O sinal de arroba ( **@** ) precede cada uma das variáveis locais. A expressão se refere ao valor digitado com a instrução UPDATE ou INSERT. Qualquer nome ou símbolo pode ser usado para representar o valor durante a criação da regra. No entanto, o primeiro caractere deve ser o sinal de arroba ( **@** ).  
  
> [!NOTE]  
>  Evite criar regras em expressões que usam tipos de dados de alias. Embora as regras possam ser criadas em expressões que usam tipos de dados de alias, após associar as regras a tipos de dados de colunas ou de alias, as expressões falham ao compilar quando referenciadas.  
  
## <a name="remarks"></a>Remarks  
 CREATE RULE não pode ser combinada com outras instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] em um único lote. As regras não se aplicam a dados já existentes no banco de dados no momento da criação das regras, e as regras não podem ser associadas a tipos de dados do sistema.  
  
 A regra só pode ser criada no banco de dados atual. Depois de criar uma regra, execute **sp_bindrule** para associá-la ao tipo de dados de coluna ou de alias. A regra deve ser compatível com o tipo de dados de coluna. Por exemplo, "\@value LIKE A% " não pode ser usado como regra para uma coluna numérica. Uma regra não pode ser associada a um **text**, **ntext**, **image**, **varchar(max)** , **nvarchar(max)** , **varbinary(max)** , **xml**, tipo de dado CLR definido pelo usuário ou uma coluna **timestamp**. A regra não pode ser associada a uma coluna computada.  
  
 Inclua as constantes de caractere e data entre aspas ('), precedendo as constantes binárias com 0x. Se a regra não for compatível com a coluna à qual está associada, o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] retornará uma mensagem de erro quando o valor for inserido, mas não quando a regra for associada.  
  
 Uma regra associada a um tipo de dados de alias é ativada apenas quando se tenta inserir um valor em, ou atualizar, uma coluna de banco de dados do tipo de dados de alias. Como as regras não testam variáveis, não atribua um valor a uma variável do tipo de dados de alias que possa ser rejeitada por uma regra associada à coluna do mesmo tipo de dados.  
  
 Para obter um relatório sobre uma regra, use **sp_help**. Para exibir o texto de uma regra, execute **sp_helptext** com o nome da regra como o parâmetro. Para renomear uma regra, use **sp_rename**.  
  
 Uma regra deve ser removida com DROP RULE antes que uma nova com o mesmo nome seja criada, e a regra deve ser desassociada usando **sp_unbindrule** antes de ser removida. Para desassociar uma regra de uma coluna, use **sp_unbindrule**.  
  
 Você pode associar uma nova regra a uma coluna ou tipo de dados sem desassociar a anterior; a nova regra substitui a anterior. As regras associadas a colunas sempre têm precedência a regras associadas a tipos de dados de alias. A associação de uma regra a uma coluna substitui a regra já associada ao tipo de dados de alias daquela coluna. Mas a associação de uma regra a um tipo de dados não substitui a regra associada à coluna daquele tipo de dados de alias. A tabela a seguir mostra a precedência em vigor quando as regras são associadas a colunas e a tipos de dados de alias nos quais já existem regras.  
  
|Nova regra associada a|Regra antiga associada a<br /><br /> tipo de dados de alias|Regra antiga associada a<br /><br /> coluna|  
|-----------------------|-------------------------------------------|----------------------------------|  
|Tipo de dados de alias|Regra antiga substituída|Nenhuma alteração|  
|coluna|Regra antiga substituída|Regra antiga substituída|  
  
 Se uma coluna tiver um padrão e uma regra associados, o padrão deverá se encaixar no domínio definido pela regra. Um padrão em conflito com uma regra nunca é inserido. O Mecanismo de Banco de Dados do SQL Server gera uma mensagem de erro toda vez que tenta inserir um padrão assim.  
  
## <a name="permissions"></a>Permissões  
 Para executar CREATE RULE, no mínimo, um usuário deve ter a permissão CREATE RULE no banco de dados atual e a permissão ALTER no esquema em que a regra está sendo criada.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-creating-a-rule-with-a-range"></a>A. Criando uma regra com um intervalo  
 O exemplo a seguir cria uma regra que restringe o intervalo de inteiros inserido na coluna ou colunas às quais essa regra está associada.  
  
```  
CREATE RULE range_rule  
AS   
@range>= $1000 AND @range <$20000;  
```  
  
### <a name="b-creating-a-rule-with-a-list"></a>B. Criando uma regra com uma lista  
 O exemplo a seguir cria uma regra que restringe os valores reais digitados na coluna ou colunas (às quais essa regra está associada) somente para aqueles listados na regra.  
  
```  
CREATE RULE list_rule  
AS   
@list IN ('1389', '0736', '0877');  
```  
  
### <a name="c-creating-a-rule-with-a-pattern"></a>C. Criando uma regra com um padrão  
 O exemplo a seguir cria uma regra para seguir o padrão de quaisquer dois caracteres seguidos de um hífen (`-`), qualquer número de caracteres ou nenhum caractere, e que termina com um número inteiro de `0` a `9`.  
  
```  
CREATE RULE pattern_rule   
AS  
@value LIKE '__-%[0-9]'  
```  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [CREATE DEFAULT &#40;Transact-SQL&#41;](../../t-sql/statements/create-default-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [DROP DEFAULT &#40;Transact-SQL&#41;](../../t-sql/statements/drop-default-transact-sql.md)   
 [DROP RULE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-rule-transact-sql.md)   
 [Expressões &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [sp_bindrule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-bindrule-transact-sql.md)   
 [sp_help &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [sp_helptext &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md)   
 [sp_rename &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)   
 [sp_unbindrule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-unbindrule-transact-sql.md)   
 [WHERE &#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)  
  
  
