---
title: Gerar comandos com CommandBuilders
description: Explica como usar construtores para gerar automaticamente comandos INSERT, UPDATE e DELETE para um `DataAdapter` que tenha um comando SELECT de tabela única.
ms.date: 11/25/2020
dev_langs:
- csharp
ms.assetid: 6e3fb8b5-373b-4f9e-ab03-a22693df8e91
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: 091f7c2736c240951beb0f434fdcd2efb39a9b59
ms.sourcegitcommit: debaff72dbfae91b303f0acd42dd6d99e03135a2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/01/2020
ms.locfileid: "96428172"
---
# <a name="generating-commands-with-commandbuilders"></a>Gerar comandos com CommandBuilders

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

Quando a propriedade `SelectCommand` do objeto <xref:System.Data.Common.DbDataAdapter> é especificada dinamicamente em tempo de execução, como por meio de uma ferramenta de consulta que recebe um comando textual do usuário, pode não ser possível especificar o `InsertCommand`, `UpdateCommand` ou `DeleteCommand` apropriado no tempo de design. Se seu <xref:System.Data.DataTable> mapear para ou for gerado a partir de uma única tabela do banco de dados, você poderá aproveitar o objeto <xref:System.Data.Common.DbCommandBuilder> para gerar automaticamente o `DeleteCommand`, `InsertCommand` e `UpdateCommand` do <xref:System.Data.Common.DbDataAdapter>.

> [!NOTE]
> No Provedor de Dados do Microsoft SqlClient para SQL Server, a classe <xref:Microsoft.Data.SqlClient.SqlDataAdapter> é derivada da classe <xref:System.Data.Common.DbDataAdapter>, e a classe <xref:Microsoft.Data.SqlClient.SqlCommandBuilder> é derivada da <xref:System.Data.Common.DbCommandBuilder>.

Como um requisito mínimo, você deverá definir a propriedade `SelectCommand` para que a geração automática de comando funcione. O esquema da tabela recuperado pela propriedade `SelectCommand` determina a sintaxe das instruções INSERT, UPDATE e DELETE geradas automaticamente.

O <xref:System.Data.Common.DbCommandBuilder> deve executar o `SelectCommand` na ordem para retornar os metadados necessários para construir os comandos SQL INSERT, UPDATE e DELETE. Como resultado, uma viagem extra à fonte de dados é necessária e isso pode comprometer o desempenho. Para obter o desempenho ideal, especifique seus comandos explicitamente em vez de usar o <xref:System.Data.Common.DbCommandBuilder>.

> [!NOTE]
> O `SelectCommand` também deve retornar pelo menos uma chave primária ou coluna exclusivo. Se nenhuma delas estiver presente, uma exceção `InvalidOperation` será gerada, e os comandos não serão gerados.

Quando estiver associado com um `DataAdapter`, o <xref:System.Data.Common.DbCommandBuilder> gera automaticamente as propriedades `InsertCommand`, `UpdateCommand` e `DeleteCommand` do `DataAdapter` se forem referências nulas. Se um `Command` já existir para uma propriedade, o `Command` existente será usado.

As exibições de banco de dados que são criadas juntando duas ou mais tabelas não são consideradas uma única tabela de banco de dados. Nessa instância, não é possível usar o <xref:System.Data.Common.DbCommandBuilder> para gerar comandos automaticamente. Você deve especificar os comandos de forma explícita.

Você pode desejar mapear parâmetros de saída de volta para a linha atualizada de um `DataSet`. Uma tarefa comum é recuperar o valor de um campo de identidade ou um carimbo de data/hora gerado automaticamente da fonte de dados. O <xref:System.Data.Common.DbCommandBuilder> não mapeará parâmetros de saída para colunas em uma linha atualizada por padrão. Nessa instância, você deve especificar o comando explicitamente.

## <a name="rules-for-automatically-generated-commands"></a>Regras para comandos gerados automaticamente

A tabela a seguir mostra as regras para como os comandos gerados automaticamente são gerados.

