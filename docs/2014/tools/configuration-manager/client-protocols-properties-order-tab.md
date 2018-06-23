---
title: Propriedades (guia ordem) de protocolos de cliente | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- configmgr-client
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- client protocols [SQL Server]
ms.assetid: 64fd7135-1756-4885-bed9-9ab8997ecc6c
caps.latest.revision: 17
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 8b77c6812f01400a809c56be19886294285c628c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36117774"
---
# <a name="client-protocols-properties-order-tab"></a>Propriedades de Protocolos de Cliente (guia Ordem)
  Use a página **Ordem** na caixa de diálogo **Propriedades de Protocolos de Cliente** para exibir e habilitar os protocolos de cliente.  
  
 Clique em um protocolo e, em seguida, em **Habilitar** ou **Desabilitar** para mover o protocolo selecionado para a lista **Protocolos Desabilitados** ou **Protocolos Habilitados**.  
  
 Os protocolos são testados na ordem listada, tentando conectar usando o primeiro protocolo da lista, depois o segundo protocolo e assim por diante. Mova protocolos para cima ou para baixo na lista **Protocolos Habilitados**, clicando nos botões de seta para cima e para baixo. Na conexão com o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por meio de um cliente nesse computador, o protocolo **Memória Compartilhada** sempre será tentado primeiro, se habilitado.  
  
> [!NOTE]  
>  Essas configurações não são usadas pelo [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET SqlClient. A ordem dos protocolos para o .NET SqlClient é primeiro o TCP, e, em seguida, pipes nomeados que não podem ser alterados.  
  
## <a name="options"></a>Opções  
 **Protocolos Desabilitados**  
 Lista os protocolos que estão instalados, mas não são usados atualmente.  
  
 **Protocolos Habilitados**  
 Lista os protocolos que estão disponíveis para os clientes do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] neste computador.  
  
 **>**  
 Habilita o protocolo realçado na caixa **Protocolos Desabilitados** , movendo-o para a caixa **Protocolos Habilitados** .  
  
 **\<**  
 Desabilita o protocolo realçado na caixa **Protocolos Habilitados** , movendo-o para a caixa **Protocolos Desabilitados** .  
  
 Seta para cima  
 Move o protocolo realçado para cima na lista. Isso permite aumentar a prioridade com que a Biblioteca de Rede tentará usar o protocolo selecionado para conexões.  
  
 Seta para baixo  
 Move o protocolo realçado para baixo na lista. Isso permite diminuir a prioridade com que a Biblioteca de Rede tentará usar o protocolo selecionado para conexões.  
  
 **Habilitar Protocolo de Memória Compartilhada**  
 Habilita o protocolo de memória compartilhada que sempre é tentado primeiro (se habilitado), ao conectar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por meio de um cliente nesse computador.  
  
> [!NOTE]  
>  Se o protocolo for especificado por meio de um prefixo ou como parte da cadeia de conexão, somente o protocolo especificado será tentado.  
  
## <a name="see-also"></a>Consulte também  
 [Escolhendo um protocolo de rede](../../../2014/tools/configuration-manager/choosing-a-network-protocol.md)  
  
  