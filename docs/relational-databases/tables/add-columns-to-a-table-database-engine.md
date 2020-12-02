---
description: Adicionar colunas a uma tabela (Mecanismo de Banco de Dados)
title: Adicionar colunas a uma tabela (mecanismo de banco de dados) | Microsoft Docs
ms.custom: ''
ms.date: 10/27/2016
ms.prod: sql
ms.prod_service: table-view-index, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- inserting columns
- columns [SQL Server], adding
- adding columns
ms.assetid: abeb8d52-d562-4e29-9e1e-2923ae874859
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ad7cb3cdba7b9b20a28362b8570cc6e2fc0b04d1
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96128757"
---
# <a name="add-columns-to-a-table-database-engine"></a>Adicionar colunas a uma tabela (Mecanismo de Banco de Dados)

[!INCLUDE [sqlserver2016-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi-asa-pdw.md)]

Este artigo descreve como adicionar novas colunas a uma tabela no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)].

## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar

### <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitações e restrições

 Usar a instrução ALTER TABLE para adicionar colunas a uma tabela automaticamente adiciona essas colunas ao final da tabela. Se você desejar que as colunas fiquem em uma ordem específica na tabela, use o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. No entanto, observe que esta não é uma prática recomendada de design de banco de dados. A prática recomendada é especificar a ordem em que as colunas serão retornadas nos níveis de aplicativo e de consulta. Você não deve confiar no uso de SELECT * para retornar todas as colunas na ordem esperada com base na ordem em que são definidas na tabela. Sempre especifique as colunas por nome em suas consultas e aplicativos na ordem em que você gostaria que elas aparecessem.

### <a name="security"></a><a name="Security"></a> Segurança

#### <a name="permissions"></a><a name="Permissions"></a> Permissões

Exige a permissão ALTER na tabela.

## <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio

### <a name="to-insert-columns-into-a-table-with-table-designer"></a>Para inserir colunas em uma tabela com o Designer de Tabela

1. No **Pesquisador de Objetos**, clique com o botão direito do mouse na tabela à qual você deseja adicionar colunas e selecione **Design**.
2. Clique na primeira célula vazia da coluna **Nome da Coluna** .
3. Digite o nome de coluna na célula. O nome da coluna é um valor obrigatório.
4. Pressione a tecla TAB para ir para a célula **Tipo de Dados** e selecione um tipo de dados no menu suspenso.

   Trata-se também de um valor obrigatório e será atribuído o valor padrão, se você não selecionar um.

   > [!NOTE]
   >  O valor padrão de **Opções** pode ser alterado na caixa de diálogo de **Ferramentas do Banco de Dados**.

5. Prossiga com a definição de outras propriedades de coluna na guia **Propriedades da Coluna** .

    > [!NOTE]
    >  Valores padrão de propriedades de coluna são adicionados quando uma nova coluna é criada. Contudo, é possível alterá-los na guia **Propriedades da Coluna** .

6. Quando você terminar de adicionar as colunas, no menu **Arquivo**, escolha **Salvar** _nome da tabela_.
  
## <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL
  
### <a name="to-insert-columns-into-a-table"></a>Para inserir colunas em uma tabela  
  
O exemplo a seguir adiciona duas colunas à tabela `dbo.doc_exa`.

```sql
ALTER TABLE dbo.doc_exa ADD column_b VARCHAR(20) NULL, column_c INT NULL ;
```

#### <a name="for-more-information-see-alter-table-40transact-sql41"></a><a name="FollowUp"></a> Para obter mais informações, consulte [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)
