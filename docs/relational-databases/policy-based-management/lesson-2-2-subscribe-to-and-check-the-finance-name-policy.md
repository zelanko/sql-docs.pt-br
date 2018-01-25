---
title: "Assinar e verificar a política Nome Financeiro | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance-monitor
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-query-tuning
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
ms.assetid: 126b4c4c-2a1c-4701-a0ad-8de23fbd7306
caps.latest.revision: "24"
author: BYHAM
ms.author: rickbyh
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 247af1bcdb8e3d3293792fb52a5d0e8149ce6ccc
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/18/2018
---
# <a name="lesson-2-2---subscribe-to-and-check-the-finance-name-policy"></a>Lição 2-2 – Assinar e verificar a política Nome Financeiro
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Nesta tarefa, você configurará o banco de dados Finanças para assinar a categoria de política Finanças. Então, você testará a política Nome de Finanças.  
  
### <a name="to-subscribe-to-the-finance-policy-category"></a>Para assinar a categoria de políticas Finanças  
  
1.  Em Pesquisador de Objetos, expanda **Bancos de Dados**, clique com o botão direito do mouse em **Finanças**, aponte para **Políticas**e clique em **Categorias**.  
  
2.  Selecione a caixa de seleção **Assinado** da categoria **Finanças** .  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-test-the-enforcement-of-the-finance-name-policy"></a>Para testar a execução da política Nome de Finanças  
  
1.  Em [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], abra uma janela de consulta. Execute as instruções a seguir que tentam criar uma tabela que viola a política **Nome de Finanças** . A tabela viola a política porque o nome de tabela não começa com as letras **fintbl**.  
  
    ```  
    USE Finance ;  
    GO  
    CREATE TABLE NewTable  
    (Col1 int) ;  
    GO  
  
    ```  
  
    Observe que a política impede que a tabela seja criada e retorne uma mensagem informativa que forneça o nome da política.  
  
2.  Para fornecer um nome válido, modifique o código como se segue e execute a instrução novamente.  
  
    ```  
    USE Finance ;  
    GO  
    CREATE TABLE fintblNewTable  
    (Col1 int) ;  
    GO  
  
    ```  
  
    Neste momento, a tabela é criada.  
  
### <a name="to-apply-the-policy-to-the-whole-server"></a>Para aplicar a política ao servidor inteiro  
  
1.  Atualmente, o banco de dados Finanças se inscreve na categoria de política Finanças. Em muitos casos, é mais fácil aplicar a categoria de política ao servidor inteiro. Em Pesquisador de Objetos, expanda **Gerenciamento**, clique com o botão direito do mouse em **Gerenciamento de Política**e clique em **Gerenciar Categorias**.  
  
2.  Na caixa de diálogo **Gerenciar Categorias de Política** , localize a categoria Finanças e marque a caixa de seleção **Autorizar Assinaturas de Bancos de Dados** para a categoria Finanças.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)] Agora a categoria Finanças se aplica a todos os bancos de dados, mas a condição que você criou restringe a política Nome de Finanças ao banco de dados Finanças. Isso mostra como você pode usar combinações complexas de políticas de destino de forma a aplicá-las corretamente em muitos servidores.  
  
## <a name="summary"></a>Resumo  
Este tutorial mostrou como criar condições do Gerenciamento Baseado em Políticas, políticas e grupos de políticas e como aplicar filtros e verificar a compatibilidade de destinos de Gerenciamento Baseado em Políticas.  
  
## <a name="next"></a>Próximo  
Este tutorial está concluído. Para retornar ao início, clique em [Tutorial: Administrando servidores com o Gerenciamento Baseado em Políticas](../../relational-databases/policy-based-management/tutorial-administering-servers-by-using-policy-based-management.md).  
  
Para obter uma lista de tutoriais, consulte [Tutoriais do SQL Server 2016](../../sql-server/tutorials-for-sql-server-2016.md).  
  
## <a name="see-also"></a>Consulte Também  
[Administrar servidores com Gerenciamento Baseado em Políticas](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)  
  
  
  
