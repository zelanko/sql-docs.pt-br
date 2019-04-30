---
title: Serviço desconhecido (guia fazer logon) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: e9b35cb5-d8ae-42ea-b59e-deedc99c4823
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 686eb039660efb6e3596b9dac88fc0d24deacaee
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63150525"
---
# <a name="unknown-service-log-on-tab"></a>Serviço desconhecido (guia Fazer Logon)
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager não pode identificar este serviço.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager recebe informações de serviço do provedor WMI no computador que está executando o serviço. Ocorreu um erro ao ler as propriedades do serviço ou essas propriedades não estão completas. Para resolver o problema, tente fechar e reabrir o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager ou verifique o provedor WMI no computador que está executando o serviço.  
  
 O provedor WMI é um componente do Windows. Para obter informações sobre como verificar permissões no provedor WMI, consulte "como: Configure o WMI para mostrar o Status do servidor nas ferramentas do SQL Server "nos Manuais Online do SQL Server.  
  
 Se você achar que está exibindo o serviço correto, use a guia **Fazer Logon** da caixa de diálogo **Propriedades de Serviço Desconhecido** para especificar a conta usada por esse serviço e para iniciar e parar o serviço.  
  
## <a name="options"></a>Opções  
 **Conta Sistema Local**  
 Especifique uma conta Sistema Local que não requeira uma senha. No entanto, ela pode impedir a interação do serviço com outros servidores, dependendo dos privilégios concedidos a ela.  
  
 **Esta conta**  
 Especifique um local ou conta de usuário do domínio que utilize Autenticação do Windows. É recomendável usar uma conta de usuário do domínio com direitos mínimos para serviços. Para obter informações sobre como selecionar uma conta, consulte "Configurando as contas de serviço do Windows" nos Manuais Online do SQL Server.  
  
 **Nome da Conta**  
 Especifique o nome da conta local ou de usuário de domínio.  
  
 **Senha**  
 Digite a senha da conta.  
  
 **Confirmar senha**  
 Digite a senha da conta novamente.  
  
 **Iniciar**  
 Inicie o serviço.  
  
 **Parar**  
 Parar o serviço.  
  
 **Pausar**  
 Pausar o serviço.  
  
 **Retomar**  
 Retomar um serviço pausado.  
  
  
