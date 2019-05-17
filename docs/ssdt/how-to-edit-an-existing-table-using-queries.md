---
title: 'Como fazer: editar uma tabela existente usando consultas | Microsoft Docs'
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 58f4de8e-97b4-4bcb-953f-f3d428432491
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 2c988efd63982b2dc5ebd8e73f2291a19b3b9b76
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65090232"
---
# <a name="how-to-edit-an-existing-table-using-queries"></a>Como fazer: Editar uma tabela existente usando consultas
Você pode editar a definição de uma tabela ou de seus dados gravando uma consulta Transact\-SQL. Para exibir ou inserir dados em uma tabela visualmente, use o Editor de Dados como descrito em [Desenvolvimento de banco de dados conectado](../ssdt/connected-database-development.md).  
  
> [!WARNING]  
> Os procedimentos a seguir usam entidades criadas em procedimentos anteriores na seção [Desenvolvimento de banco de dados conectado](../ssdt/connected-database-development.md).  
  
### <a name="to-edit-the-definition-of-an-existing-table"></a>Para editar a definição de uma tabela existente.  
  
1.  Expanda o nó **Tabelas** do banco de dados **Trade** no **Pesquisador de Objetos do SQL Server** e clique com o botão direito do mouse em **dbo.Suppliers**.  
  
2.  Selecione **Exibir Designer** para exibir o esquema de tabela no Designer de Tabela.  
  
3.  Marque a caixa **Permitir Valores Nulos** para a coluna **Endereço**. Observe que o código correspondente no painel de script é alterado imediatamente para `NULL`.  
  
4.  Atualize o banco de dados seguindo as etapas no tópico [Como atualizar um banco de dados conectado com o Power Buffer](../ssdt/how-to-update-a-connected-database-with-power-buffer.md).  
  
### <a name="to-populate-data-in-new-tables-using-a-transact-sql-query"></a>Para popular dados em novas tabelas usando uma consulta Transact\-SQL  
  
1.  Clique com o botão direito do mouse no nó do banco de dados **Trade** e selecione **Nova Consulta**.  
  
2.  No painel de script, cole no seguinte código.  
  
    ```  
    insert into dbo.Suppliers values  
    (1, 'NorthWind Traders', 'Seattle, WA'),  
    (2, 'Contoso', 'Tacoma, WA')  
    GO  
  
    insert dbo.Customer values  
    (1, 'Fourth Coffee')  
    GO  
  
    insert dbo.Products values  
    (1, 'Apples', 0, 1, 1),  
    (2, 'Instant Coffee', 1, 2, 1)  
    GO  
    ```  
  
3.  Clique no botão **Executar Consulta** para executar essa consulta. Os seguintes no painel **Mensagem** indicam que as linhas são adicionadas às tabelas com êxito.  
  
**(2 linhas afetadas) (1 linha afetada) (2 linhas afetadas)**  
  
4.  Substitua o código no painel de script pelo seguinte e execute a consulta. Isto tentará adicionar uma nova linha à tabela `Products` com um `ShelfLife` de 6.  
  
    ```  
    insert dbo.Products values  
    (3, 'Potato Chips', 6, 1, 1)  
    GO  
    ```  
  
5.  O painel **Mensagem** indica que a instrução `INSERT` está em conflito com sua restrição de verificação existente, que limita o valor de `ShelfLife` para ser menor que 5. A tabela Produtos não é atualizada devido à instrução que falha uma restrição existente.  
  
6.  Altere o código para o seguinte e execute a consulta novamente. Observe que a linha é atualizada com êxito dessa vez.  
  
    ```  
    insert dbo.Products values  
    (3, 'Potato Chips', 2, 1, 1)  
    GO  
    ```  
  
## <a name="see-also"></a>Consulte Também  
[Gerenciar tabelas, relações e corrigir erros](../ssdt/manage-tables-relationships-and-fix-errors.md)  
[Usar o Editor Transact-SQL para editar e executar scripts](../ssdt/use-transact-sql-editor-to-edit-and-execute-scripts.md)  
  
