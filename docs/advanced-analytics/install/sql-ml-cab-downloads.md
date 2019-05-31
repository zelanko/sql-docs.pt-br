---
title: Downloads do CAB para atualizações cumulativas do SQL Server - aprendizagem de máquina do SQL Server
description: R e Python CAB e o pacote baixa para serviços de aprendizado de máquina do SQL Server 2017 e o SQL Server 2016 R Services.
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/30/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 3c5c27186969db01cc90fa43a6cf4ec2774ab051
ms.sourcegitcommit: fc0eb955b41c9c508a1fe550eb5421c05fbf11b4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/30/2019
ms.locfileid: "66403234"
---
# <a name="cab-downloads-for-cumulative-updates-of-sql-server-in-database-analytics-instances"></a>Downloads do CAB para atualizações cumulativas de análise do SQL Server no banco de dados de instâncias

Instâncias do SQL Server que estão configuradas para análise no banco de dados incluem recursos de R e Python. Esses recursos são enviados em arquivos CAB, instalado e atendidos por meio da instalação do SQL Server. Em dispositivos conectados à internet, o CAB atualizações normalmente são aplicadas por meio do Windows Update. Em servidores desconectados, os arquivos CAB devem ser baixados e aplicados manualmente. 

Este artigo fornece links de download para os arquivos CAB para cada atualização cumulativa. São fornecidos links para os SQL Server 2017 serviços Machine Learning (R e Python), bem como SQL Server 2016 R Services. Para obter mais informações sobre instalações offline, consulte [componentes sem acesso à internet de aprendizado de máquina de instalar o SQL Server](sql-ml-component-install-without-internet-access.md#apply-cu).

## <a name="prerequisites"></a>Prerequisites

Comece com uma instalação de linha de base.

+ Em serviços do SQL Server 2017 Machine Learning, a versão inicial é a instalação de linha de base. 
+ No SQL Server 2016 R Services, você pode iniciar com a versão inicial, SP1 ou SP2. 

Você também pode aplicar atualizações cumulativas para um servidor autônomo.

## <a name="sql-server-2017-cabs"></a>SQL Server 2017 CABs

Arquivos CAB são listados em ordem cronológica inversa. Quando você baixar os arquivos CAB e transferi-las para o computador de destino, colocá-los em uma pasta conveniente, como **Downloads** ou pasta do usuário da instalação % temp %.

|Versão  |Componente | Link de download  | Problemas resolvidos | 
|---------|----------|----------------|------------------|
|**[SQL Server 2017 CU14](https://support.microsoft.com/help/4484710/)-[CU15](https://support.microsoft.com/help/4498951/)** |  |  |  |
| | Microsoft R Open     | [SRO_3.3.3.1400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2073898&clcid=1033)| Binários de dentro do pacote agora estão conectados. |
| | R Server      |[SRS_9.2.0.1400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2069739&clcid=1033)| Binários de dentro do pacote agora estão conectados. |
| | Microsoft Python Open     | [SPO_9.2.0.1400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2073897&clcid=1033)| Binários de dentro do pacote agora estão conectados. |
| | Python Server    |[SPS_9.2.0.1400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2071421&clcid=1033)| Binários de dentro do pacote agora estão conectados.  |
|**[SQL Server 2017 CU13](https://support.microsoft.com/help/4466404)** |  |  |  |
| | Microsoft R Open     | [SRO_3.3.3.1300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| Nenhuma alteração de versões anteriores. |
| | R Server      |[SRS_9.2.0.1300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2038263&clcid=1033)| Contém uma correção para atualizar uma [operacionalizados R Server autônomo](https://docs.microsoft.com/machine-learning-server/what-is-operationalization), como instalado por meio da instalação do SQL Server. Use o CU13 CABs e siga [estas instruções](sql-machine-learning-standalone-windows-install.md#apply-cu) para aplicar a atualização. |
| | Microsoft Python Open     | [SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| Nenhuma alteração de versões anteriores. |
| | Python Server    |[SPS_9.2.0.1300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2038197&clcid=1033)| Contém uma correção para atualizar uma [operacionalizados Server Python autônomo](https://docs.microsoft.com/machine-learning-server/what-is-operationalization), como instalado por meio da instalação do SQL Server. Use o CU13 CABs e siga [estas instruções](sql-machine-learning-standalone-windows-install.md#apply-cu) para aplicar a atualização. |
|**[SQL Server 2017 CU10](https://support.microsoft.com/help/4342123)-[CU11](https://support.microsoft.com/help/4462262)-[CU12](https://support.microsoft.com/help/4464082)** |  |  |  |
| | Microsoft R Open     | [SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| Nenhuma alteração de versões anteriores. |
| | R Server      |[SRS_9.2.0.1000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2006287&clcid=1033)| Correções secundárias.|
| | Microsoft Python Open     | [SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| Nenhuma alteração de versões anteriores. |
| | Python Server    |[SPS_9.2.0.1000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2006805&clcid=1033)| Python rx_data_step perde a ordem de linha quando as duplicatas são removidas. <br/>SPEE Falha na detecção de tipo de dados em um índice columnstore clusterizado. <br/>Retorna uma tabela vazia quando as colunas contêm todos os valores nulos. |
|**[SQL Server 2017 CU8](https://support.microsoft.com/help/4338363)-[CU9](https://support.microsoft.com/help/4341265)** |  |  |  |
| | Microsoft R Open     | [SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| Nenhuma alteração de versões anteriores. |
| | R Server      |[SRS_9.2.0.800_1033.cab](https://go.microsoft.com/fwlink/?LinkId=874708&clcid=1033)|
| | Microsoft Python Open     | [SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| Nenhuma alteração de versões anteriores. |
| | Python Server    |[SPS_9.2.0.800_1033.cab](https://go.microsoft.com/fwlink/?LinkId=874707&clcid=1033)|
|**[SQL Server 2017 CU6](https://support.microsoft.com/help/4101464)-[CU7](https://support.microsoft.com/help/4229789)** |  |  |  |
| | Microsoft R Open     | [SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| Nenhuma alteração de versões anteriores. |
| | R Server      |[SRS_9.2.0.600_1033.cab](https://go.microsoft.com/fwlink/?LinkId=871074&clcid=1033)|
| | Microsoft Python Open     | [SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| Nenhuma alteração de versões anteriores. |
| | Python Server    |[SPS_9.2.0.600_1033.cab](https://go.microsoft.com/fwlink/?LinkId=871073&clcid=1033)| Tipos de dados de data e hora na consulta SPEES.<br/>aprimorada a mensagens de erro em microsoftml quando modelos previamente treinados estão ausentes.<br/> Correções para revoscalepy transformam funções e variáveis.|
|**[SQL Server 2017 CU5](https://support.microsoft.com/help/4092643)** |  |  |  |
| | Microsoft R Open     | [SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| Nenhuma alteração de versões anteriores. |
| | R Server      |[SRS_9.2.0.500_1033.cab](https://go.microsoft.com/fwlink/?LinkId=869052&clcid=1033)| Erros de caminho longo relacionados no rxInstallPackages.<br/>Conexões em um loopback para RxExec.
| | Microsoft Python Open    | Nenhuma alteração de versões anteriores. |
| | Python Server    |[SPS_9.2.0.500_1033.cab](https://go.microsoft.com/fwlink/?LinkId=869053&clcid=1033)| <br/>Conexões em um loopback para rx_exec.
|**[SQL Server 2017 CU4](https://support.microsoft.com/help/4056498)** |  |   |  |
| | Microsoft R Open     | [SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| Nenhuma alteração de versões anteriores. |
| | R Server      |[SRS_9.2.0.400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866212&clcid=1033)|
| | Microsoft Python Open     |[SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| Nenhuma alteração de versões anteriores. |
| |  Python Server    |[SPS_9.2.0.400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866213&clcid=1033)|
|**[SQL Server 2017 CU3](https://support.microsoft.com/help/4052987)** |  |  |  |
| | Microsoft R Open     |[SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)|
| | R Server      |[SRS_9.2.0.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863893)|
| | Microsoft Python Open     |[SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| Nenhuma alteração de versões anteriores. |
| | Python Server    |[SPS_9.2.0.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863892)| Revoscalepy, a serialização do modelo de Python usando o [rx_serialize_model função](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model).<br/>[Pontuação nativa](../sql-native-scoring.md) suporte, além de aprimoramentos [pontuação em tempo real](../real-time-scoring.md). 
|**[SQL Server 2017 CU1](https://support.microsoft.com/help/4038634)-[CU2](https://support.microsoft.com/help/4052574)** |  |  |  |
| | Microsoft R Open     | [SRO_3.3.3.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851496)| Nenhuma alteração de versões anteriores. |
| | R Server      |[SRS_9.2.0.100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851501)|
| | Microsoft Python Open     | [SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| Nenhuma alteração de versões anteriores. | 
| | Python Server    |[SPS_9.2.0.100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851500) | Adiciona rx_create_col_info para retornar informações de esquema. <br/>Aprimoramentos [rx_exec](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-exec) para dar suporte a cenários paralelos usando o `RxLocalParallel` contexto de computação.|
|**Versão inicial** |  |  |
| | Microsoft R Open     |[SRO_3.3.3.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851496)|
| | R Server      |[SRS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851507)|
| | Microsoft Python Open     |[SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502) |
| | Python Server    |[SPS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851508) |


<a name="bkmk_2016Installers"></a>

## <a name="sql-server-2016-cabs"></a>SQL Server 2016 CABs

Para SQL Server 2016 R Services, as versões de linha de base são a versão RTM ou uma versão de service pack.

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
> Ao instalar o SQL Server 2016 SP1 CU4 ou SP1 CU5 offline, faça o download SRO_3.2.2.16000_1033.cab. Se você baixou SRO_3.2.2.13000_1033.cab da 831785 FWLINK conforme indicado na caixa de diálogo de instalação, renomeie o arquivo como SRO_3.2.2.16000_1033.cab antes de instalar a atualização cumulativa.

Se você quiser exibir o código-fonte para o Microsoft R, ela está disponível para download como um arquivo no formato. tar: [Baixe os instaladores do R Server](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows#download)

## <a name="see-also"></a>Confira também

[Aplicar atualizações cumulativas em computadores sem acesso à internet](sql-ml-component-install-without-internet-access.md#apply-cu)

[Aplicar atualizações cumulativas em computadores que possuem conectividade com a internet](sql-ml-component-install-without-internet-access.md#apply-cu)

[Aplicar atualizações cumulativas para um servidor autônomo](sql-machine-learning-standalone-windows-install.md#apply-cu)
