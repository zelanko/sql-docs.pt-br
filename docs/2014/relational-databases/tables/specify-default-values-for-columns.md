---
title: Especificar valores padrão para colunas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- columns [SQL Server], defaults
- default values
ms.assetid: 64514aed-b846-407b-992e-cf813f9a1a91
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 14bc2f8445f61cb8cbafb94770c646df4d6a48bb
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52748488"
---
# <a name="specify-default-values-for-columns"></a>Especificar valores padrão para colunas
  Você pode especificar um valor padrão que será inserido na coluna no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Se você não atribuir um valor padrão e o usuário deixar a coluna em branco:  
  
-   Se você definir a opção para permitir valores nulos, será inserido NULL na coluna.  
  
-   Se você não definir a opção para permitir valores nulos, a coluna permanecerá em branco, mas o usuário não poderá salvar a linha até fornecer um valor para a coluna.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para especificar um valor padrão usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e Restrições  
  
-   Se sua entrada no campo **Valor Padrão** substituir um padrão associado (exibido sem parênteses), será solicitado que você desvincule o padrão e substitua-o pelo novo padrão.  
  
-   Para inserir uma cadeia de caracteres de texto, coloque o valor entre aspas simples ('); não utilize aspas duplas ("), pois elas estão reservadas para identificadores entre aspas.  
  
-   Para inserir um padrão numérico, insira o número sem colocá-lo entre aspas.  
  
-   Para inserir um objeto/função, digite o nome do objeto/função sem aspas.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Exige a permissão ALTER na tabela.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-specify-a-default-value-for-a-column"></a>Para especificar um valor padrão para uma coluna  
  
1.  No **Pesquisador de Objetos**, clique com o botão direito do mouse na tabela com as colunas cuja escala você deseja alterar e clique em **Design**.  
  
2.  Selecione a coluna para a qual você deseja especificar o valor padrão.  
  
3.  Na guia **Propriedades da Coluna** , insira o novo valor padrão na propriedade **Valor ou Associação Padrão** .  
  
    > [!NOTE]  
    >  Para inserir um valor numérico padrão, insira o número. Para um objeto ou função insira seu nome. Para um padrão alfanumérico insira o valor entre aspas simples.  
  
4.  No menu **Arquivo**, clique em **Salvar***nome da tabela*.  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
  
#### <a name="to-specify-a-default-value-for-a-column"></a>Para especificar um valor padrão para uma coluna  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    CREATE TABLE dbo.doc_exz ( column_a INT, column_b INT) ;  
    GO  
    INSERT INTO dbo.doc_exz (column_a)VALUES ( 7 ) ;  
    GO  
    ALTER TABLE dbo.doc_exz  
    ADD CONSTRAINT col_b_def  
    DEFAULT 50 FOR column_b ;  
    GO  
  
    ```  
  
 Para obter mais informações, veja [ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql).  
  
###  <a name="TsqlExample"></a>  
