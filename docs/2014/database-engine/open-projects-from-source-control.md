---
title: Abrir projetos do controle do código-fonte | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- projects [SQL Server Management Studio], opening
- opening projects
ms.assetid: 942f93a3-e264-4ec4-ba72-a28e0509a527
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ec14f86b283fa8ccbc037feec4a8a54983126403
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62774950"
---
# <a name="open-projects-from-source-control"></a>Abrir projetos no controle do código-fonte
  Você pode usar o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] para abrir projetos diretamente do controle doe código-fonte. Quando você fizer isso, o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] recuperará a versão mais recente do projeto e a copiará em seu disco local. O ambiente do [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] também cria automaticamente uma solução para o projeto.  
  
 Depois de abrir um projeto a partir do controle do código-fonte, você poderá fazer check-out e modificar os arquivos de projeto.  
  
> [!NOTE]  
>  O procedimento a seguir só deve ser usado uma vez. Depois disso, você deve abrir o projeto como qualquer outro projeto (clicando em **arquivo**, **abrir**e, em seguida, **projeto**).  
  
### <a name="to-open-a-project-from-source-control"></a>Para abrir um projeto no controle do código-fonte  
  
1.  No menu **arquivo** , aponte para **controle do código-fonte**e clique em **Abrir do controle do código-fonte**.  
  
2.  Se solicitado, faça logon no [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual SourceSafe.  
  
3.  Na caixa de diálogo **criar projeto local do SourceSafe** , abra a pasta que contém o projeto a ser aberto.  
  
4.  A caixa **criar um novo projeto na pasta** é alterada para identificar o diretório local no qual o projeto será criado. Se você quiser colocar o projeto em um diretório diferente, digite o caminho para o diretório ou use o botão **procurar** para localizar o diretório no disco local.  
  
5.  Na **caixa criar um novo projeto na pasta**, verifique se a pasta correta é exibida e clique em **OK**.  
  
6.  Na caixa de diálogo **Abrir solução** , selecione o projeto que você deseja abrir e clique em **abrir**.  
  
## <a name="see-also"></a>Consulte Também  
 [Abrir soluções e projetos do controle do código-fonte](../../2014/database-engine/open-solutions-and-projects-from-source-control.md)   
 [Abrir soluções no controle do código-fonte](../../2014/database-engine/open-solutions-from-source-control.md)  
  
  
