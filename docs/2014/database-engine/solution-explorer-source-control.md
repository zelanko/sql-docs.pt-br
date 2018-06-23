---
title: Controle de origem do Solution Explorer | Microsoft Docs
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
- Visual SourceSafe
- SQL Server Management Studio [SQL Server], source control services
- source-controlled files [SQL Server]
- source controls [SQL Server Management Studio], services
- version control services [SQL Server]
- file source control services [SQL Server]
- VSS [Visual SourceSafe]
ms.assetid: 6373adb8-3d81-4945-a9fc-1d0d5799d29a
caps.latest.revision: 28
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 7165143ad238bbbeda14ac91f214f1410082beb2
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36012067"
---
# <a name="solution-explorer-source-control"></a>Controle do código-fonte do Gerenciador de Soluções
  [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] Gerenciador de soluções pode ser integrado em um sistema de controle do código-fonte separado. Quando uma solução ou projeto é integrado em um sistema de controle do código-fonte, você pode controlar o acesso ao arquivo e a versão para os scripts e consultas em seus projetos.  
  
## <a name="solution-and-project-source-control"></a>Solução e projeto no controle do código-fonte  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../includes/ssnotedepfutureavoid-md.md)]  
  
 O controle do código-fonte recorre a um sistema em que uma parte central do software de servidor armazena e rastreia versões de arquivos e também controla o acesso a eles. Um sistema de controle do código-fonte típico inclui um provedor de controle do código-fonte, e dois ou mais clientes de controle do código-fonte. O [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] pode ser integrado a um serviço de controle do código-fonte. Isso significa que você pode usar a ferramenta como um cliente de seu provedor de controle do código-fonte. Sem deixar o ambiente, você pode administrar seus projetos individuais e em equipe facilmente. O provedor de controle do código-fonte não é incluído com o [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)].  
  
#### <a name="to-select-a-source-control-provider"></a>Para selecionar um provedor de controle do código-fonte  
  
1.  Instale a parte cliente de seu provedor de controle do código-fonte.  
  
2.  No [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)], no menu **Ferramentas** , clique em **Opções**.  
  
3.  No **opções** caixa de diálogo caixa, expanda **controle de origem**e, em seguida, clique no **seleção de plug-in** página.  
  
4.  No **atual de controle do código-fonte plug-in** , selecione o plug-in de controle de origem.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Description|  
|-----------|-----------------|  
|[Noções básicas de controle do código-fonte](../../2014/database-engine/source-control-basics.md)|Define a terminologia básica de controle do código-fonte e explica como seu projeto pode se beneficiar do uso de controle do código-fonte.|  
|[Adicionar soluções e projetos ao controle do código-fonte](../../2014/database-engine/add-solutions-and-projects-to-source-control.md)|Explica como usar o ambiente do [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] para adicionar soluções e projetos ao controle do código-fonte.|  
|[Abrir soluções e projetos no controle do código-fonte](../../2014/database-engine/open-solutions-and-projects-from-source-control.md)|Explica como usar o ambiente do [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] para abrir soluções e projetos com controle do código-fonte.|  
|[Gerenciar check-outs](../../2014/database-engine/manage-checkouts.md)|Explica como fazer check-out em soluções e arquivos de controle do código-fonte.|  
|[Gerenciar check-ins](../../2014/database-engine/manage-checkins.md)|Explica como fazer check-in de soluções e arquivos em controle do código-fonte.|  
|[Definir e recuperar informações de versão](../../2014/database-engine/set-and-retrieve-version-information.md)|Explica como recuperar o histórico de um projeto ou item, recuperar uma cópia local de um item ou comparar duas versões de item.|  
|||  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciador de soluções](../ssms/solution/solution-explorer.md)   
 [Soluções &#40;SQL Server Management Studio&#41;](../ssms/sql-server-management-studio-ssms.md)   
 [Projetos &#40;SQL Server Management Studio&#41;](../ssms/solution/projects-sql-server-management-studio.md)   
 [Arquivos que gerenciam soluções e projetos](../ssms/solution/files-that-manage-solutions-and-projects.md)  
  
  