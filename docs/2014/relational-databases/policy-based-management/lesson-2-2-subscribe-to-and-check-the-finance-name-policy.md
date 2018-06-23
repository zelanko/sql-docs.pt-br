---
title: Assinar e verificar a política Nome Financeiro | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 126b4c4c-2a1c-4701-a0ad-8de23fbd7306
caps.latest.revision: 24
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: d6387825abc2b2eb3426bbbd19f05674615f9e7a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36013543"
---
# <a name="subscribe-to-and-check-the-finance-name-policy"></a>Assinar e verificar a política Nome Financeiro
  Nesta tarefa, você configurará o banco de dados Finanças para assinar a categoria de políticas Finanças. Então, você testará a política Nome de Finanças.  
  
### <a name="to-subscribe-to-the-finance-policy-category"></a>Para assinar a categoria de políticas Finanças  
  
1.  No Pesquisador de objetos, expanda **bancos de dados**, clique com botão direito `Finance`, aponte para **políticas**e, em seguida, clique em **categorias**.  
  
2.  Selecione o **assinado** caixa de seleção para o `Finance` categoria.  
  
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
 Este tutorial está concluído. Para retornar ao início, clique em [Tutorial: Administrando servidores com o Gerenciamento Baseado em Políticas](tutorial-administering-servers-by-using-policy-based-management.md).  
  
 Para obter uma lista de tutoriais, consulte [tutoriais para SQL Server 2014](../../tutorials/tutorials-for-sql-server-2014.md).  
  
## <a name="see-also"></a>Consulte também  
 [Administrar servidores com Gerenciamento Baseado em Políticas](administer-servers-by-using-policy-based-management.md)  
  
  