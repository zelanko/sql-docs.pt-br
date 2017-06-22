---
title: Modificar colunas (Mecanismo de Banco de Dados) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- modifying data types
- column data types [SQL Server]
- data types [SQL Server], columns
ms.assetid: b67b95c5-61ef-4bd8-9a3e-1640eb7583ac
caps.latest.revision: 16
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 736b83dffa241040cf08e7f7d9410eaab80649af
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="modify-columns-database-engine"></a>Modificar colunas (Mecanismo de Banco de Dados)
[!INCLUDE[tsql-appliesto-ss2016-all_md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  Você pode modificar o tipo de dados de uma coluna no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
> [!WARNING]  
>  Modificar o tipo de dados de uma coluna que já contenha dados pode resultar na perda permanente de dados quando os dados existentes forem convertidos para o novo tipo. Além disso, códigos e aplicativos que dependem da coluna modificada podem falhar. Isso inclui consultas, exibições, procedimentos armazenados, funções definidas pelo usuário e aplicativos clientes. Observe que essas falhas ocorrerão em cascata. Por exemplo, um procedimento armazenado que chama uma função definida pelo usuário que dependa da coluna modificada pode falhar. Considere cuidadosamente todas as alterações que você pretende realizar em uma coluna antes fazê-las.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para modificar o tipo de dados de uma coluna usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Exige a permissão ALTER na tabela.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-modify-the-data-type-of-a-column"></a>Para modificar o tipo de dados de uma coluna  
  
1.  No **Pesquisador de Objetos**, clique com o botão direito do mouse na tabela com as colunas cuja escala você deseja alterar e clique em **Design**.  
  
2.  Selecione a coluna cujo tipo de dados você pretende modificar.  
  
3.  Na guia **Propriedades da Coluna** , clique na célula de grade da propriedade **Tipo de Dados** e selecione o novo tipo de dados na lista suspensa.  
  
4.  No menu **Arquivo** , clique em **Salvar***table name*.  
  
> [!NOTE]  
>  Quando o tipo de dados de uma coluna é modificado, o Designer de Tabela aplica o comprimento padrão do tipo de dados que foi selecionado, até mesmo quando outro já tiver sido especificado. Defina sempre o comprimento do tipo de dados do valor desejado após especificar o tipo de dados.  
  
> [!WARNING]  
>  Se você tentar modificar o tipo de dados de uma coluna relacionada a outras tabelas, o Designer de Tabela solicitará que você confirme se a alteração deve ser feita nas colunas das outras tabelas também.  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
  
#### <a name="to-modify-the-data-type-of-a-column"></a>Para modificar o tipo de dados de uma coluna  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    CREATE TABLE dbo.doc_exy (column_a INT ) ;  
    GO  
    INSERT INTO dbo.doc_exy (column_a) VALUES (10) ;  
    GO  
    ALTER TABLE dbo.doc_exy ALTER COLUMN column_a DECIMAL (5, 2) ;  
    GO  
  
    ```  
  
 Para obter mais informações, veja [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
  
  
