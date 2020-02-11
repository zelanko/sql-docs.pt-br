---
title: Criar a política Nome Financeiro | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 56b2c852-fd69-4cd2-9b5d-977467b94fd9
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a4484f9ccb76ea31c95a5392570e18df2c4b0ff5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67792910"
---
# <a name="create-the-finance-name-policy"></a>Criar a política Nome Financeiro
  Nesta tarefa, você criará um banco de dados chamado Finance e, em seguida, criará uma condição que exige que todas as tabelas comecem com as letras **fintbl**. Em seguida, você criará uma política e uma categoria de políticas para impor um padrão de nomenclatura para as tabelas no banco de dados Finanças.  
  
### <a name="to-create-the-finance-database"></a>Para criar o banco de dados Finanças  
  
1.  Em [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], abra uma janela de consulta e execute a instrução a seguir:  
  
    ```  
    CREATE DATABASE Finance ;  
    GO  
    ```  
  
2.  No Pesquisador de Objetos, clique em **Bancos de Dados**e, em seguida, pressione F5 para atualizar a lista de bancos de dados.  
  
### <a name="to-create-the-finance-tables-condition"></a>Para criar a condição Tabelas de Finanças  
  
1.  No Pesquisador de Objetos, expanda **Gerenciamento**, **Gerenciamento de Política**, clique com o botão direito do mouse em **Condições**e clique em **Nova Condição**.  
  
2.  Na caixa de diálogo **Criar Nova Condição** , na caixa **Nome** , digite **Tabelas de Finanças**.  
  
3.  Na lista **Faceta** , selecione **Nome com Diversas Partes**.  
  
4.  Na área **expressão** , na caixa **campo** , selecione ** \@nome**; na caixa **operador** , selecione **like**; e na caixa **valor** , digite **' fintbl% '** para forçar todos os nomes de tabela a começar com as letras **fintbl**.  
  
5.  Na página **Descrição** , digite **Os nomes da tabela de Finanças deve começar com fintbl**e, em seguida, clique em **OK** para criar a condição.  
  
### <a name="to-create-the-finance-name-policy"></a>Para criar a política Nome Financeiro  
  
1.  No Pesquisador de Objetos, clique com o botão direito do mouse em **Políticas**e clique em **Nova Política**.  
  
2.  Na caixa de diálogo **Criar Nova Política** , na caixa **Nome** , digite **Nome de Finanças**.  
  
3.  Na lista **Verificar condição** , selecione **Tabelas de Finanças**. Isso está na área **Nome com Diversas Partes** .  
  
4.  Na área **Contra** você verá uma lista dos objetos de banco de dados que poderiam aplicar essa política. Selecione a caixa de seleção para **Cada Tabela**.  
  
5.  Na área **Cada Banco de Dados** , expanda **Tudo**e clique em **Nova condição**.  
  
6.  Na caixa de diálogo **Criar Nova Condição** , na caixa **Nome** , digite **Banco de Dados de Finanças**.  
  
7.  Na caixa **expressão** , conclua a expressão para incluir ** \@Name = ' Finance '** e clique em **OK** para fechar a página condição.  
  
    > [!NOTE]  
    >  Você poderia ter a guia fora da caixa **Valor** para habilitar o botão **OK** .  
  
8.  Na lista **Modo de Avaliação** , selecione **Ao alterar: impedir**. Isso aplicará a política criando um gatilho de banco de dados no banco de dados Finanças.  
  
9. Selecione a lista **Habilitado** . (A caixa **Habilitado** não se aplica a políticas **Sob Demanda** .)  
  
10. Na lista **Restrição de servidor** , selecione **Nenhum**.  
  
11. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-create-the-finance-policy-category"></a>Para criar a categoria da política Finanças  
  
1.  Em Pesquisador de Objetos, expanda **Gerenciamento**, clique com o botão direito do mouse em **Gerenciamento de Política**e clique em **Gerenciar Categorias**.  
  
2.  Na caixa de diálogo **gerenciar categorias de política** , em **nome**, `Finance` digite na caixa em branco e desmarque autorizar **assinaturas de banco de dados**. A opção**Autorizar Assinaturas de Banco de Dados** forçará todos os bancos de dados na instância a assinarem as políticas que pertencem a esta categoria de política. Para esta lição, somente o banco de dados Finanças deve assinar a política Nome Financeiro.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Assinar e verificar a política Nome Financeiro](lesson-2-2-subscribe-to-and-check-the-finance-name-policy.md)  
  
  
