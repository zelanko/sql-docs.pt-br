---
title: Especificar valores padrão para colunas | Microsoft Docs
ms.custom: ''
ms.date: 02/20/2019
ms.prod: sql
ms.prod_service: table-view-index, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- columns [SQL Server], defaults
- default values
ms.assetid: 64514aed-b846-407b-992e-cf813f9a1a91
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5e00c22ed3b7728d906ab2a143ca30f2eec8c7ee
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68016283"
---
# <a name="specify-default-values-for-columns"></a>Especificar valores padrão para colunas

[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

Você pode usar [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para especificar um valor padrão que será inserido na coluna da tabela. Você pode usar o Pesquisador de Objetos da interface do usuário ou o controle geral para enviar [!INCLUDE[tsql](../../includes/tsql-md.md)].

Se você não atribuir um valor padrão para a coluna e o usuário deixar a coluna em branco, então:

- Se você definir a opção para permitir valores nulos, será inserido NULL na coluna.

- Se você não definir a opção para permitir valores nulos, a coluna permanecerá em branco, mas o usuário não poderá salvar a linha até fornecer um valor para a coluna.

## <a name="Restrictions"></a> Limitações e restrições

Antes de começar, esteja ciente das seguintes limitações e restrições:

- Se sua entrada no campo **Valor Padrão** substituir um padrão associado (exibido sem parênteses), será solicitado que você desvincule o padrão e substitua-o pelo novo padrão.

- Para inserir uma cadeia de caracteres de texto, coloque o valor entre aspas simples ('); não utilize aspas duplas ("), pois elas estão reservadas para identificadores entre aspas.

- Para inserir um padrão numérico, insira o número sem colocá-lo entre aspas.

- Para inserir um objeto/função, digite o nome do objeto/função sem aspas.

### <a name="Security"></a> Permissões de segurança

As ações descritas neste artigo exigem a permissão ALTER na tabela.

## <a name="SSMSProcedure"></a> Usar SSMS para especificar um padrão

Você pode usar o Pesquisador de Objetos para especificar um valor padrão para uma coluna de tabela.

### <a name="object-explorer"></a>Pesquisador de Objetos

1. No **Pesquisador de Objetos**, clique com o botão direito do mouse na tabela com as colunas cuja escala você deseja alterar e clique em **Design**.

2. Selecione a coluna para a qual você deseja especificar o valor padrão.

3. Na guia **Propriedades da Coluna** , insira o novo valor padrão na propriedade **Valor ou Associação Padrão** .

   > [!NOTE]
   > Para inserir um valor numérico padrão, insira o número. Para um objeto ou função insira seu nome. Para um padrão alfanumérico insira o valor entre aspas simples.

4. No menu **Arquivo**, clique em **Salvar** _nome da tabela_.

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

## <a name="TsqlProcedure"></a> Usar o Transact-SQL para especificar um padrão

Há várias maneiras pelas quais você pode especificar um valor padrão para uma coluna usando o SSMS para enviar o T-SQL.

### <a name="alter-table-t-sql"></a>ALTER TABLE (T-SQL)

1. No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].

2. Na barra Padrão, clique em **Nova Consulta**.

3. Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.

   ```sql
   CREATE TABLE dbo.doc_exz (column_a INT, column_b INT); -- Allows nulls.
   GO
   INSERT INTO dbo.doc_exz (column_a) VALUES (7);
   GO
   ALTER TABLE dbo.doc_exz
     ADD CONSTRAINT col_b_def
     DEFAULT 50 FOR column_b;
   GO
   ```

<!--
The following two T-SQL code examples were offered by 'nycdotnet' (Steve) via public PR 1660, Feb 2019.
-->

### <a name="create-table-t-sql"></a>CREATE TABLE (T-SQL)

```sql
    CREATE TABLE dbo.doc_exz (
      column_a INT,
      column_b INT DEFAULT 50);
```

### <a name="named-constraint-t-sql"></a>CONSTRAINT nomeada (T-SQL)

```sql
    CREATE TABLE dbo.doc_exz (
      column_a INT,
      column_b INT CONSTRAINT DF_doc_exz_column_b DEFAULT 50);
```

Para obter mais informações, veja [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md).
