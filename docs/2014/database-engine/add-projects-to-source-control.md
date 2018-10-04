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
manager: craigg
ms.openlocfilehash: c0936af9b97d08c6bcd5033e61d9fa1c9153272e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48074465"
---
# <a name="add-projects-to-source-control"></a>Adicionar projetos ao controle do código-fonte
  As soluções do [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] podem hospedar vários projetos de script. Como você adiciona um projeto ao controle do código-fonte depende do fato de a solução a que o projeto pertence estar sob controle do código-fonte. Se a solução estiver sob controle do código-fonte, fazer check-in da solução adicionará automaticamente o projeto ao controle do código-fonte. Para obter mais informações sobre como fazer check-in de soluções, consulte [verificar nos arquivos](../../2014/database-engine/check-in-files.md).  
  
 Se a solução a que esse projeto pertence não estiver sob controle do código-fonte, você poderá adicionar essa solução ao controle, o que adicionará automaticamente os projetos da solução. Para obter mais informações sobre como adicionar soluções ao controle de origem, consulte [adicionar soluções ao controle do código-fonte](../../2014/database-engine/add-solutions-to-source-control.md).  
  
 Se você não quiser adicionar a solução ao controle de origem, você pode usar o **Adicionar seleção ao controle do código-fonte** comando para adicionar o projeto manualmente.  
  
 Os objetos de banco de dados não são protegidos diretamente pelo provedor de controle do código-fonte, mas você pode criar scripts de objetos de banco de dados e salvá-los sob o controle do código-fonte.  
  
### <a name="to-add-a-project-to-source-control"></a>Para adicionar um projeto ao controle do código-fonte  
  
1.  No Gerenciador de Soluções, selecione um projeto.  
  
2.  Sobre o **arquivo** , aponte para **controle do código-fonte**e, em seguida, clique em **adicionar projetos selecionados ao controle do código-fonte**.  
  
    > [!NOTE]  
    >  Se você usar o **adicionar projetos selecionados ao controle do código-fonte** de comando para adicionar um projeto que pertence a uma solução de controle do código-fonte, você será solicitado se você deseja adicionar o projeto como uma subpasta da solução de controle do código-fonte ou para adicionar o projeto como uma pasta separada.  
  
3.  Se solicitado, faça logon em seu provedor de controle do código-fonte.  
  
4.  O **adicionar ao projeto do SourceSafe** caixa de diálogo é exibida. O nome do seu projeto aparece na **projeto** caixa.  
  
5.  No **pastas** lista, abra a pasta onde você deseja colocar seu projeto. Como alternativa, você pode clicar **Create** para criar uma pasta com o nome exibido na **projeto** caixa.  
  
## <a name="see-also"></a>Consulte também  
 [Adicionar soluções e projetos ao controle do código-fonte](../../2014/database-engine/add-solutions-and-projects-to-source-control.md)  
  
  
