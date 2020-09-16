---
title: Propriedades do NS$&lt;nome do serviço&gt; (guia Logon)
description: Saiba mais sobre a guia Fazer Logon da caixa de diálogo Propriedades do Notification Services no SQL Server. Confira como especificar uma conta e iniciar ou parar o serviço.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: 5e6816ec-d4c5-4429-8033-b97427584890
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: a31f91e4b7387d213f8365f5d10d56251ccd0e87
ms.sourcegitcommit: 6d53ecfdc463914f045c20eda96da39dec22acca
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/26/2020
ms.locfileid: "88900224"
---
# <a name="nsltservice-namegt-properties-log-on-tab"></a>Propriedades do NS$&lt;nome do serviço&gt; (guia Logon)
[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]
  Use a guia **Fazer Logon** da caixa de diálogo **Propriedades de Notification Services** para especificar a conta usada pelo serviço [!INCLUDE[ssNS](../../includes/ssns-md.md)] e para iniciar e parar o serviço.  
  
## <a name="options"></a>Opções  
 **Conta Sistema Local**  
 Especifique uma conta Sistema Local que não requeira uma senha. Porém, essa conta pode restringir a interação do serviço com outros servidores, dependendo dos privilégios concedidos a ela.  
  
 **Esta conta**  
 Especifique uma conta de usuário local ou de domínio que usa a Autenticação do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows. [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomenda usar uma conta de usuário do domínio com direitos mínimos para serviços. Para obter informações sobre como selecionar uma conta, pesquise o tópico "Configurando as contas de serviço do Windows" nos Manuais Online.  
  
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
  
  
