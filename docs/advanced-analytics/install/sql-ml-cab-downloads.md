---
title: Baixar atualizações para instalação offline
description: Baixe arquivos CAB do Python e do R para os Serviços de Machine Learning do SQL Server. Esses arquivos CAB contêm atualizações do recurso Serviços de Machine Learning (Python e R) e são usados ao instalar o SQL Server em um servidor sem acesso à Internet.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/07/2020
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: b2b84349e60bf89a066fb2157a9c521d7be8ecbd
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "75776517"
---
# <a name="cab-downloads-for-cumulative-updates-of-sql-server-machine-learning-services"></a>Downloads do CAB para atualizações cumulativas dos Serviços de Machine Learning do SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
Baixe arquivos CAB do Python e do R para os Serviços de Machine Learning do SQL Server. Esses arquivos CAB contêm atualizações do recurso Serviços de Machine Learning (Python e R) e são usados ao instalar o SQL Server em um servidor sem acesso à Internet.
::: moniker-end

::: moniker range=">=sql-server-2016||=sqlallproducts-allversions"
Baixe arquivos CAB do Python e do R para o SQL Server 2016 R Services. Esses arquivos CAB contêm atualizações do recurso R Services e são usados ao instalar o SQL Server em um servidor sem acesso à Internet.
::: moniker-end