|Comando|Regra|  
|-------------|----------|  
|`InsertCommand`|Insere uma linha na fonte de dados para todas as linhas na tabela com um <xref:System.Data.DataRow.RowState%2A> de <xref:System.Data.DataRowState.Added>. Insere valores para todas as colunas que são atualizáveis (mas não colunas como identidades, expressões ou carimbos de data/hora).|  
|`UpdateCommand`|Atualiza linhas na fonte de dados para todas as linhas na tabela com um `RowState` de <xref:System.Data.DataRowState.Modified>. Atualiza os valores de todas as colunas exceto as que não são atualizáveis, como identidades ou expressões. Atualiza todas as linhas onde os valores de coluna na fonte de dados correspondem aos valores de coluna de chave primária da linha, e onde as colunas restantes na fonte de dados correspondem aos valores originais da linha. Para obter mais informações, consulte “Modelo de simultaneidade otimista para atualizações e exclusões”, posteriormente neste tópico.|  
|`DeleteCommand`|Exclui linhas na fonte de dados para todas as linhas na tabela com um `RowState` de <xref:System.Data.DataRowState.Deleted>. Exclui todas as linhas onde os valores de coluna correspondem aos valores de coluna de chave primária da linha, e onde as colunas restantes na fonte de dados correspondem aos valores originais da linha. Para obter mais informações, confira o [Modelo de simultaneidade otimista para atualizações e exclusões](#optimistic-concurrency-model-for-updates-and-deletes), mais adiante neste tópico.|

## <a name="optimistic-concurrency-model-for-updates-and-deletes"></a>Modelo de simultaneidade otimista para atualizações e exclusões

A lógica para gerar automaticamente comandos para instruções UPDATE e DELETE é baseada na *simultaneidade otimista*, isto é, os registros não são bloqueados para edição e podem ser alterados por outros usuários ou processos a qualquer momento. Como um registro pode ter sido modificado após ter sido retornado da instrução SELECT, mas antes de a instrução UPDATE ou DELETE ser emitida, a instrução UPDATE ou DELETE gerada automaticamente contém uma cláusula WHERE, especificando que uma linha estará atualizada apenas se contiver todos os valores originais e não tiver sido excluída da fonte de dados. Isso é feito para evitar sobrescrever novos dados.
 
> [!NOTE]
> Onde uma atualização gerada automaticamente tentar atualizar uma linha que foi excluída ou que não contém os valores originais localizados no <xref:System.Data.DataSet>, o comando não afetará nenhum registro e uma <xref:System.Data.DBConcurrencyException> será gerada.

Se você desejar que a instrução UPDATE ou DELETE seja concluída independentemente dos valores originais, você deverá definir explicitamente o `UpdateCommand` para o `DataAdapter` e não depender da geração de comando automática.

## <a name="limitations-of-automatic-command-generation-logic"></a>Limitações da lógica de geração automática de comando

As seguintes limitações aplicam-se à geração automática de comando.

### <a name="unrelated-tables-only"></a>Somente tabelas não relacionadas

A lógica de geração automática de comando gera instruções INSERT, UPDATE ou DELETE para tabelas autônomas sem levar em consideração as relações com outras tabelas em uma fonte de dados. Como resultado, você pode encontrar uma falha ao chamar `Update` para enviar alterações para uma coluna que participa em uma restrição de chave estrangeira no banco de dados. Para evitar essa exceção, não use o <xref:System.Data.Common.DbCommandBuilder> para atualizar as colunas envolvidas em uma restrição de chave estrangeira; em vez disso, especifique explicitamente as instruções usadas para executar a operação.

### <a name="table-and-column-names"></a>Nomes de coluna e tabela

A lógica da geração automática de comando poderá falhar se os nomes de colunas ou tabelas contiverem algum caractere especial, como espaços, pontos, aspas ou outros caracteres não alfanuméricos, mesmo se estiver limitado por colchetes. Dependendo do provedor, definir os parâmetros QuotePrefix e QuoteSuffix pode permitir que a lógica de geração processe os espaços, mas não será possível substituir caracteres especiais. Os nomes de tabela totalmente qualificados na forma de *catalog.schema.table* têm suporte.

## <a name="using-the-commandbuilder-to-automatically-generate-an-sql-statement"></a>Usar CommandBuilder para gerar automaticamente uma instrução SQL

Para gerar automaticamente as instruções SQL para um `DataAdapter`, primeiro defina a propriedade `SelectCommand` de `DataAdapter`, em seguida, crie um objeto `CommandBuilder` e especifique como argumento o `DataAdapter` para o qual o `CommandBuilder` gerará instruções SQL automaticamente.

[!code-csharp[SqlCommandBuilder_Create#1](~/../sqlclient/doc/samples/SqlCommandBuilder_Create.cs#1)]

## <a name="modifying-the-selectcommand"></a>Alterando o SelectCommand

Se você alterar o `CommandText` do `SelectCommand` após os comandos INSERT, UPDATE ou DELETE terem sido gerados automaticamente, uma exceção poderá ocorrer. Se o `SelectCommand.CommandText` modificado contiver informações de esquema que forem inconsistentes com o `SelectCommand.CommandText` usado quando os comandos de inserção, atualização ou exclusão foram gerados automaticamente, as chamadas futuras para o método `DataAdapter.Update` poderão tentar acessar as colunas que não existem mais na tabela atual referenciada pelo `SelectCommand` e uma exceção será gerada.

Você pode atualizar as informações de esquema usadas pelo `CommandBuilder` para gerar automaticamente comandos chamando o método `RefreshSchema` do `CommandBuilder`.

Se você quiser saber qual comando foi gerado automaticamente, poderá obter uma referência para comandos gerados automaticamente usando os métodos `GetInsertCommand`, `GetUpdateCommand` e `GetDeleteCommand` do objeto `CommandBuilder` e verificando a propriedade `CommandText` do comando associado.

O exemplo de código a seguir grava no console o comando de atualização que foi gerado automaticamente.

[!code-csharp[SqlCommandBuilder_Create#2](~/../sqlclient/doc/samples/SqlCommandBuilder_Create.cs#2)]

O exemplo a seguir recria a tabela no conjunto de dados. O método **RefreshSchema** é chamado para atualizar os comandos gerados automaticamente com as informações dessa nova coluna.

[!code-csharp[SqlCommandBuilder_Create#3](~/../sqlclient/doc/samples/SqlCommandBuilder_Create.cs#3)]

## <a name="see-also"></a>Confira também

- [Comandos e parâmetros](commands-parameters.md)
- [Executar um comando](execute-command.md)
