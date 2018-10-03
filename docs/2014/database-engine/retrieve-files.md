---
title: Recuperar arquivos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- version control services [SQL Server], file retrieval
- file retrieval [SQL Server]
- retrieving files
ms.assetid: 37b74426-e262-43b2-a81f-79b1fd1a36ec
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 548fac7dbc7d1f2750a130da9847be406361d8bf
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48149536"
---
# <a name="retrieve-files"></a>Recuperar arquivos
  Após abrir um projeto com controle do código-fonte, você pode usar o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] para recuperar cópias locais de arquivos do projeto da armazenagem do controle do código-fonte para o diretório local em que o projeto fica armazenado.  
  
 Você pode usar o controle do código-fonte integrado para recuperar arquivos de acordo com um dos modos a seguir:  
  
-   **Obter a versão mais recente (recursivo)** comando  
  
     Recupera a última versão registrada dos arquivos selecionados. Se uma solução ou um projeto for selecionado, esse comando recuperará a versão mais recente de todos os arquivos da solução e do projeto.  
  
-   **Obter** comando  
  
     Exibe a **obter** caixa de diálogo que você pode usar para recuperar a versão mais recente de um arquivo selecionado, ou para recuperar um subconjunto dos arquivos no projeto ou solução selecionada.  
  
### <a name="to-retrieve-the-latest-version-of-all-the-files-in-a-project"></a>Para recuperar a versão mais recente registrada de todos os arquivos em um projeto  
  
1.  No Gerenciador de Soluções, selecione o projeto.  
  
2.  Sobre o **arquivo** , aponte para **controle do código-fonte**e, em seguida, clique em **obter versão mais recente (recursivo)**.  
  
 As versões mais recentes dos arquivos do projeto são recuperadas no local do projeto no disco local.  
  
#### <a name="to-retrieve-only-certain-files-in-a-project"></a>Para recuperar somente determinados arquivos em um projeto  
  
1.  No Gerenciador de Soluções, selecione o item que você deseja recuperar.  
  
2.  Sobre o **arquivo** , aponte para **controle do código-fonte**e, em seguida, clique em **obter**.  
  
3.  No **Obtenha** caixa de diálogo, clique em **Okey**. Como alternativa, se você tiver selecionado uma solução ou um projeto no Gerenciador de Soluções, desmarque as caixas de seleção que aparecem próximas aos itens que não deseja recuperar.  
  
## <a name="see-also"></a>Consulte também  
 [Obtém uma caixa de diálogo &#40;controle de origem&#41;](../../2014/database-engine/get-dialog-box-source-control.md)   
 [Definir e recuperar informações de versão](../../2014/database-engine/set-and-retrieve-version-information.md)   
 [Exibir histórico de projetos](../../2014/database-engine/view-project-history.md)   
 [Exibir status de arquivos](../../2014/database-engine/view-file-status.md)  
  
  
