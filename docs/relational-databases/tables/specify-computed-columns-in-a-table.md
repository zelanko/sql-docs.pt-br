---
title: Especificar colunas computadas em uma tabela | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- computed columns, define
ms.assetid: 731a4576-09c1-47f0-a8f6-edd0b55679f4
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 546490349b2d80135c873ff0917ab571f3cae830
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85731577"
---
# <a name="specify-computed-columns-in-a-table"></a>Especificar colunas computadas em uma tabela

[!INCLUDE[tsql-appliesto-ss-asdb-xxxx-xxx-md](../../includes/applies-to-version/sql-asdb.md)]

Uma coluna computada é uma coluna virtual que não está fisicamente armazenada na tabela, a menos que a coluna esteja marcada como PERSISTED. Uma expressão de coluna computada pode usar dados de outras colunas para calcular um valor para a coluna à qual pertence. Você pode especificar uma expressão para uma coluna computada no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)].

**Neste tópico**

- **Antes de começar:**

   [Limitações e restrições](#Limitations)

   [Segurança](#Security)

- **Para especificar uma coluna computada usando:**

   [SQL Server Management Studio](#SSMSProcedure)

   [Transact-SQL](#TsqlProcedure)

## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar

### <a name="limitations-and-restrictions"></a><a name="Limitations"></a> Limitações e restrições

- Uma coluna computada não pode ser usada como uma definição de restrição DEFAULT ou FOREIGN KEY ou com uma definição de restrição NOT NULL. Entretanto, se o valor da coluna computada for definido por uma expressão determinística e o tipo de dados do resultado for permitido em colunas de índice, uma coluna computada poderá ser usada como uma coluna de chave em um índice ou como parte de qualquer restrição PRIMARY KEY ou UNIQUE. Por exemplo, se a tabela tiver colunas de inteiros a e b, a coluna computada a + b poderá ser indexada, mas a coluna computada a +DATEPART(dd, GETDATE()) não poderá ser indexada, pois o valor pode ser alterado em invocações subsequentes.
- Uma coluna computada não pode ser o destino de uma instrução INSERT ou UPDATE.

### <a name="security"></a><a name="Security"></a> Segurança

#### <a name="permissions"></a><a name="Permissions"></a> Permissões

Exige a permissão ALTER na tabela.

## <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio

### <a name="to-add-a-new-computed-column"></a><a name="NewColumn"></a> Para adicionar uma nova coluna computada

1. No **Pesquisador de Objetos**, expanda a tabela na qual você deseja adicionar a nova coluna computada. Clique com o botão direito do mouse em **Colunas** e selecione **Nova Coluna**.
2. Insira o nome da coluna e aceite o tipo de dados padrão (**nchar**(10)). O [!INCLUDE[ssDE](../../includes/ssde-md.md)] determina o tipo de dados da coluna computada, aplicando as regras de precedência de tipos de dados às expressões especificadas na fórmula. Por exemplo, se a fórmula referenciar uma coluna de tipo **money** e uma coluna de tipo **int**, a coluna computada será do tipo **money** porque esse tipo de dados tem maior precedência. Para obter mais informações, veja [Precedência de tipo de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-type-precedence-transact-sql.md).
3. Na guia **Propriedades da Coluna** , expanda a propriedade **Especificação de Coluna Computada** .
4. Na propriedade filho **(Fórmula)** , insira a expressão para essa coluna na célula de grade à direita. Por exemplo, em uma coluna `SalesTotal` , a fórmula que você insere pode ser `SubTotal+TaxAmt+Freight`, que associa o valor nessas colunas a cada linha na tabela.

   > [!IMPORTANT]
   > Quando uma fórmula combina duas expressões de tipos de dados diferentes, as regras de precedência do tipo de dados especificam que o tipo de dados com menor precedência é convertido no tipo de dados de maior precedência. Se a conversão não for uma conversão implícita com suporte, o erro "`Error validating the formula for column column_name.`" será retornado. Use a função CAST ou CONVERT para resolver o conflito de tipo de dados. Por exemplo, se uma coluna de tipo **nvarchar** é combinada com uma coluna de tipo **int**, o tipo inteiro deve ser convertido em **nvarchar** , conforme mostrado nesta fórmula `('Prod'+CONVERT(nvarchar(23),ProductID))`. Para obter mais informações, veja [CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md).

5. Indique se os dados são persistentes escolhendo **Sim** ou **Não** na lista suspensa da propriedade filho **Is Persisted** .

6. No menu **Arquivo**, clique em **Salvar** _nome da tabela_.

#### <a name="to-add-a-computed-column-definition-to-an-existing-column"></a>Para adicionar uma definição de coluna computada em uma coluna existente

1. No **Pesquisador de Objetos**, clique com o botão direito do mouse na tabela com a coluna que você deseja alterar e expanda a pasta **Colunas** .
2. Clique com o botão direito do mouse na coluna para a qual você deseja especificar uma fórmula de coluna computada e clique em **Excluir**. Clique em **OK**.
3. Adicione uma nova coluna e especifique a fórmula de coluna computada seguindo o procedimento anterior para adicionar uma nova coluna computada.

## <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL

### <a name="to-add-a-computed-column-when-creating-a-table"></a>Para adicionar uma coluna computada ao criar uma tabela

O exemplo a seguir cria uma tabela com uma coluna computada que multiplica o valor da coluna `QtyAvailable` pelo valor da coluna `UnitPrice`.

```sql
CREATE TABLE dbo.Products
   (
      ProductID int IDENTITY (1,1) NOT NULL
      , QtyAvailable smallint
      , UnitPrice money
      , InventoryValue AS QtyAvailable * UnitPrice
    )
;
-- Insert values into the table.
INSERT INTO dbo.Products (QtyAvailable, UnitPrice)
   VALUES (25, 2.00), (10, 1.5)
;
-- Display the rows in the table.
SELECT ProductID, QtyAvailable, UnitPrice, InventoryValue
FROM dbo.Products
;
```

### <a name="to-add-a-new-computed-column-to-an-existing-table"></a>Para adicionar uma nova coluna computada em uma tabela existente

O exemplo a seguir adiciona uma nova coluna à tabela criada no exemplo anterior.

```sql
ALTER TABLE dbo.Products ADD RetailValue AS (QtyAvailable * UnitPrice * 1.5)
;
```

Opcionalmente, adicione o argumento PERSISTED para armazenar fisicamente os valores computados na tabela:

```sql
ALTER TABLE dbo.Products ADD RetailValue AS (QtyAvailable * UnitPrice * 1.5) PERSISTED
;
```

### <a name="to-change-an-existing-column-to-a-computed-column"></a>Para transformar uma coluna existente em coluna computada

O exemplo a seguir modifica a coluna adicionada no exemplo anterior.

```sql
ALTER TABLE dbo.Products DROP COLUMN RetailValue
;
GO
ALTER TABLE dbo.Products ADD RetailValue AS (QtyAvailable * UnitPrice * 1.5)
;
```

Para obter mais informações, veja [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md).