Abaixo, você encontrará links de download para os arquivos CAB de cada atualização cumulativa. Para obter mais informações sobre instalações offline, confira [Instalar componentes de aprendizado de máquina do SQL Server sem acesso à Internet](sql-ml-component-install-without-internet-access.md#apply-cu).

## <a name="prerequisites"></a>Prerequisites

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
Comece com uma instalação de linha de base. Nos Serviços de Machine Learning do SQL Server, a versão inicial é a instalação de linha de base. 
::: moniker-end

::: moniker range=">=sql-server-2016||=sqlallproducts-allversions"
Comece com uma instalação de linha de base.  No SQL Server 2016 R Services, você pode começar com a versão inicial, o SP1 ou o SP2. 
::: moniker-end

Aplique também atualizações cumulativas.

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"

## <a name="sql-server-2017-cabs"></a>CABs do SQL Server 2017

Os arquivos CAB são listados na ordem cronológica inversa. Ao baixar os arquivos CAB e transferi-los para o computador de destino, coloque-os em uma pasta conveniente como **Downloads** ou na pasta %temp% do usuário de instalação.

|Versão  |Componente | Link de download  | Problemas resolvidos | 
|---------|----------|----------------|------------------|
|**[SQL Server 2017 CU14](https://support.microsoft.com/help/4484710/)-[CU15](https://support.microsoft.com/help/4498951/)-[CU16](https://support.microsoft.com/help/4508218/)** |  |  |  |
| | Microsoft R Open     | [SRO_3.3.3.1400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2073898&clcid=1033)| Os binários no pacote agora estão assinados. |
| | R Server      |[SRS_9.2.0.1400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2069739&clcid=1033)| Os binários no pacote agora estão assinados. |
| | Microsoft Python Open     | [SPO_9.2.0.1400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2073897&clcid=1033)| Os binários no pacote agora estão assinados. |
| | Python Server    |[SPS_9.2.0.1400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2071421&clcid=1033)| Os binários no pacote agora estão assinados.  |
|**[SQL Server 2017 CU13](https://support.microsoft.com/help/4466404)** |  |  |  |
| | Microsoft R Open     | [SRO_3.3.3.1300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| Nenhuma alteração das versões anteriores. |
| | R Server      |[SRS_9.2.0.1300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2038263&clcid=1033)| Contém uma correção para a atualização de um [R Server autônomo operacionalizado](https://docs.microsoft.com/machine-learning-server/what-is-operationalization), conforme instalado por meio da instalação do SQL Server. Use os CABs CU13 e siga [estas instruções](sql-machine-learning-standalone-windows-install.md#apply-cu) para aplicar a atualização. |
| | Microsoft Python Open     | [SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| Nenhuma alteração das versões anteriores. |
| | Python Server    |[SPS_9.2.0.1300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2038197&clcid=1033)| Contém uma correção para a atualização de um [Python Server autônomo operacionalizado](https://docs.microsoft.com/machine-learning-server/what-is-operationalization), conforme instalado por meio da instalação do SQL Server. Use os CABs CU13 e siga [estas instruções](sql-machine-learning-standalone-windows-install.md#apply-cu) para aplicar a atualização. |
|**[SQL Server 2017 CU10](https://support.microsoft.com/help/4342123)-[CU11](https://support.microsoft.com/help/4462262)-[CU12](https://support.microsoft.com/help/4464082)** |  |  |  |
| | Microsoft R Open     | [SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| Nenhuma alteração das versões anteriores. |
| | R Server      |[SRS_9.2.0.1000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2006287&clcid=1033)| Correções secundárias.|
| | Microsoft Python Open     | [SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| Nenhuma alteração das versões anteriores. |
| | Python Server    |[SPS_9.2.0.1000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2006805&clcid=1033)| O rx_data_step do Python deixa as linhas na ordem incorreta quando as duplicatas são removidas. <br/>O SPEE falha na detecção de tipo de dados no índice columnstore clusterizado. <br/>Retorna uma tabela vazia quando as colunas contêm todos os valores nulos. |
|**[SQL Server 2017 CU8](https://support.microsoft.com/help/4338363)-[CU9](https://support.microsoft.com/help/4341265)** |  |  |  |
| | Microsoft R Open     | [SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| Nenhuma alteração das versões anteriores. |
| | R Server      |[SRS_9.2.0.800_1033.cab](https://go.microsoft.com/fwlink/?LinkId=874708&clcid=1033)|
| | Microsoft Python Open     | [SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| Nenhuma alteração das versões anteriores. |
| | Python Server    |[SPS_9.2.0.800_1033.cab](https://go.microsoft.com/fwlink/?LinkId=874707&clcid=1033)|
|**[SQL Server 2017 CU6](https://support.microsoft.com/help/4101464)-[CU7](https://support.microsoft.com/help/4229789)** |  |  |  |
| | Microsoft R Open     | [SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| Nenhuma alteração das versões anteriores. |
| | R Server      |[SRS_9.2.0.600_1033.cab](https://go.microsoft.com/fwlink/?LinkId=871074&clcid=1033)|
| | Microsoft Python Open     | [SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| Nenhuma alteração das versões anteriores. |
| | Python Server    |[SPS_9.2.0.600_1033.cab](https://go.microsoft.com/fwlink/?LinkId=871073&clcid=1033)| Tipos de dados DateTime na consulta do SPEES.<br/>Mensagens de erro aprimoradas no microsoftml quando modelos pré-treinados estão ausentes.<br/> Correções para funções e variáveis de transformação revoscalepy.|
|**[SQL Server 2017 CU5](https://support.microsoft.com/help/4092643)** |  |  |  |
| | Microsoft R Open     | [SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| Nenhuma alteração das versões anteriores. |
| | R Server      |[SRS_9.2.0.500_1033.cab](https://go.microsoft.com/fwlink/?LinkId=869052&clcid=1033)| Erros relacionados a caminhos longos em rxInstallPackages.<br/>Conexões em um loopback para RxExec.
| | Microsoft Python Open    | Nenhuma alteração das versões anteriores. |
| | Python Server    |[SPS_9.2.0.500_1033.cab](https://go.microsoft.com/fwlink/?LinkId=869053&clcid=1033)| <br/>Conexões em um loopback para rx_exec.
|**[SQL Server 2017 CU4](https://support.microsoft.com/help/4056498)** |  |   |  |
| | Microsoft R Open     | [SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| Nenhuma alteração das versões anteriores. |
| | R Server      |[SRS_9.2.0.400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866212&clcid=1033)|
| | Microsoft Python Open     |[SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| Nenhuma alteração das versões anteriores. |
| |  Python Server    |[SPS_9.2.0.400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866213&clcid=1033)|
|**[SQL Server 2017 CU3](https://support.microsoft.com/help/4052987)** |  |  |  |
| | Microsoft R Open     |[SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)|
| | R Server      |[SRS_9.2.0.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863893)|
| | Microsoft Python Open     |[SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| Nenhuma alteração das versões anteriores. |
| | Python Server    |[SPS_9.2.0.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863892)| Serialização de modelo do Python em revoscalepy, usando a função [rx_serialize_model](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model).<br/>Suporte à [pontuação nativa](../sql-native-scoring.md), além de aprimoramentos à [pontuação em tempo real](../real-time-scoring.md). 
|**[SQL Server 2017 CU1](https://support.microsoft.com/help/4038634)-[CU2](https://support.microsoft.com/help/4052574)** |  |  |  |
| | Microsoft R Open     | [SRO_3.3.3.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851496)| Nenhuma alteração das versões anteriores. |
| | R Server      |[SRS_9.2.0.100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851501)|
| | Microsoft Python Open     | [SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| Nenhuma alteração das versões anteriores. | 
| | Python Server    |[SPS_9.2.0.100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851500) | Adiciona rx_create_col_info para retornar informações de esquema. <br/>Aprimoramentos a [rx_exec](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-exec) para oferecer suporte a cenários paralelos usando o contexto de computação de `RxLocalParallel`.|
|**Versão inicial** |  |  |
| | Microsoft R Open     |[SRO_3.3.3.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851496)|
| | R Server      |[SRS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851507)|
| | Microsoft Python Open     |[SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502) |
| | Python Server    |[SPS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851508) |

::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"

<a name="bkmk_2016Installers"></a>

## <a name="sql-server-2016-cabs"></a>CABs do SQL Server 2016

Para o SQL Server 2016 R Services, as versões de linha de base são a versão RTM ou uma versão do service pack.

|Versão  |Link de download  |
|---------|---------------|
|**SQL Server 2016 SP2 CU6**     |
|Microsoft R Open     |[SRO_3.2.2.20100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2079936&clcid=1033)|
|Servidor R da Microsoft    |[SRS_8.0.3.20100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2079933&clcid=1033)|
|**SQL Server 2016 SP2 CU1-CU5**     |
|Microsoft R Open     |[SRO_3.2.2.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836819)|
|Servidor R da Microsoft    |[SRS_8.0.3.20000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866038)|
|**SQL Server 2016 SP2**     |
|Microsoft R Open     |[SRO_3.2.2.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836819)|
|Servidor R da Microsoft    |[SRS_8.0.3.17000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=850317)|
|**SQL Server 2016 SP1 CU14**     |
|Microsoft R Open     |[SRO_3.2.2.16100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2080130&clcid=1033)|
|Servidor R da Microsoft    |[SRS_8.0.3.17200_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2079935&clcid=1033)|
|**SQL Server 2016 SP1 CU1-CU13**     |
|Microsoft R Open     |[SRO_3.2.2.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836819)|
|Servidor R da Microsoft    |[SRS_8.0.3.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836818)|
|**SQL Server 2016 SP1**     |
|Microsoft R Open     |[SRO_3.2.2.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824879)|
|Servidor R da Microsoft     |[SRS_8.0.3.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824881)|
|**SQL Server 2016 CU4-CU9**     |
|Microsoft R Open     |[SRO_3.2.2.13000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=831785)|
|Servidor R da Microsoft     |[SRS_8.0.3.13000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=831676)|
|**SQL Server 2016 CU2-CU3**     |
|Microsoft R Open     |[SRO_3.2.2.12000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=827398)|
|Servidor R da Microsoft     |[SRS_8.0.3.12000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=827399)|
|**SQL Server 2016 CU1**     |
|Microsoft R Open     |[SRO_3.2.2.10000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=808803)|
|Servidor R da Microsoft     |[SRS_8.0.3.10000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=808805)|
|**SQL Server 2016 RTM**     |
|Microsoft R Open     |[SRO_3.2.2.803_1033.cab](https://go.microsoft.com/fwlink/?LinkId=761266)|
|Servidor R da Microsoft     |[SRS_8.0.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=735051)|

> [!NOTE]
> 
> Ao instalar o SQL Server 2016 SP1 CU4 ou SP1 CU5 offline, baixe o arquivo SRO_3.2.2.16000_1033.cab. Se você baixou o arquivo SRO_3.2.2.13000_1033.cab do FWLINK 831785 conforme indicado na caixa de diálogo de instalação, renomeie o arquivo como SRO_3.2.2.16000_1033.cab antes de instalar a atualização cumulativa.

Caso você queira exibir o código-fonte para o Microsoft R, ele estará disponível para download como um arquivo no formato .tar: [Baixar instaladores do R Server](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows#download)

::: moniker-end

## <a name="next-steps"></a>Próximas etapas

[Aplicar atualizações cumulativas em computadores sem acesso à Internet](sql-ml-component-install-without-internet-access.md#apply-cu)

[Aplicar atualizações cumulativas em computadores com conectividade à Internet](sql-ml-component-install-without-internet-access.md#apply-cu)

[Aplicar atualizações cumulativas a um servidor autônomo](sql-machine-learning-standalone-windows-install.md#apply-cu)
