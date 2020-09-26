---
title: Implantar o SQL do Azure no Edge com o Azure Data Studio
description: Como implantar instâncias do SQL do Azure no Edge no Azure Data Studio
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: how-to
author: dzsquared
ms.author: drskwier
ms.reviewer: maghan
ms.custom: ''
ms.date: 09/22/2020
ms.openlocfilehash: 89732af2b2fc5926193519b4a6508b97ac998c88
ms.sourcegitcommit: 63aef5a96905f0b026322abc9ccb862ee497eebe
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/25/2020
ms.locfileid: "91364113"
---
# <a name="deploy-azure-sql-edge-with-azure-data-studio-preview"></a>Implantar o SQL do Azure no Edge com o Azure Data Studio (Versão Prévia)

O [SQL do Azure no Edge](https://docs.microsoft.com/azure/azure-sql-edge/overview) é um mecanismo de banco de dados relacional otimizado para implantações de IoT e do Azure IoT Edge. Ele oferece funcionalidades para a criação de uma camada de processamento e armazenamento de dados de alto desempenho para aplicativos e soluções de IoT. Este artigo mostrará como implantar uma instância do SQL do Azure no Edge com o Azure Data Studio e os cenários de implantação compatíveis com o assistente de implantação.  

Os seguintes cenários são compatíveis com o assistente de implantação no Azure Data Studio:

- Instância de contêiner local
- Instância de contêiner remoto
- Hub IoT do Azure e VM novos
- Dispositivo existente de um Hub IoT do Azure
- Vários dispositivos de um Hub IoT do Azure

| Ferramentas necessárias | `Docker` | `Azure CLI` |
| ------------- | :---: | :---: |
| Instância de contêiner local | x | |
| Instância de contêiner remoto | | |
| Hub IoT do Azure e VM novos | | x |
| Dispositivo existente de um Hub IoT do Azure |  | x |
| Vários dispositivos de um Hub IoT do Azure |   |  x |

> [!NOTE]
> A implantação do SQL do Azure no Edge (versão prévia) está disponível por meio de uma extensão chamada "Extensão de Implantação do SQL do Azure no Edge", já esses recursos estão na versão prévia. Para disponibilizar os recursos, instale a extensão no Azure Data Studio.

Para iniciar uma implantação no Azure Data Studio, abra o menu na exibição **Conexões** e selecione a opção **Nova Implantação...** .  Para obter todos os cenários do SQL do Azure no Edge, selecione **SQL do Azure no Edge** na tela a seguir e o cenário desejado na lista suspensa **Destino de implantação**. O assistente de implantação gera um notebook TSQL que pode ser executado para concluir a implantação. É importante observar que as informações de conexão, incluindo a senha de administrador do SQL, estão contidas no notebook por padrão.

![visão geral da implantação](media/deploy-azure-sql-edge/deploy-overview.png)

## <a name="local-container-instance"></a>Instância de contêiner local

O SQL do Azure no Edge poderá ser implantado em um contêiner do Docker no localhost especificando o nome do contêiner, a senha de usuário `sa` e a porta do host para obter uma conectividade do SQL do Azure no Edge.  Depois de concluir a implantação, vários links estarão disponíveis na parte inferior do notebook para executar ações adicionais:

- **Clicar aqui para se conectar à instância do SQL do Azure no Edge**: cria uma conexão no Azure Data Studio para a nova instância do SQL do Azure no Edge
- **Abrir a janela do terminal**: abre um terminal (existente ou novo) no Azure Data Studio
- **Interromper o contêiner**: copia um comando no terminal que interromperá o contêiner quando for executado pelo usuário
- **Remover o contêiner**: copia um comando no terminal que removerá o contêiner quando for executado pelo usuário

## <a name="remote-container-instance"></a>Instância de contêiner remoto

O SQL do Azure no Edge poderá ser implantado no contêiner do Docker em um host remoto usando o Docker instalado e especificando as informações do contêiner e do computador host/de destino.  Depois de concluir a implantação, um link de conexão estará disponível na parte inferior do notebook.  Para interromper ou remover o contêiner, devido a um ambiente de host de contêiner remoto, os comandos deverão ser copiados para serem executados em um shell remoto.

## <a name="new-azure-iot-hub-and-vm"></a>Hub IoT do Azure e VM novos

O assistente de implantação do SQL do Azure no Edge poderá criar vários recursos do Azure necessários para implantar uma VM (máquina virtual) habilitada para borda e conectada a um hub IoT do Azure. Será necessário obter uma assinatura ativa do Azure. Essa implantação criará:

- Grupo de recursos (caso o grupo de recursos atual não esteja selecionado)
- Grupo de segurança de rede
- Máquina virtual
- Endereço IP público estático

Também será possível compactar um arquivo dacpac em uma pasta e implantá-lo na nova instância do SQL do Azure no Edge como parte do processo.  Caso um arquivo dacpac seja fornecido, uma conta de Armazenamento de Blobs do Azure será criada no mesmo grupo de recursos.

## <a name="existing-device-of-an-azure-iot-hub"></a>Dispositivo existente de um Hub IoT do Azure

Caso tenha um hub IoT existente e um dispositivo conectado, o SQL do Azure no Edge poderá ser implantado no dispositivo com base no grupo de recursos, em um nome do hub IoT e na ID do dispositivo.
O endereço IP fornecido durante a execução do assistente de implantação será utilizado para gerar um link de conexão rápida na parte inferior do notebook.

Também será possível compactar um arquivo dacpac em uma pasta e implantá-lo na nova instância do SQL do Azure no Edge como parte do processo.  Caso um arquivo dacpac seja fornecido, uma conta de Armazenamento de Blobs do Azure será criada no mesmo grupo de recursos.

## <a name="multiple-devices-of-an-azure-iot-hub"></a>Vários dispositivos de um Hub IoT do Azure

Caso tenha um hub IoT existente e dispositivos conectados, o SQL do Azure no Edge poderá ser implantado no dispositivo com base no grupo de recursos, em um nome do hub IoT, bem como em uma [condição de destino](https://docs.microsoft.com/azure/iot-edge/module-deployment-monitoring#target-condition) para selecionar o(s) dispositivo(s).
O endereço IP fornecido durante a execução do assistente de implantação será utilizado para gerar um link de conexão rápida na parte inferior do notebook.

Também será possível compactar um arquivo dacpac em uma pasta e implantá-lo na nova instância do SQL do Azure no Edge como parte do processo.  Caso um arquivo dacpac seja fornecido, uma conta de Armazenamento de Blobs do Azure será criada no mesmo grupo de recursos.

## <a name="next-steps"></a>Próximas etapas

- [Saiba mais sobre o SQL do Azure no Edge](https://docs.microsoft.com/azure/azure-sql-edge/)