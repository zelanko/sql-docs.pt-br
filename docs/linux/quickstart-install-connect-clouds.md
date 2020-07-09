---
title: Introdução ao SQL Server (em Linux) na Nuvem
titleSuffix: SQL Server
description: Este início rápido mostra como executar o SQL Server em Linux na sua nuvem preferida.
author: VanMSFT
ms.author: vanto
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: ''
ms.openlocfilehash: cb24499b411d288e1e79b49d202fba63b251a805
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85897543"
---
# <a name="quickstart-run-sql-server-in-the-cloud"></a>Início Rápido: Executar SQL Server na nuvem
[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

Neste início rápido, você instalará o SQL Server no RHEL (Red Hat Enterprise Linux), no SLES (SUSE Linux Enterprise Server) ou no Ubuntu na nuvem de sua escolha. Acesse [Provisionar uma máquina virtual do SQL Server do Linux no portal do Azure](https://docs.microsoft.com/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=/sql/toc/toc.json) para executar o SQL Server em Linux no Azure.

> [!NOTE]
> Se você optar por executar uma edição paga do SQL Server, precisará usar BYOL (traga sua própria licença).

## <a name="amazon-web-services"></a>Amazon Web Services
1.  Criar um AMI Linux com pelo menos 2 GB de memória com base no marketplace 
    * [RHEL 7.3+](https://aws.amazon.com/marketplace/pp/B00KWBZVK6)
    * [SLES v12 SP2+](https://aws.amazon.com/marketplace/pp/B00PMM99PI)
    * [Ubuntu 16.04](https://aws.amazon.com/marketplace/pp/B01JBL2M0O)
1.  Conectar-se ao AMI com ssh
1.  Siga o início rápido para ver a distribuição do Linux que você escolheu: 
    * [RHEL](quickstart-install-connect-red-hat.md)
    * [SLES](quickstart-install-connect-suse.md)
    * [Ubuntu](quickstart-install-connect-ubuntu.md)
1.  Configure conexões remotas: 
    * Abra o [console do Amazon EC2]( https://console.aws.amazon.com/ec2/)
    * No painel de navegação, escolha **Grupos de Segurança**. 
    * Escolha **Entrada, Editar, Adicionar Regra**
    * Adicione uma regra de entrada para permitir o tráfego na porta na qual o SQL Server escuta (porta TCP 1433 padrão)

    
## <a name="digital-ocean"></a>Oceano digital
1. Faça logon no [painel de controle](https://cloud.digitalocean.com/login) e clique em criar um droplet
1. Escolha um droplet Ubuntu 16.04 com pelo menos 2 GB de memória
1. Conectar-se ao droplet com ssh
1. Siga o [início rápido do Ubuntu](quickstart-install-connect-ubuntu.md)
1. Configure conexões remotas:
    * Na parte superior do Painel deCcontrole, siga o link **Rede** e selecione **Firewalls**
    * Adicione uma regra de entrada para permitir o tráfego na porta na qual o SQL Server escuta (porta TCP 1433 padrão)
    
## <a name="google-cloud-platform"></a>Google Cloud Platform
1.  Criar uma imagem Linux com pelo menos 2 GB de memória com base no Cloud Launcher 
    * [RHEL 7.3+](https://console.cloud.google.com/launcher/details/rhel-cloud/rhel-7)
    * [SLES v12 SP4](https://console.cloud.google.com/launcher/details/suse-cloud/sles-12)
    * [Ubuntu 16.04](https://console.cloud.google.com/launcher/details/ubuntu-os-cloud/ubuntu-xenial)
1.  Conectar-se à imagem com ssh
1.  Siga o início rápido para ver a distribuição do Linux que você escolheu: 
    * [RHEL](quickstart-install-connect-red-hat.md)
    * [SLES](quickstart-install-connect-suse.md)
    * [Ubuntu](quickstart-install-connect-ubuntu.md)
1.  Configure conexões remotas: 
    * Acesse as [Regras de Firewall](https://console.cloud.google.com/networking/firewalls)
    * Adicione uma regra de entrada para permitir o tráfego na porta na qual o SQL Server escuta (tcp padrão: 1433)
