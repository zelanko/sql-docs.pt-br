---
title: Abrir projetos do controle de origem | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- projects [SQL Server Management Studio], opening
- opening projects
ms.assetid: 942f93a3-e264-4ec4-ba72-a28e0509a527
caps.latest.revision: 21
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 0963ef46d2378cd23eae5c1cec23b76c0919e3d1
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36120847"
---
# <a name="open-projects-from-source-control"></a>Abrir projetos no controle do código-fonte
  Você pode usar o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] para abrir projetos diretamente do controle doe código-fonte. Quando você fizer isso, o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] recuperará a versão mais recente do projeto e a copiará em seu disco local. O ambiente do [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] também cria automaticamente uma solução para o projeto.  
  
 Depois de abrir um projeto a partir do controle do código-fonte, você poderá fazer check-out e modificar os arquivos de projeto.  
  
> [!NOTE]  
>  O procedimento a seguir só deve ser usado uma vez. Depois disso, você deve abrir o projeto como qualquer outro projeto (clicando **arquivo**, **abrir**e, em seguida, **projeto**).  
  
### <a name="to-open-a-project-from-source-control"></a>Para abrir um projeto no controle do código-fonte  
  
1.  Sobre o **arquivo** , aponte para **controle de origem**e clique em **abrir do controle de origem**.  
  
2.  Se solicitado, faça logon no [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual SourceSafe.  
  
3.  No **criar projeto local do SourceSafe** caixa de diálogo caixa, abra a pasta que contém o projeto para ser aberto.  
  
4.  O **criar um novo projeto na pasta** caixa alterações para identificar o diretório local no qual o projeto será criado. Se você deseja colocar o projeto em um diretório diferente, digite o caminho para o diretório ou use o **procurar** botão para localizar o diretório em seu disco local.  
  
5.  No **criar um novo projeto na caixa pasta**, verifique se a pasta correta é exibida e, em seguida, clique em **Okey**.  
  
6.  No **abrir solução** caixa de diálogo, selecione o projeto que você deseja abrir e clique em **abrir**.  
  
## <a name="see-also"></a>Consulte também  
 [Abrir soluções e projetos de controle de origem](../../2014/database-engine/open-solutions-and-projects-from-source-control.md)   
 [Abrir soluções no controle do código-fonte](../../2014/database-engine/open-solutions-from-source-control.md)  
  
  