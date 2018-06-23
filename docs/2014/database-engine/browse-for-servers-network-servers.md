---
title: Procurar servidores (servidores de rede) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.swb.browseservers.network.f1
ms.assetid: a59ffcd6-4b69-4c5c-9740-699ccb2183fb
caps.latest.revision: 27
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: db0e235abb91181ac2090000b9d307181f720768
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36115280"
---
# <a name="browse-for-servers-network-servers"></a>Procurar servidores (Servidores de Rede)
  Se você está se conectando a um componente do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e não sabe o nome exato da instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], clique em **Procurar mais** na caixa **Nome do servidor** para abrir a caixa de diálogo **Procurar Servidores**.  
  
 Esta caixa de diálogo é populada pelo serviço [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Browser nos computadores de servidor. Há várias razões pelas quais o nome de uma instância pode não aparecer na lista:  
  
-   O serviço [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Browser pode não estar executando no computador que executa o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
-   A porta 1434 UDP pode estar bloqueada por um firewall.  
  
-   O sinalizador **HideInstance** pode estar configurado.  
  
 Para se conectar a uma instância que não apareça na lista, digite uma cadeia de caracteres de conexão completa para a instância, incluindo o número da porta TCP/IP ou o nome pipe dos pipes nomeados.  
  
## <a name="options"></a>Opções  
 **Selecione uma instância do SQL Server na rede para sua conexão**  
 Designe o servidor ao qual você deseja se conectar clicando na instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] exibida na árvore. Você pode mostrar ou ocultar partes do modo de exibição de árvore clicando nos nós marcados com um sinal de mais **+** ou de menos **–** .  
  
  