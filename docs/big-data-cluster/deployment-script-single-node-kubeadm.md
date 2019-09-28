---
title: Implantar com um script de Bash em um cluster kubeadm de nó único
titleSuffix: SQL Server big data clusters
description: Use um script de implantação bash para implantar um [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] em um cluster kubeadm de nó único.
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 2379f96e3b5288fc33f5c925613bf9fd5d35612d
ms.sourcegitcommit: c4875c097e3aae1b76233777d15e0a0ec8e0d681
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71341842"
---
# <a name="deploy-with-a-bash-script-to-a-single-node-kubeadm-cluster"></a>Implantar com um script de Bash em um cluster kubeadm de nó único

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Neste tutorial, você usa um script de implantação de Bash de exemplo para implantar um cluster do Kubernetes de nó único usando o kubeadm e um cluster de Big Data do SQL Server nele.  

## <a name="prerequisites"></a>Pré-requisitos

- Uma máquina virtual ou física **do servidor** Ubuntu 18, 4 ou 16, 4. Todas as dependências são configuradas pelo script e você executa o script de dentro da VM.

  > [!NOTE]
  > O uso de VMs Linux do Azure ainda não tem suporte.

- A VM deve ter pelo menos 8 CPUs, 64-GB de RAM e 100 GB de espaço em disco. Depois de extrair todas as imagens do Docker do cluster de Big Data, você terá 50 GB para dados e logs, para usá-los em todos os componentes.

- Atualize os pacotes existentes usando os comandos abaixo para garantir que a imagem do sistema operacional esteja atualizada.

   ``` bash
   sudo apt update && sudo apt upgrade -y
   sudo systemctl reboot
   ```

## <a name="recommended-virtual-machine-settings"></a>Configurações de máquina virtual recomendadas

1. Use a configuração de memória estática para a máquina virtual. Por exemplo, em instalações do Hyper-V, não use alocação de memória dinâmica, mas aloque o 64 GB ou superior recomendado.

1. Use o recurso de ponto de verificação ou instantâneo no seu Hyper-visor para que você possa reverter a máquina virtual para um estado limpo.


## <a name="instructions-to-deploy-sql-server-big-data-cluster"></a>Instruções para implantar SQL Server Cluster de Big Data

1. Baixe o script na VM que você planeja usar para a implantação.

   ```bash
   curl --output setup-bdc.sh https://raw.githubusercontent.com/microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/deployment/kubeadm/ubuntu-single-node-vm/setup-bdc.sh
   ```

2. Torne o script executável com o seguinte comando.

   ```bash
   chmod +x setup-bdc.sh
   ```

3. Execute o script (verifique se você está executando com o *sudo*)

   ```bash
   sudo ./setup-bdc.sh
   ```

   Quando solicitado, forneça sua entrada para a senha a ser usada para os seguintes pontos de extremidade externos: controlador, SQL Server mestre e gateway. A senha deve ser suficientemente complexa com base nas regras existentes para SQL Server senha. O nome de usuário do controlador usa *admin* como padrão.

4. Configure um alias para a ferramenta **azdata**.

   ```bash
   source ~/.bashrc
   ```

5. Atualizar a configuração de alias para azdata.

   ```bash
   azdata --version
   ```

## <a name="cleanup"></a>Limpeza

O script [Cleanup-BDC.sh](https://raw.githubusercontent.com/microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/deployment/kubeadm/ubuntu-single-node-vm/cleanup-bdc.sh) é fornecido como conveniência para redefinir o ambiente, se necessário. No entanto, recomendamos que você use uma máquina virtual para fins de teste e use o recurso de instantâneo em seu hipervisor para reverter a máquina virtual para um estado limpo.

## <a name="next-steps"></a>Próximas etapas

Para começar a usar clusters Big Data, consulte [Tutorial: Carregue dados de exemplo em um cluster SQL Server Big Data @ no__t-0.
