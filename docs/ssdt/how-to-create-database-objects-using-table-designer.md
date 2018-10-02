---
title: Como criar objetos de banco de dados usando o Designer de Tabela | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- sql.data.tools.design.table.scriptpanel
- sql.data.tools.design.table.context.view
ms.assetid: 9c9479c1-9bfc-4039-837e-e53fce67723d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7001819d4603c392b034d54fffaee7b901400c20
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47779274"
---
# <a name="how-to-create-database-objects-using-table-designer"></a>Como: Criar objetos de banco de dados usando o Designer de Tabela
Além de ser semelhante visualmente ao SSMS, no novo nó **SQL Server** do **Pesquisador de Objetos do SQL Server** você pode criar novos objetos usando menus contextuais que funcionam como suas contrapartes do SSMS.  
  
Por exemplo, você pode criar um novo banco de dados no nó **Bancos de Dados**. De maneira semelhante, você pode selecionar um banco de dados específico e criar ou editar definições de tabela e seus objetos de programação relacionados rapidamente usando o novo Designer de Tabela. Do Designer de Tabela, você pode alternar para um painel de script que permite editar diretamente o script que define esta tabela.  
  
### <a name="to-create-a-new-database"></a>Para criar um novo banco de dados  
  
1.  No **Pesquisador de Objetos do SQL Server**, no nó **SQL Server**, expanda sua instância de servidor conectada.  
  
2.  Clique com o botão direito do mouse no nó **Bancos de Dados** e selecione **Adicionar Novo Banco de Dados**.  
  
3.  Renomeie o novo banco de dados como **Trade**.  
  
### <a name="to-create-new-tables-using-the-table-designer"></a>Para criar novas tabelas usando o Designer de Tabela  
  
1.  Expanda o nó **Trade** criado recentemente. Clique com o botão direito do mouse no nó **Tabelas** e selecione **Adicionar Nova Tabela**.  
  
2.  O Designer de Tabela abre em uma segunda janela. O designer é composto por Grade de Colunas, Painel de Script e Painel Contexto. A Grade de Colunas lista todas as colunas na tabela. Nós revisitaremos outros componentes do designer em procedimentos posteriores.  
  
3.  No Painel de Script, renomeie a nova tabela como `Suppliers`. Especificamente, substitua  
  
    ```  
    CREATE TABLE [dbo].[Table1]  
    ```  
  
    por  
  
    ```  
    CREATE TABLE [dbo].[Suppliers]  
    ```  
  
4.  Clique na linha vazia na Grade de Colunas para adicionar uma nova coluna à tabela.  Insira **CompanyName** para o campo **Nome**, **nvarchar (128)** para **Tipo de Dados** e desmarque o campo **Permitir Nulos**. À medida que você se move pelas guias nos campos, observe que o Painel de Script é atualizado imediatamente.  
  
5.  Adicione outra nova coluna. Insira **Endereço** para o campo **Nome**, **nvarchar (MAX)** para **Tipo de Dados** e desmarque o campo **Permitir Nulos**.  
  
    > [!WARNING]  
    > Quando você estiver editando objetos de um banco de dados conectado, não os salve em sua unidade local. Para salvar corretamente suas alterações no banco de dados, execute as etapas no próximo procedimento [Como atualizar um banco de dados conectados com o Power Buffer](../ssdt/how-to-update-a-connected-database-with-power-buffer.md).  
  
6.  Repita as etapas acima para criar outra tabela chamada **Cliente**. Dessa vez, adicione as colunas seguintes à tabela Cliente usando a Grade de Colunas. E lembre-se de alterar o script de forma que o nome da tabela seja `[dbo].[Customer]`.  
  
    |Nome|Tipo de Dados|**Permitir Nulos**|  
    |--------|-------------|-------------------|  
    |ID|INT|desmarcado|  
    |Nome|nvarchar (128)|desmarcado|  
  
7.  Crie mais uma tabela chamada **Produtos**. Adicione as colunas seguintes à tabela Produtos usando a Grade de Colunas. E lembre-se de alterar o script de forma que o nome da tabela seja `[dbo].[Products]`.  
  
    |Nome|Tipo de Dados|**Permitir Nulos**|  
    |--------|-------------|-------------------|  
    |ID|INT|desmarcado|  
    |Nome|nvarchar (128)|desmarcado|  
    |ShelfLife|INT|verificado|  
    |SupplierId|INT|verificado|  
    |CustomerId|INT|verificado|  
  
### <a name="to-create-a-new-check-constraint-using-the-table-designer"></a>Para criar uma nova restrição de verificação usando o Designer de Tabela  
  
1.  O Painel Contexto do Designer de Tabela dará uma exibição lógica da definição de tabela (Chaves, Índices, Restrições, Gatilhos, etc.) e permite que você selecione um objeto para realçar seus relacionamentos em colunas individuais.  
  
    Para a tabela Produtos, clique com o botão direito do mouse no nó **Verificar Restrições** no Painel Contexto do designer de tabela e selecione **Adicionar Nova Restrição de Verificação**.  
  
2.  Observe que a contagem do nó é incrementada automaticamente em 1.  
  
3.  Clique no Painel de Script e substitua a definição padrão da restrição pelo seguinte.  
  
    ```  
    CONSTRAINT [CK_Products_ShelfLife] CHECK ([ShelfLife] <5),  
    ```  
  
    Esta restrição limitará o valor de ShelfLife para uma linha para ser menor que 5.  
  
### <a name="to-create-new-foreign-key-references-using-the-table-designer"></a>Para criar novas referências de chave estrangeira usando o Designer de Tabela  
  
1.  Para a tabela Produtos, clique com o botão direito do mouse no nó **Chaves Estrangeiras** no Painel Contexto e selecione **Adicionar Nova Chave Estrangeira**.  
  
2.  Observe que a contagem do nó é incrementada automaticamente em 1.  
  
3.  Clique no Painel de Script e substitua a definição padrão da referência de chave estrangeira pelo seguinte.  
  
    ```  
    CONSTRAINT [FK_Products_SupplierId] FOREIGN KEY ([SupplierId]) REFERENCES [dbo].[Suppliers] ([Id]),  
    ```  
  
4.  Repita as etapas acima para adicionar outra referência de chave estrangeira à tabela Produtos. Dessa vez, substitua a definição padrão pelo seguinte.  
  
    ```  
    CONSTRAINT [FK_Products_CustomerId] FOREIGN KEY ([CustomerId]) REFERENCES [dbo].[Customer] ([Id])  
    ```  
  
## <a name="see-also"></a>Consulte Também  
[Gerenciar tabelas, relações e corrigir erros](../ssdt/manage-tables-relationships-and-fix-errors.md)  
  
