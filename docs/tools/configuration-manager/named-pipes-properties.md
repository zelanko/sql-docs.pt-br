---
title: Propriedades de Pipes Nomeados
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- pipes [SQL Server]
- listening [SQL Server], pipes
- pipes [SQL Server], listening on pipes
- Named Pipes [SQL Server], listening on pipes
ms.assetid: a5fd5b8e-f889-485b-89e3-d4010ec4c6ec
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 923f84ccc98837892d144a07ce71238c877ca5b6
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "75306441"
---
# <a name="named-pipes-properties"></a>Propriedades de Pipes Nomeados
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
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
 [Escolhendo um protocolo de rede](https://msdn.microsoft.com/library/6565fb7d-b076-4447-be90-e10d0dec359a)   
 [Criando uma cadeia de conexão válida usando pipes nomeados](https://msdn.microsoft.com/library/90930ff2-143b-4651-8ae3-297103600e4f)  
  
  
