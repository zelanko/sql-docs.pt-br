---
title: Noções básicas do controle do código-fonte | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- source controls [SQL Server Management Studio], providers
- source controls [SQL Server Management Studio]
- source controls [SQL Server Management Studio], about source controls
- source controls [SQL Server Management Studio], clients
ms.assetid: ca35b67a-104a-41fb-ac58-a61be06fe114
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: bce3bd6862e612a8cefa35d1c981d608bf2c341c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62842939"
---
# <a name="source-control-basics"></a>Noções básicas de controle do código-fonte
  O controle do código-fonte recorre a um sistema em que uma parte central do software de servidor armazena e rastreia versões de arquivos e também controla o acesso a eles. Um sistema de controle do código-fonte típico inclui um provedor de controle do código-fonte, e dois ou mais clientes de controle do código-fonte.  
  
## <a name="source-control-benefits"></a>Vantagens do controle do código-fonte  
 Colocar seus arquivos no controle do código-fonte possibilita  
  
-   O gerenciamento do processo pelo qual o controle de itens passa de uma pessoa para outra. Os provedores de controle do código-fonte dão suporte a acesso a arquivos exclusivos e compartilhados. Se o acesso a arquivos do projeto for exclusivo, o provedor de controle do código-fonte permitirá que apenas um usuário de cada vez faça check-out e modifique os arquivos. Se o acesso for compartilhado, mais de um usuário poderá fazer check-out do arquivo de script e o provedor de controle do código-fonte fornecerá um mecanismo para mesclar as versões conforme seu check-in é feito.  
  
-   Arquivar versões sucessivas de itens com controle do código-fonte. Um provedor de controle do código-fonte armazena os dados que distinguem uma versão de um item com controle do código-fonte de outro. O provedor armazena as diferenças entre versões, além das informações cruciais sobre a versão: quando foi criada, quando foi modificada e por quem. Quando várias pessoas estiverem trabalhando no mesmo arquivo, elas devem usar a mesma página de código, para que as versões possam ser comparadas com precisão. Consequentemente, você pode recuperar qualquer versão de um item com controle do código-fonte. Também é possível designar qualquer versão para ser a mais recente do item.  
  
-   Manter um histórico detalhado e informações de versão sobre itens com controle do código-fonte. O controle do código-fonte armazena a data e hora que o item foi criado, quando foi feito check-out ou check-in e o usuário que executou a ação.  
  
-   Colaborar em diversos projetos. O compartilhamento de arquivos possibilita o compartilhamento de itens com controle do código-fonte entre vários projetos. As alterações feitas em um item compartilhado são refletidas em todos os projetos que compartilham o item.  
  
-   Automatizar operações de controle do código-fonte repetidas com frequência. Um provedor de controle do código-fonte pode definir uma interface no prompt de comando que ofereça suporte aos principais recursos de controle do código-fonte. Você pode usar essa interface em arquivos em lote para automatizar as tarefas de controle do código-fonte executadas regularmente.  
  
-   Recuperar exclusões acidentais. Você pode restaurar a versão mais recente do arquivo em que foi feito check-in no controle do código-fonte.  
  
-   Conservar espaço em disco no cliente e no servidor de controle do código-fonte. Alguns provedores de controle do código-fonte, como o [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual SourceSafe dão suporte à conservação de espaço em disco no servidor, armazenando a última versão de um arquivo e as diferenças entre cada versão e a versão precedente ou seguinte. No cliente, o Visual SourceSafe dá suporte à conservação de espaço em disco. Você pode proteger pastas e arquivos para que eles não sejam baixados para seu disco local.  
  
 Check-in e check-out de arquivos e outras operações de controle do código-fonte são realizadas por um cliente de controle do código-fonte, como o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. O cliente é projetado para interagir com o provedor para tornar os recursos do provedor disponíveis a um grupo distribuído de usuários. Usando um cliente de controle de controle do código-fonte, os usuários podem pesquisar arquivos armazenados pelo provedor, adicionar e excluir arquivos, fazer check-in e check-out e recuperar cópias de arquivos locais.  
  
> [!NOTE]  
>  Esta documentação parte do pressuposto de que você está usando o [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual SourceSafe como seu provedor de controle do código-fonte. Se você estiver usando um provedor de controle do código-fonte diferente, poderá notar diferenças entre esta documentação e a do software que está executando. Caso observe diferenças, consulte a documentação do seu provedor de controle do código-fonte.  
  
## <a name="related-tasks"></a>Related Tasks  
  
|||  
|-|-|  
|**Tarefa**|**Tópico**|  
|Definir opções de controle do código-fonte|[Definir opções de controle do código-fonte](../../2014/database-engine/set-source-control-options.md)|  
|Alterar conexões de controle do código-fonte|[Alterar conexões de controle do código-fonte](../../2014/database-engine/change-source-control-connections.md)|  
|Excluir arquivos do controle do código-fonte|[Excluir arquivos do controle do código-fonte](../../2014/database-engine/exclude-files-from-source-control.md)|  
  
  
