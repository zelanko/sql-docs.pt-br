---
title: Propriedades de pipes nomeados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- pipes [SQL Server]
- listening [SQL Server], pipes
- pipes [SQL Server], listening on pipes
- Named Pipes [SQL Server], listening on pipes
ms.assetid: a5fd5b8e-f889-485b-89e3-d4010ec4c6ec
author: stevestein
ms.author: sstein
ms.openlocfilehash: 1177449ee7828c86c6d7803d5052b9d6e95c24ea
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85064267"
---
# <a name="named-pipes-properties"></a>Propriedades de Pipes Nomeados
  Use a página **Protocolo**na caixa de diálogo **Propriedades de Pipes Nomeados** para exibir ou alterar o pipe nomeado que o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] escuta ao usar o protocolo Pipes Nomeados.  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Habilitar ou desabilitar um protocolo de rede de servidor](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)   
 [Escolhendo um protocolo de rede](../../../2014/tools/configuration-manager/choosing-a-network-protocol.md)   
 [Criando uma cadeia de conexão válida usando pipes nomeados](../../../2014/tools/configuration-manager/creating-a-valid-connection-string-using-named-pipes.md)  
  
  
