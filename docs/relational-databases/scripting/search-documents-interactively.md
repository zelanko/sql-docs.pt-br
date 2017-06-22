---
title: Pesquisar documentos interativamente | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- interactive searches [SQL Server Management Studio]
- searches [SQL Server Management Studio], interactive
- Query Editor [SQL Server Management Studio], interactive search
ms.assetid: dae65ac5-67af-45c6-a6e0-952fea26d680
caps.latest.revision: 22
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a87a33ea63725ae2db48d61d557ff4bf91704490
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="search-documents-interactively"></a>Pesquisar documentos interativamente
  Usando a caixa de diálogo **Localizar e Substituir** , você pode pesquisar um ou mais arquivos ou janelas abertas, e navegar pelos resultados da pesquisa um a um. Essa técnica permite a revisão de cada correspondência individual da pesquisa no contexto do texto da correspondência. Você também tem a opção de executar operações de localização em massa e revisar correspondências da pesquisa no formato de relatório usando a caixa de diálogo **Localizar e Substituir** .  
  
### <a name="to-search-all-open-documents"></a>Para pesquisar todos os documentos abertos  
  
1.  Abra os itens que você deseja pesquisar.  
  
2.  No menu **Editar** , aponte para **Localizar e Substituir** e depois clique em **QuickFind**.  
  
3.  Na caixa de texto **Localizar e Substituir** , digite o texto da pesquisa.  
  
4.  Na lista **Examinar** , selecione **Todos os Documentos Abertos**.  
  
    > [!NOTE]  
    >  Alguns arquivos abertos talvez não sejam pesquisados quando a opção **Todos os Documentos Abertos** for selecionada. Somente os arquivos abertos atualmente em uma exibição textual, como exibição de Código, são incluídos nas pesquisas. Os arquivos na exibição de designer não são incluídos nas pesquisas.  
  
5.  Selecione opções adicionais de pesquisa para melhorar a precisão da pesquisa.  
  
6.  Clique em **Localizar Próximo** para iniciar a pesquisa e continue clicando em **Localizar Próximo** até o último arquivo ser pesquisado.  
  
 Quando a pesquisa passar do começo ou fim do documento, uma mensagem será exibida na barra de status. Uma caixa de mensagem será exibida quando a pesquisa alcançar o ponto de partida da pesquisa.  
  
#### <a name="to-replace-in-all-active-files-interactively"></a>Para substituir todos os arquivos ativos interativamente  
  
1.  No menu **Editar** , aponte para **Localizar e Substituir**e clique em **QuickReplace**.  
  
2.  Na caixa **Localizar** , digite o texto da pesquisa.  
  
3.  Na caixa **Substituir por** , digite o texto para substituir o texto de pesquisa.  
  
4.  Na lista **Examinar** , selecione **Todos os Documentos Abertos**.  
  
5.  Clique em **Substituir**e continue clicando em **Substituir** até a última correspondência no último arquivo ser substituída. Clique em **Localizar Próximo** para ignorar uma correspondência que você não deseja substituir.  
  
     -ou-  
  
     Escolha **Substituir Tudo** para substituir todas as correspondências. Uma caixa de mensagem é exibida, relacionando o número total de substituições.  
  
 O comando **Substituir Tudo** substitui todas as correspondências da pesquisa, inclusive aquelas ignoradas com o botão **Localizar Próximo** . Para cancelar **Substituir Tudo**, clique em **Desfazer** no menu **Editar** antes de fechar qualquer arquivo.  
  
## <a name="see-also"></a>Consulte também  
 [Pesquisar um documento ativo de forma incremental](../../relational-databases/scripting/search-an-active-document-incrementally.md)   
 [Pesquisar e substituir](../../relational-databases/scripting/search-and-replace.md)   
 [Pesquisar documentos usando listas de resultados](../../relational-databases/scripting/search-documents-using-results-lists.md)   
 [Pesquisar texto com curingas](../../relational-databases/scripting/search-text-with-wildcards.md)   
 [Pesquisar texto com expressões regulares](../../relational-databases/scripting/search-text-with-regular-expressions.md)  
  
  
