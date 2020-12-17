---
title: Propriedades do SQL Server (guia Fazer Logon)
description: Saiba mais sobre a guia Fazer Logon da caixa de diálogo Propriedades do SQL Server. Use essa guia para especificar a conta que o SQL Server usa e iniciar ou parar o serviço.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: 405073fc-eaa3-43c6-bf82-2cd58cacc1c3
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016'
ms.openlocfilehash: 79f44e0dc2cd86fa4d2d839ed0542e8db697ee26
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97478387"
---
# <a name="sql-server-properties-log-on-tab"></a>Propriedades do SQL Server (guia Fazer Logon)
[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]
  Use a guia **Fazer Logon** da caixa de diálogo **Propriedades do SQL Server** para especificar a conta usada pelo serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , para alterar a senha de uma conta e para iniciar e parar o serviço. A alteração da senha de uma conta entra em vigor imediatamente.  
  
> [!NOTE]  
>  Quando ocorrer alteração no nome de conta usado por um serviço em uma instância clusterizada, a nova conta deverá ser membro do grupo de domínio especificado, durante a instalação, para o serviço que está sendo alterado, ou você deverá ter permissão para adicionar membros a esse grupo. Se você não tiver permissão para modificar a associação de grupo, contate o administrador de domínio.  
>   
>  Para obter mais informações sobre como selecionar uma conta para executar o serviço, consulte "Configurando as contas de serviço do Windows" nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="options"></a>Opções  
 **Conta interna**  
 **Sistema Local**  
 -   Especifique a conta Sistema Local. Essa conta não requer uma senha. No entanto, ela pode impedir a interação do serviço com outros servidores, dependendo dos privilégios concedidos a ela.  
  
 **Serviço Local**  
 -   Especifique a conta de serviço local. Essa conta não requer uma senha. No entanto, ela pode impedir a interação do serviço com outros servidores, dependendo dos privilégios concedidos a ela.  
  
 **Serviço de Rede**  
 -   É recomendável não usar a conta do Serviço de Rede para os serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. As contas de Usuário Local ou Usuário de Domínio são mais apropriadas para esses serviços.  
  
 **Esta conta**  
 Especifique um local ou conta de usuário do domínio que utilize Autenticação do Windows. É recomendável usar uma conta de usuário de domínio com direitos mínimos para serviços.  
  
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
  
> [!IMPORTANT]  
>  Por padrão, apenas membros do grupo de administradores local podem iniciar, interromper, pausar, retomar ou reiniciar um serviço. Para conceder a capacidade de gerenciar serviços a não administradores, consulte [Como conceder aos usuários direitos para gerenciar serviços no Windows Server 2003](https://support.microsoft.com/kb/325349). (O processo é semelhante em outras versões do Windows.)  
  
> [!NOTE]  
>  Ao iniciar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], um erro do WMI com a frase "not implemented [0x80004001]" pode indicar que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não está instalado no computador de destino.  
  
  
