---
title: Downloads de CAB para atualizações cumulativas SQL Server
description: Downloads de pacote e CAB do r e Python para SQL Server Serviços de Machine Learning e SQL Server 2016 R Services.
ms.prod: sql
ms.technology: machine-learning
ms.date: 07/30/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: ebc5ccef3130a490a6563531dd61e66a0218083d
ms.sourcegitcommit: 0c6c1555543daff23da9c395865dafd5bb996948
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70304820"
---
# <a name="cab-downloads-for-cumulative-updates-of-sql-server-in-database-analytics-instances"></a>Downloads CAB para atualizações cumulativas de SQL Server instâncias de análise no banco de dados

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server instâncias configuradas para análise no banco de dados incluem recursos de R e Python. Esses recursos são fornecidos em arquivos CAB, instalados e atendidos por meio da instalação do SQL Server. Em dispositivos conectados à Internet, as atualizações de CAB normalmente são aplicadas por meio de Windows Update. Em servidores desconectados, os arquivos CAB devem ser baixados e aplicados manualmente. 

Este artigo fornece links de download para arquivos CAB para cada atualização cumulativa. Para obter mais informações sobre instalações offline, consulte [instalar SQL Server componentes de Machine Learning sem acesso à Internet](sql-ml-component-install-without-internet-access.md#apply-cu).

## <a name="prerequisites"></a>Pré-requisitos

Comece com uma instalação de linha de base.

+ No SQL Server Serviços de Machine Learning, a versão inicial é a instalação de linha de base. 
+ No SQL Server R Services 2016, você pode começar com a versão inicial, o SP1 ou o SP2. 

Você também pode aplicar atualizações cumulativas a um servidor autônomo.

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"

## <a name="sql-server-2017-cabs"></a>SQL Server CABs 2017

Os arquivos CAB são listados em ordem cronológica inversa. Ao baixar os arquivos CAB e transferi-los para o computador de destino, coloque-os em uma pasta conveniente, como **downloads** ou a pasta% Temp% do usuário de instalação.

|Versão  |Componente | Link de download  | Problemas resolvidos | 
|---------|----------|----------------|------------------|
|**[SQL Server 2017 CU14](https://support.microsoft.com/help/4484710/)-[CU15](https://support.microsoft.com/help/4498951/)-[CU16](https://support.microsoft.com/help/4508218/)** |  |  |  |
| | Microsoft R Open     | [SRO_3.3.3.1400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2073898&clcid=1033)| Os binários no pacote agora estão assinados. |
| | R Server      |[SRS_9.2.0.1400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2069739&clcid=1033)| Os binários no pacote agora estão assinados. |
| | Microsoft Python Open     | [SPO_9.2.0.1400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2073897&clcid=1033)| Os binários no pacote agora estão assinados. |
| | Servidor Python    |[SPS_9.2.0.1400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2071421&clcid=1033)| Os binários no pacote agora estão assinados.  |
|**[SQL Server 2017 CU13](https://support.microsoft.com/help/4466404)** |  |  |  |
| | Microsoft R Open     | [SRO_3.3.3.1300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| Nenhuma alteração de versões anteriores. |
| | R Server      |[SRS_9.2.0.1300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2038263&clcid=1033)| Contém uma correção para atualizar um [servidor R autônomo operacional](https://docs.microsoft.com/machine-learning-server/what-is-operationalization), conforme instalado por meio da instalação do SQL Server. Use o CABs CU13 e siga [estas instruções](sql-machine-learning-standalone-windows-install.md#apply-cu) para aplicar a atualização. |
| | Microsoft Python Open     | [SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| Nenhuma alteração de versões anteriores. |
| | Servidor Python    |[SPS_9.2.0.1300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2038197&clcid=1033)| Contém uma correção para atualizar um [servidor Python autônomo operacional](https://docs.microsoft.com/machine-learning-server/what-is-operationalization), conforme instalado por meio da instalação do SQL Server. Use o CABs CU13 e siga [estas instruções](sql-machine-learning-standalone-windows-install.md#apply-cu) para aplicar a atualização. |
|**[SQL Server 2017 CU10](https://support.microsoft.com/help/4342123)-[CU11](https://support.microsoft.com/help/4462262)-[CU12](https://support.microsoft.com/help/4464082)** |  |  |  |
| | Microsoft R Open     | [SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| Nenhuma alteração de versões anteriores. |
| | R Server      |[SRS_9.2.0.1000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2006287&clcid=1033)| Correções secundárias.|
| | Microsoft Python Open     | [SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| Nenhuma alteração de versões anteriores. |
| | Servidor Python    |[SPS_9.2.0.1000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2006805&clcid=1033)| Python rx_data_step perde a ordem de linha quando duplicatas são removidas. <br/>SPEE falha na detecção de tipo de dados no índice columnstore clusterizado. <br/>Retorna uma tabela vazia quando colunas contêm todos os valores nulos. |
|**[SQL Server 2017 CU8](https://support.microsoft.com/help/4338363)-[CU9](https://support.microsoft.com/help/4341265)** |  |  |  |
| | Microsoft R Open     | [SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| Nenhuma alteração de versões anteriores. |
| | R Server      |[SRS_9.2.0.800_1033.cab](https://go.microsoft.com/fwlink/?LinkId=874708&clcid=1033)|
| | Microsoft Python Open     | [SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| Nenhuma alteração de versões anteriores. |
| | Servidor Python    |[SPS_9.2.0.800_1033.cab](https://go.microsoft.com/fwlink/?LinkId=874707&clcid=1033)|
|**[SQL Server 2017 CU6](https://support.microsoft.com/help/4101464)-[CU7](https://support.microsoft.com/help/4229789)** |  |  |  |
| | Microsoft R Open     | [SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| Nenhuma alteração de versões anteriores. |
| | R Server      |[SRS_9.2.0.600_1033.cab](https://go.microsoft.com/fwlink/?LinkId=871074&clcid=1033)|
| | Microsoft Python Open     | [SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| Nenhuma alteração de versões anteriores. |
| | Servidor Python    |[SPS_9.2.0.600_1033.cab](https://go.microsoft.com/fwlink/?LinkId=871073&clcid=1033)| Tipos de dados DateTime na consulta SPEES.<br/>mensagens de erro aprimoradas no microsoftml quando modelos pré-treinados estão ausentes.<br/> Correções para funções e variáveis de transformação revoscalepy.|
|**[SQL Server 2017 CU5](https://support.microsoft.com/help/4092643)** |  |  |  |
| | Microsoft R Open     | [SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| Nenhuma alteração de versões anteriores. |
| | R Server      |[SRS_9.2.0.500_1033.cab](https://go.microsoft.com/fwlink/?LinkId=869052&clcid=1033)| Erros relacionados a caminhos longos em rxInstallPackages.<br/>Conexões em um auto-retorno para RxExec.
| | Microsoft Python Open    | Nenhuma alteração de versões anteriores. |
| | Servidor Python    |[SPS_9.2.0.500_1033.cab](https://go.microsoft.com/fwlink/?LinkId=869053&clcid=1033)| <br/>Conexões em um auto-retorno para rx_exec.
|**[SQL Server 2017 CU4](https://support.microsoft.com/help/4056498)** |  |   |  |
| | Microsoft R Open     | [SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| Nenhuma alteração de versões anteriores. |
| | R Server      |[SRS_9.2.0.400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866212&clcid=1033)|
| | Microsoft Python Open     |[SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| Nenhuma alteração de versões anteriores. |
| |  Servidor Python    |[SPS_9.2.0.400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866213&clcid=1033)|
|**[SQL Server 2017 CU3](https://support.microsoft.com/help/4052987)** |  |  |  |
| | Microsoft R Open     |[SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)|
| | R Server      |[SRS_9.2.0.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863893)|
| | Microsoft Python Open     |[SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| Nenhuma alteração de versões anteriores. |
| | Servidor Python    |[SPS_9.2.0.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863892)| Serialização de modelo do Python em revoscalepy, usando a [função rx_serialize_model](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model).<br/>Suporte a [Pontuação nativa](../sql-native-scoring.md) , além de aprimoramentos na [Pontuação em tempo real](../real-time-scoring.md). 
|**[SQL Server 2017 CU1](https://support.microsoft.com/help/4038634)-[CU2](https://support.microsoft.com/help/4052574)** |  |  |  |
| | Microsoft R Open     | [SRO_3.3.3.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851496)| Nenhuma alteração de versões anteriores. |
| | R Server      |[SRS_9.2.0.100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851501)|
| | Microsoft Python Open     | [SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| Nenhuma alteração de versões anteriores. | 
| | Servidor Python    |[SPS_9.2.0.100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851500) | Adiciona rx_create_col_info para retornar informações de esquema. <br/>Aprimoramentos no [rx_exec](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-exec) para dar suporte a cenários paralelos usando o contexto de `RxLocalParallel` computação.|
|**Versão inicial** |  |  |
| | Microsoft R Open     |[SRO_3.3.3.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851496)|
| | R Server      |[SRS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851507)|
| | Microsoft Python Open     |[SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502) |
| | Servidor Python    |[SPS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851508) |

::: moniker-end

::: moniker range=">=sql-server-2016||=sqlallproducts-allversions"

<a name="bkmk_2016Installers"></a>

## <a name="sql-server-2016-cabs"></a>SQL Server CABs 2016

Para os SQL Server R Services 2016, as versões de linha de base são a versão RTM ou uma versão service pack.

|Versão  |Link de download  |
|---------|---------------|
|**SQL Server 2016 SP2 CU6**     |
|Microsoft R Open     |[SRO_3.2.2.20100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2079936&clcid=1033)|
|Microsoft R Server    |[SRS_8.0.3.20100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2079933&clcid=1033)|
|**SQL Server 2016 SP2 CU1-CU5**     |
|Microsoft R Open     |[SRO_3.2.2.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836819)|
|Microsoft R Server    |[SRS_8.0.3.20000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866038)|
|**SQL Server 2016 SP2**     |
|Microsoft R Open     |[SRO_3.2.2.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836819)|
|Microsoft R Server    |[SRS_8.0.3.17000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=850317)|
|**SQL Server 2016 SP1 CU14**     |
|Microsoft R Open     |[SRO_3.2.2.16100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2080130&clcid=1033)|
|Microsoft R Server    |[SRS_8.0.3.17200_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2079935&clcid=1033)|
|**SQL Server 2016 SP1 CU1-CU13**     |
|Microsoft R Open     |[SRO_3.2.2.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836819)|
|Microsoft R Server    |[SRS_8.0.3.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836818)|
|**SQL Server 2016 SP1**     |
|Microsoft R Open     |[SRO_3.2.2.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824879)|
|Microsoft R Server     |[SRS_8.0.3.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824881)|
|**SQL Server 2016 CU4-CU9**     |
|Microsoft R Open     |[SRO_3.2.2.13000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=831785)|
|Microsoft R Server     |[SRS_8.0.3.13000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=831676)|
|**SQL Server 2016 CU2-CU3**     |
|Microsoft R Open     |[SRO_3.2.2.12000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=827398)|
|Microsoft R Server     |[SRS_8.0.3.12000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=827399)|
|**SQL Server 2016 CU1**     |
|Microsoft R Open     |[SRO_3.2.2.10000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=808803)|
|Microsoft R Server     |[SRS_8.0.3.10000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=808805)|
|**SQL Server 2016 RTM**     |
|Microsoft R Open     |[SRO_3.2.2.803_1033.cab](https://go.microsoft.com/fwlink/?LinkId=761266)|
|Microsoft R Server     |[SRS_8.0.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=735051)|

> [!NOTE]
> 
> Ao instalar SQL Server 2016 SP1 CU4 ou SP1 CU5 offline, baixe SRO_ 3.2.2.16000 _1033. cab. Se você baixou SRO_ 3.2.2.13000 _1033. cab de FWLINK 831785 conforme indicado na caixa de diálogo de instalação, renomeie o arquivo como SRO_ 3.2.2.16000. cab antes de instalar a atualização cumulativa.

Se você quiser exibir o código-fonte do Microsoft R, ele estará disponível para download como um arquivo morto no formato. tar: [Baixar instaladores do R Server](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows#download)

::: moniker-end

## <a name="next-steps"></a>Próximas etapas

[Aplicar atualizações cumulativas em computadores sem acesso à Internet](sql-ml-component-install-without-internet-access.md#apply-cu)

[Aplicar atualizações cumulativas em computadores com conectividade com a Internet](sql-ml-component-install-without-internet-access.md#apply-cu)

[Aplicar atualizações cumulativas a um servidor autônomo](sql-machine-learning-standalone-windows-install.md#apply-cu)
