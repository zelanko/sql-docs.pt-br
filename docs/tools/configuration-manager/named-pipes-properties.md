---
title: Propriedades de Pipes Nomeados
description: Use a página Protocolo na caixa de diálogo Propriedades de Pipes Nomeados para, quando usar o protocolo Pipes Nomeados, exibir ou alterar o pipe nomeado escutado pelo SQL Server.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- pipes [SQL Server]
- listening [SQL Server], pipes
- pipes [SQL Server], listening on pipes
- Named Pipes [SQL Server], listening on pipes
ms.assetid: a5fd5b8e-f889-485b-89e3-d4010ec4c6ec
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016'
ms.openlocfilehash: c4929816503430c151c80735078d6a71b0221e71
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97463855"
---
# <a name="named-pipes-properties"></a>Propriedades de Pipes Nomeados
[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]
  Use a página **Protocolo** na caixa de diálogo **Propriedades de Pipes Nomeados** para exibir ou alterar o pipe nomeado que o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] escuta ao usar o protocolo Pipes Nomeados.  
  
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
 [Escolhendo um protocolo de rede](/previous-versions/sql/sql-server-2016/ms187892(v=sql.130))   
 [Criando uma cadeia de conexão válida usando pipes nomeados](/previous-versions/sql/sql-server-2016/ms189307(v=sql.130))  
  
