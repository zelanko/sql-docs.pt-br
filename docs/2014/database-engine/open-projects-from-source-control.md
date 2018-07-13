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
ms.topic: conceptual
helpviewer_keywords:
- projects [SQL Server Management Studio], opening
- opening projects
ms.assetid: 942f93a3-e264-4ec4-ba72-a28e0509a527
caps.latest.revision: 21
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 204b3a4419ffe486907e8a60bcf7fd229c78192e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37277252"
---
# <a name="open-projects-from-source-control"></a>Abrir projetos no controle do código-fonte
  Você pode usar o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] para abrir projetos diretamente do controle doe código-fonte. Quando você fizer isso, o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] recuperará a versão mais recente do projeto e a copiará em seu disco local. O ambiente do [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] também cria automaticamente uma solução para o projeto.  
  
 Depois de abrir um projeto a partir do controle do código-fonte, você poderá fazer check-out e modificar os arquivos de projeto.  
  
> [!NOTE]  
>  O procedimento a seguir só deve ser usado uma vez. Depois disso, você deve abrir o projeto como qualquer outro projeto (clicando **arquivo**, **abra**e então **projeto**).  
  
### <a name="to-open-a-project-from-source-control"></a>Para abrir um projeto no controle do código-fonte  
  
1.  Sobre o **arquivo** , aponte para **controle do código-fonte**e clique em **abrir do controle de origem**.  
  
2.  Se solicitado, faça logon no [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual SourceSafe.  
  
3.  No **criar projeto local no SourceSafe** caixa de diálogo caixa, abra a pasta que contém o projeto para abrir.  
  
4.  O **criar um novo projeto na pasta** caixa muda para identificar o diretório local em que o projeto será criado. Se você deseja colocar o projeto em um diretório diferente, digite o caminho para o diretório ou use o **procurar** botão para localizar o diretório em seu disco local.  
  
5.  No **criar um novo projeto na caixa pasta**, verifique se a pasta correta é exibida e, em seguida, clique em **Okey**.  
  
6.  No **Open Solution** diálogo caixa, selecione o projeto que você deseja abrir e, em seguida, clique em **abrir**.  
  
## <a name="see-also"></a>Consulte também  
 [Abrir soluções e projetos de controle de origem](../../2014/database-engine/open-solutions-and-projects-from-source-control.md)   
 [Abrir soluções no controle do código-fonte](../../2014/database-engine/open-solutions-from-source-control.md)  
  
  
