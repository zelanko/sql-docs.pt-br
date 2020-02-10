---
title: Definir e recuperar informações de versão | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- historical information [SQL Server]
- source controls [SQL Server Management Studio], version information
- retrieving version information
- current file version information
- version control services [SQL Server], retrieving version information
- version control services [SQL Server], setting version information
- status information [SQL Server], source control files
- historical information [SQL Server], source control files
ms.assetid: c3f253c4-4e3d-48e8-8d90-bd6ee899faf7
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 68113c6de003aea94924f6e220373664212becf1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62843477"
---
# <a name="set-and-retrieve-version-information"></a>Definir e recuperar informações de versão
  As informações de versão incluem o histórico e o status atual de um arquivo com controle do código-fonte. Para todo arquivo com controle do código-fonte, o [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual SourceSafe mantém um histórico abrangente, de forma que você pode localizar a evolução de um ou mais arquivos com o passar do tempo. Você também pode usar essas informações para recuperar uma cópia local de qualquer versão do arquivo ou comparar duas versões de arquivos.  
  
 O histórico de um arquivo inclui:  
  
-   O número de versão que identifica sua sequência entre outras versões do mesmo arquivo.  
  
-   A ação executada. Operações rastreadas incluem criação de arquivo, check-in e exclusão.  
  
-   O nome do usuário que executou uma ação envolvendo o arquivo.  
  
-   A data e hora em que a operação foi executada.  
  
 O Visual SourceSafe também mantém informações sobre o status atual da solução carregada. Essas informações fornecem um instantâneo do status atual do arquivo, incluindo:  
  
-   A identidade do usuário que fez o check-out do arquivo.  
  
-   A versão mais recente do arquivo selecionado.  
  
-   A data em que a versão foi criada.  
  
-   O comentário do usuário associado com a versão.  
  
-   Os caminhos dos projetos com os quais o arquivo é compartilhado.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Exibir o histórico de arquivos](../../2014/database-engine/view-file-history.md)  
  
-   [Exibir histórico de projetos](../../2014/database-engine/view-project-history.md)  
  
-   [Exibir status de arquivos](../../2014/database-engine/view-file-status.md)  
  
-   [Recuperar arquivos](../../2014/database-engine/retrieve-files.md)  
  
-   [Especificar uma versão como a versão mais recente](../../2014/database-engine/specify-a-version-as-the-latest-version.md)  
  
-   [Comparar arquivos](../../2014/database-engine/compare-files.md)  
  
-   [Compartilhar arquivos](../../2014/database-engine/share-files.md)  
  
-   [Criar histórico e relatórios de status](../../2014/database-engine/create-history-and-status-reports.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Noções básicas de controle do código-fonte](../../2014/database-engine/source-control-basics.md)  
  
  
