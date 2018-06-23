---
title: Compartilhar arquivos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- sharing files
- file sharing [SQL Server]
- version control services [SQL Server], file sharing
ms.assetid: 645f5c0a-e949-4e87-8988-85e4d6128464
caps.latest.revision: 20
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 528e0ac6eb185089fc7e5e38f654dd1acf2fb64e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36118939"
---
# <a name="share-files"></a>Compartilhar arquivos
  Você pode usar o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] para compartilhar itens em projetos de controle do código-fonte. Quando você compartilha um item, as alterações feitas nele são refletidas em todos os projetos em que ele é compartilhado.  
  
 O compartilhamento de itens oferece as vantagens a seguir para usuários de controle do código-fonte:  
  
-   Torna desnecessário o armazenamento de uma cópia separada do item para cada projeto que usa o item compartilhado, preservando assim espaço em disco no cliente e no servidor de controle do código-fonte. O provedor de controle do código-fonte armazena o item compartilhado em um local central e todos os projetos em que ele é compartilhado armazenam um ponteiro para aquele local.  
  
-   Evita problemas de compatibilidade de versões. Como todos os projetos usam a mesma versão de item compartilhado, você evita conflitos resultantes de alteração de cada cópia de um item independente dentro de vários projetos.  
  
### <a name="to-share-an-item"></a>Para compartilhar um item  
  
1.  No Gerenciador de Soluções, selecione a pasta ou o projeto em que você deseja colocar os arquivos compartilhados.  
  
2.  Sobre o **arquivo** , aponte para **controle de origem**e, em seguida, clique em **compartilhamento**.  
  
3.  No **compartilhar com** caixa de diálogo, navegue pela lista de diretório para o item que você deseja compartilhar e clique nesse item.  
  
4.  Clique em **compartilhamento**.  
  
## <a name="see-also"></a>Consulte também  
 [Noções básicas de controle do código-fonte](../../2014/database-engine/source-control-basics.md)  
  
  