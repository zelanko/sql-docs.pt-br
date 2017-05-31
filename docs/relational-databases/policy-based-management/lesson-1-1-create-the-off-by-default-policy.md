---
title: "Criar a política desativada por padrão | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-query-tuning
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: 98fde3c5-297c-4d95-981e-95700bbf5ccd
caps.latest.revision: 28
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: ad1ef04caea4fc15cc53fced05ab5861d54ad7eb
ms.contentlocale: pt-br
ms.lasthandoff: 04/11/2017

---
# <a name="lesson-1-1---create-the-off-by-default-policy"></a>Lição 1-1 – Criar a política desativada por padrão
Esta tarefa cria uma condição chamada Correio Desativado que é baseada na faceta Configuração da Área da Superfície. Então, cria uma política chamada Desativada por Padrão.  
  
### <a name="to-create-the-mail-off-condition"></a>Para criar a condição Correio Desativado  
  
1.  Em Pesquisador de Objetos, expanda **Gerenciamento**, **Gerenciamento de Política**, **Facetas**, clique com o botão direito do mouse em **Configuração da Área da Superfície**e clique em **Nova Condição**.  
  
2.  Na caixa de diálogo **Criar Nova Condição** , na caixa **Nome** , digite **Correspondência Desativada**.  
  
3.  Na caixa **Faceta** , confirme se a faceta **Configuração da Área da Superfície** está selecionada.  
  
4.  Na caixa de diálogo **Expressão** , na caixa **Campo** , selecione **@DatabaseMailEnabled**, na caixa **Operador** , selecione **=**e, em **Valor** , selecione **False**.  
  
5.  Na página **Descrição** , digite uma descrição da condição e clique em **OK** para criar a condição.  
  
### <a name="to-create-the-off-by-default-policy"></a>Para criar a política Desativada por Padrão  
  
1.  Em Pesquisador de Objetos, clique com o botão direito do mouse em **Configuração da Área da Superfície**e clique em **Nova Política**.  
  
2.  Na caixa de diálogo **Criar Nova Política** , na caixa **Nome** , digite **Desativada por Padrão**.  
  
3.  Deixe a caixa de seleção **Habilitada** desmarcada. A caixa de seleção **Habilitada** se aplica às políticas automatizadas, e essa política será executada sob demanda.  
  
4.  Na caixa de seleção **Verificar condição** , role a tela para baixo até a área **Configuração da Área da Superfície** e selecione **Correspondência Desativada** como condição de verificação.  
  
5.  A caixa **Em relação aos destinos** ficará em branco porque esta é uma política com escopo no servidor.  
  
6.  Na caixa de seleção **Modo de Avaliação** , selecione **Sob demanda** como modo de avaliação.  
  
7.  Na caixa de seleção **Restrição de servidor** , selecione **Nenhuma**.  
  
8.  Na página **Descrição** , digite uma descrição para a política.  
  
9. Você pode fornecer um hiperlink a uma página da Web para suas políticas na área **Hiperlink de ajuda adicional** . Na caixa **Texto a ser exibido** , digite o texto que aparecerá no hiperlink.  
  
10. Na caixa **Endereço** , digite um hiperlink para uma página Ajuda, como a home page do departamento de TI de sua empresa.  
  
11. Para confirmar o endereço abrindo a página da Web, clique em **Testar Link**.  
  
12. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
[Configurar um servidor para executar a política desativada por padrão](../../relational-databases/policy-based-management/lesson-1-2-configure-a-server-to-run-the-off-by-default-policy.md)  
  
  
  

