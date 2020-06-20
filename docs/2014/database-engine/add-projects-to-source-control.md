---
title: Adicionar projetos ao controle do código-fonte | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- adding projects
- projects [SQL Server Management Studio], adding
ms.assetid: fd4616b2-a564-4a66-ac53-d1f5cba213c2
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: de32cbecdf132f1c881ab9fe5637af3a5c6cd400
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84937347"
---
# <a name="add-projects-to-source-control"></a>Adicionar projetos ao controle do código-fonte
  As soluções do [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] podem hospedar vários projetos de script. Como você adiciona um projeto ao controle do código-fonte depende do fato de a solução a que o projeto pertence estar sob controle do código-fonte. Se a solução estiver sob controle do código-fonte, fazer check-in da solução adicionará automaticamente o projeto ao controle do código-fonte. Para obter mais informações sobre como fazer check-in de soluções, consulte [check in Files](../../2014/database-engine/check-in-files.md).  
  
 Se a solução a que esse projeto pertence não estiver sob controle do código-fonte, você poderá adicionar essa solução ao controle, o que adicionará automaticamente os projetos da solução. Para obter mais informações sobre como adicionar soluções ao controle do código-fonte, consulte [Adicionar soluções ao controle do código-fonte](../../2014/database-engine/add-solutions-to-source-control.md).  
  
 Se você não quiser adicionar a solução ao controle do código-fonte, poderá usar o comando **Adicionar seleção ao controle do código-fonte** para adicionar o projeto manualmente.  
  
 Os objetos de banco de dados não são protegidos diretamente pelo provedor de controle do código-fonte, mas você pode criar scripts de objetos de banco de dados e salvá-los sob o controle do código-fonte.  
  
### <a name="to-add-a-project-to-source-control"></a>Para adicionar um projeto ao controle do código-fonte  
  
1.  No Gerenciador de Soluções, selecione um projeto.  
  
2.  No menu **arquivo** , aponte para **controle do código-fonte**e, em seguida, clique em **adicionar projetos selecionados ao controle do código-fonte**.  
  
    > [!NOTE]  
    >  Se você usar o comando **adicionar projetos selecionados ao controle do código-fonte** para adicionar um projeto que pertence a uma solução controlada por origem, será perguntado se deseja adicionar o projeto como uma subpasta da solução controlada por origem ou adicionar o projeto como uma pasta separada.  
  
3.  Se solicitado, faça logon em seu provedor de controle do código-fonte.  
  
4.  A caixa de diálogo **Adicionar ao projeto SourceSafe** é exibida. O nome do seu projeto é exibido na caixa **projeto** .  
  
5.  Na lista **pastas** , abra a pasta onde você deseja posicionar o projeto. Como alternativa, você pode clicar em **criar** para criar uma pasta com o nome exibido na caixa **projeto** .  
  
## <a name="see-also"></a>Consulte Também  
 [Adicionar soluções e projetos ao controle do código-fonte](../../2014/database-engine/add-solutions-and-projects-to-source-control.md)  
  
  
