---
title: Implantar um cluster kubeadm de nó único
titleSuffix: SQL Server Big Data Clusters
description: Use um script de implantação de Bash para implantar um [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] em um cluster kubeadm de nó único.
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.metadata: seo-lt-2019
ms.date: 12/13/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: f60256e58339387323f923c85d2b880459455663
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "75252098"
---
# <a name="deploy-with-a-bash-script-to-a-single-node-kubeadm-cluster"></a>Implantar com um script de Bash em um cluster kubeadm de nó único

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Neste tutorial, você usa um script de implantação de Bash de exemplo para implantar um cluster do Kubernetes de nó único usando o kubeadm e um cluster de Big Data do SQL Server nele.

## <a name="prerequisites"></a>Prerequisites

- Um computador físico ou uma máquina virtual com **servidor** vanilla Ubuntu 18.04 ou 16.04. Todas as dependências são configuradas pelo script e você executa o script de dentro da VM.

  > [!NOTE]
  > O uso de VMs Linux do Azure ainda não tem suporte.

- A VM deve ter pelo menos 8 CPUs, 64 GB de RAM e 100 GB de espaço em disco. Depois de extrair todas as imagens do Docker do cluster de Big Data, você terá 50 GB para dados e logs, para usá-los em todos os componentes.

- Atualize os pacotes existentes usando os comandos abaixo para garantir que a imagem do sistema operacional esteja atualizada.

   ``` bash
   sudo apt update && sudo apt upgrade -y
   sudo systemctl reboot
   ```

## <a name="recommended-virtual-machine-settings"></a>Configurações de máquina virtual recomendadas

1. Use a configuração de memória estática para a máquina virtual. Por exemplo, em instalações do Hyper-V, não use alocação de memória dinâmica, mas aloque os 64 GB ou mais recomendados.

1. Use a funcionalidade de ponto de verificação ou de instantâneo em seu hipervisor para que você possa reverter a máquina virtual para um estado limpo.


## <a name="instructions-to-deploy-sql-server-big-data-cluster"></a>Instruções para implantar o Cluster de Big Data do SQL Server

1. Baixe o script na VM que você planeja usar para a implantação.

   ```bash
   curl --output setup-bdc.sh https://raw.githubusercontent.com/microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/deployment/kubeadm/ubuntu-single-node-vm/setup-bdc.sh
   ```

2. Torne o script executável com o seguinte comando.

   ```bash
   chmod +x setup-bdc.sh
   ```

3. Execute o script (verifique se você está executando com *sudo*)

   ```bash
   sudo ./setup-bdc.sh
   ```

   Quando solicitado, forneça sua entrada para a senha a ser usada para os seguintes pontos de extremidade externos: controlador, SQL Server mestre e gateway. A senha deve ser suficientemente complexa com base nas regras existentes para senhas do SQL Server. O nome de usuário do controlador usa *admin* como padrão.

4. Configure um alias para a ferramenta **azdata**.

   ```bash
   source ~/.bashrc
   ```

5. Atualizar a configuração de alias para azdata.

   ```bash
   azdata --version
   ```

## <a name="cleanup"></a>Limpeza

O script [cleanup-bdc.sh](https://raw.githubusercontent.com/microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/deployment/kubeadm/ubuntu-single-node-vm/cleanup-bdc.sh) é fornecido para fins de conveniência, para redefinir o ambiente se necessário. No entanto, recomendamos que você use uma máquina virtual para fins de teste e use a funcionalidade de instantâneo em seu hipervisor para reverter a máquina virtual para um estado limpo.

## <a name="next-steps"></a>Próximas etapas

Para começar a usar Clusters de Big Data, confira [Tutorial: Carregar dados de exemplo em um Cluster de Big Data do SQL Server](tutorial-load-sample-data.md).
