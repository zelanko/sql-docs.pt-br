---
title: Propriedades de Pipes nomeados | Microsoft Docs
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
- pipes [SQL Server]
- listening [SQL Server], pipes
- pipes [SQL Server], listening on pipes
- Named Pipes [SQL Server], listening on pipes
ms.assetid: a5fd5b8e-f889-485b-89e3-d4010ec4c6ec
caps.latest.revision: 31
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 2eb32e8d751a152fed9eebd8b9994005d597dd42
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36130682"
---
# <a name="named-pipes-properties"></a>Propriedades de Pipes Nomeados
  Use a página **Protocolo**na caixa de diálogo **Propriedades de Pipes Nomeados** para exibir ou alterar o pipe nomeado escutado pelo [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , quando usar o protocolo Pipes Nomeados.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve ser reiniciado para habilitar ou desabilitar o protocolo, ou para alterar o pipe nomeado.  
  
## <a name="options"></a>Opções  
 **Enabled**  
 Os valores possíveis são **Sim** e **Não**.  
  
 **Nome do Pipe**  
 Especifica o pipe nomeado no qual o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] escuta. Por padrão, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] escuta em: `\\.\pipe\sql\query` para a instância padrão e `\\.\pipe\MSSQL$<instancename>\sql\query` para uma instância nomeada. Este campo é limitado a 2.047 caracteres.  
  
## <a name="creating-an-alternate-named-pipe"></a>Criando um pipe nomeado alternativo  
 Para alterar o pipe nomeado, digite o nome do novo pipe na caixa **Nome do Pipe** e, em seguida, pare e reinicie o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Como **sql\query** é bem conhecido como o pipe nomeado usado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a alteração do pipe pode ajudar a reduzir o risco de ataque de programas mal-intencionados.  
  
### <a name="example"></a>Exemplo  
 Digite **\\\\.\pipe\unit\app** para escutar no pipe **unit\app** .  
  
 Digite **\\\\.\pipe\acct** para escutar no pipe **acct** .  
  
## <a name="see-also"></a>Consulte também  
 [Habilitar ou desabilitar um protocolo de rede de servidor](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)   
 [Escolhendo um protocolo de rede](../../../2014/tools/configuration-manager/choosing-a-network-protocol.md)   
 [Criando uma cadeia de conexão válida usando pipes nomeados](../../../2014/tools/configuration-manager/creating-a-valid-connection-string-using-named-pipes.md)  
  
  