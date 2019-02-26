---
title: Introdução ao SQL Server (no Linux) na nuvem
titleSuffix: SQL Server
description: Neste início rápido mostra como executar o SQL Server no Linux na nuvem de sua escolha.
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 10/25/2017
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux, seodec18
ms.technology: linux
ms.assetid: ''
ms.openlocfilehash: 54373ea101820a29e04501ea6848a4a85a2c893a
ms.sourcegitcommit: a13256f484eee2f52c812646cc989eb0ce6cf6aa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/25/2019
ms.locfileid: "56801150"
---
# <a name="quickstart-run-sql-server-in-the-cloud"></a>Início Rápido: Executar o SQL Server na nuvem
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Neste início rápido, você instalará o SQL Server no Red Hat Enterprise Linux (RHEL), SUSE Linux Enterprise Server (SLES) ou Ubuntu na nuvem de sua escolha. Vá para [provisionar uma máquina virtual do Linux do SQL Server no portal do Azure](https://docs.microsoft.com/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=%2fsql%2flinux%2ftoc.json) para executar o SQL Server no Linux no Azure.

> [!NOTE]
> Se você optar por executar uma edição paga do SQL Server, você precisará usar sua própria licença (BYOL).

## <a name="amazon-web-services"></a>Amazon Web Services
1.  Criar um AMI Linux com pelo menos 2 GB de memória do marketplace 
    * [RHEL 7.3+](https://aws.amazon.com/marketplace/pp/B00KWBZVK6)
    * [SLES v12 SP2](https://aws.amazon.com/marketplace/pp/B00PMM99PI)
    * [Ubuntu 16.04](https://aws.amazon.com/marketplace/pp/B01JBL2M0O)
1.  Conectar-se para o AMI com ssh
1.  Siga o guia de início rápido para a distribuição de Linux que você escolheu: 
    * [RHEL](quickstart-install-connect-red-hat.md)
    * [SLES](quickstart-install-connect-suse.md)
    * [Ubuntu](quickstart-install-connect-ubuntu.md)
1.  Configure para conexões remotas: 
    * Abra o [console Amazon EC2]( https://console.aws.amazon.com/ec2/)
    * No painel de navegação, escolha **grupos de segurança**. 
    * Escolha **de entrada, editar, Adicionar regra**
    * Adicionar uma regra de entrada para permitir o tráfego na porta na qual o SQL Server escuta (porta TCP do padrão 1433)

    
## <a name="digital-ocean"></a>Oceano digital
1. Faça logon na [painel de controle](https://cloud.digitalocean.com/login) e clique em criar um droplet
1. Escolha um droplet Ubuntu 16.04 pelo menos 2 GB de memória
1. Conectar-se para o droplet com ssh
1. Siga o [início rápido do Ubuntu](quickstart-install-connect-ubuntu.md)
1. Configure para conexões remotas:
    * Na parte superior do painel de controle, execute as **Networking** vincular e, em seguida, selecione **Firewalls**
    * Adicionar uma regra de entrada para permitir o tráfego na porta na qual o SQL Server escuta (porta TCP do padrão 1433)
    
## <a name="google-cloud-platform"></a>Plataforma de nuvem do Google
1.  Criar uma imagem do Linux com pelo menos 2 GB de memória do que o iniciador de nuvem 
    * [RHEL 7.3+](https://console.cloud.google.com/launcher/details/rhel-cloud/rhel-7)
    * [SLES v12 SP2](https://console.cloud.google.com/launcher/details/suse-cloud/sles-12)
    * [Ubuntu 16.04](https://console.cloud.google.com/launcher/details/ubuntu-os-cloud/ubuntu-xenial)
1.  Conectar-se para a imagem com ssh
1.  Siga o guia de início rápido para a distribuição de Linux que você escolheu: 
    * [RHEL](quickstart-install-connect-red-hat.md)
    * [SLES](quickstart-install-connect-suse.md)
    * [Ubuntu](quickstart-install-connect-ubuntu.md)
1.  Configure para conexões remotas: 
    * Vá para o [regras de Firewall](https://console.cloud.google.com/networking/firewalls)
    * Adicionar uma regra de entrada para permitir o tráfego na porta de escuta do SQL Server (padrão tcp: 1433)
