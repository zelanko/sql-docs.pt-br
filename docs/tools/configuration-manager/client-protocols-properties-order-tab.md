---
title: Propriedades de Protocolos de Cliente (guia Ordem)
description: Saiba como habilitar ou desabilitar protocolos de cliente. Confira como reorganizar a ordem na qual os protocolos são usados quando os clientes tentam se conectar ao SQL Server.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- client protocols [SQL Server]
ms.assetid: 64fd7135-1756-4885-bed9-9ab8997ecc6c
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016'
ms.openlocfilehash: 0265cc910186dd17ee1a23419e6843ee293a779d
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97481697"
---
# <a name="client-protocols-properties-order-tab"></a>Propriedades de Protocolos de Cliente (guia Ordem)
[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]
  Use a página **Ordem** na caixa de diálogo **Propriedades de Protocolos de Cliente** para exibir e habilitar os protocolos de cliente.  
  
 Clique em um protocolo e, em seguida, em **Habilitar** ou **Desabilitar** para mover o protocolo selecionado para a lista **Protocolos Desabilitados** ou **Protocolos Habilitados** .  
  
 Os protocolos são testados na ordem listada, tentando conectar usando o primeiro protocolo da lista, depois o segundo protocolo e assim por diante. Mova protocolos para cima ou para baixo na lista **Protocolos Habilitados** , clicando nos botões de seta para cima e para baixo. Na conexão com o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por meio de um cliente nesse computador, o protocolo **Memória Compartilhada** sempre será tentado primeiro, se habilitado.  
  
> [!NOTE]  
>  Essas configurações não são usadas pelo [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET SqlClient. A ordem dos protocolos para o .NET SqlClient é primeiro o TCP, e, em seguida, pipes nomeados que não podem ser alterados.  
  
## <a name="options"></a>Opções  
 **Protocolos Desabilitados**  
 Lista os protocolos que estão instalados, mas não são usados atualmente.  
  
 **Protocolos Habilitados**  
 Lista os protocolos disponíveis para os clientes do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] neste computador.  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Escolhendo um protocolo de rede](/previous-versions/sql/sql-server-2016/ms187892(v=sql.130))  
  
