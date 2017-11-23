---
title: "Introdução ao SQL Server 2017 na nuvem | Microsoft Docs"
description: "Este tutorial de início rápido mostra como executar o SQL Server 2017 no Linux na nuvem de sua escolha."
author: annashres
ms.author: annashres
manager: jhubbard
ms.date: 10/25/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 
ms.openlocfilehash: 0bc304b50930f8c8de5d244ea0b606add5f24d2f
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="run-the-sql-server-2017-in-the-cloud"></a>Executar o SQL Server 2017 na nuvem

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

Este tutorial de início rápido, você instalará o SQL Server 2017 no Red Hat Enterprise Linux (RHEL), SUSE Linux Enterprise Server (SLES) ou Ubuntu na nuvem de sua escolha. Vá para [provisionar uma máquina virtual de SQL Server do Linux no portal do Azure](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=%2fsql%2flinux%2ftoc.json) para executar o SQL Server no Linux no Azure.

    > [!NOTE]
    > If you choose to run a paid edition of SQL Server then you need to bring your own license (BYOL)

## <a name="amazon-web-services"></a>Amazon Web Services
1.  Criar um AMI Linux com pelo menos 3,25 GB de memória do marketplace 
    * [RHEL 7.3 +](https://aws.amazon.com/marketplace/pp/B00KWBZVK6)
    * [SLES v12 SP2](https://aws.amazon.com/marketplace/pp/B00PMM99PI)
    * [Ubuntu 16.04](https://aws.amazon.com/marketplace/pp/B01JBL2M0O)
1.  Conecte-se ao AMI com ssh
1.  Siga o guia de início rápido para o distrbution Linux que você escolheu: 
    * [RHEL](quickstart-install-connect-red-hat.md)
    * [SLES](quickstart-install-connect-suse.md)
    * [Ubuntu](quickstart-install-connect-ubuntu.md)
1.  Configure para conexões remotas: 
    * Abra o [Amazon EC2 console]( https://console.aws.amazon.com/ec2/)
    * No painel de navegação, escolha **grupos de segurança**. 
    * Escolha **de entrada, editar, Adicionar regra**
    * Adicionar uma regra de entrada para permitir o tráfego na porta na qual o SQL Server escuta (porta TCP padrão 1433)

    
## <a name="digital-ocean"></a>Azul-marinho digital
1. Logon para o [painel de controle](https://cloud.digitalocean.com/login) e clique em criar um droplet
1. Escolha um droplet Ubuntu 16.04 pelo menos 3,25 GB de memória
1. Conecte-se para o droplet com ssh
1. Siga o [início rápido do Ubuntu](quickstart-install-connect-ubuntu.md)
1. Configure para conexões remotas:
    * Na parte superior do painel de controle, siga o **rede** link e, em seguida, selecione **Firewalls**
    * Adicionar uma regra de entrada para permitir o tráfego na porta na qual o SQL Server escuta (porta TCP padrão 1433)
    
## <a name="google-cloud-platform"></a>Plataforma de nuvem do Google
1.  Criar uma imagem do Linux com pelo menos 3,25 GB de memória do iniciador a nuvem 
    * [RHEL 7.3 +](https://console.cloud.google.com/launcher/details/rhel-cloud/rhel-7)
    * [SLES v12 SP2](https://console.cloud.google.com/launcher/details/suse-cloud/sles-12)
    * [Ubuntu 16.04](https://console.cloud.google.com/launcher/details/ubuntu-os-cloud/ubuntu-xenial)
1.  Conecte-se para a imagem com ssh
1.  Siga o guia de início rápido para o distrbution Linux que você escolheu: 
    * [RHEL](quickstart-install-connect-red-hat.md)
    * [SLES](quickstart-install-connect-suse.md)
    * [Ubuntu](quickstart-install-connect-ubuntu.md)
1.  Configure para conexões remotas: 
    * Vá para o [regras de Firewall](https://console.cloud.google.com/networking/firewalls)
    * Adicionar uma regra de entrada para permitir o tráfego na porta na qual o SQL Server escuta (padrão TCP: 1433)
