---
title: "Instalação de componentes de aprendizado de máquina sem acesso à internet | Microsoft Docs"
ms.custom: 
ms.date: 03/05/2018
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0a90c438-d78b-47be-ac05-479de64378b2
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: d7d218dcb5efeddf248230abff85b46da23d389a
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/08/2018
---
# <a name="installing-machine-learning-components-without-internet-access"></a>Instalação de componentes de aprendizado de máquina sem acesso à internet
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Como os componentes de R e Python fornecidos com o SQL Server 2016 e o SQL Server 2017 são código-fonte aberto, Microsoft não instala componentes de R ou Python por padrão. Em vez disso, podemos fornecer os instaladores relacionados e vem pacotes como uma conveniência no Microsoft Download Center e outros sites confiáveis. Você deve concordar com a licença apropriada e, em seguida, o programa de instalação do SQL Server instala os componentes de R ou Python para você.

Este tópico fornece os locais de download para os instaladores e uma visão geral do processo de instalação offline.

## <a name="overview-of-the-offline-installation-process"></a>Visão geral do processo de instalação offline

Normalmente, a instalação dos componentes de máquina usada no SQL Server 2016 e no SQL Server 2017 requer uma conexão de internet. Quando a instalação do SQL Server é executado, se você selecionou qualquer a opções de aprendizado de máquina, a instalação verifica o Python ou R instaladores, como bem como quaisquer outros componentes necessários.

+ **Se o computador tiver uma conexão de internet**

    SQL Server localiza e baixa os componentes para você e instala-los durante a instalação. Aceite os termos de licença separadamente para cada componente do código-fonte aberto (R ou Python) que você instalar.

+ **Se o computador não tiver acesso à internet**

    Você deve baixar os instaladores adicionais antes de continuar com a instalação. No mínimo, baixe os instaladores de R ou Python com suporte para a versão do SQL Server que você está instalando.

    Dependendo da configuração do servidor, talvez seja necessário componentes adicionais.  Consulte [componentes adicionais](#bkmk_OtherComponents) para obter detalhes.

    Depois de baixar os instaladores, você usá-los ao instalar o recurso como parte da instalação do SQL Server.

### <a name="step-1-obtain-additional-installers"></a>Etapa 1. Obter instaladores adicionais

Em geral, instaladores separadas são fornecidas para código-fonte aberto e componentes proprietárias. O Assistente de instalação do SQL Server garante que eles estão instalados na ordem correta. No entanto, algumas versões, poderá atualizar apenas um conjunto de componentes. Consulte o [tabela instaladores de](#bkmk_2017Installers) por versão para obter detalhes.

**Para R**

A linguagem R tem suporte no SQL Server 2016 e posterior. 

+ Instaladores com **SRO** no nome do fornecem os componentes de software livre.
+ Instaladores com **SRS** no nome contém componentes fornecidos pela Microsoft, incluindo aqueles para integração com o banco de dados.

**Para Python**

A linguagem Python requer o SQL Server 2017 ou posterior. 

+ Instaladores com **SPO** no nome são para abrir o Microsoft Python e fornecer os componentes de software livre.
+ Instaladores com **SPS** no nome são para o servidor do Microsoft Python e contêm componentes fornecidos pela Microsoft, incluindo aqueles para integração com o banco de dados.

**Como fazer o download**

1. Baixe os instaladores do [sites Microsoft Download Center](#installerlocs) em um computador com acesso à internet e salve o instalador em vez de executá-lo.
2. Copie os arquivos do instalador (CAB) no computador onde você pretende instalar componentes de aprendizado de máquina.
3. No SQL Server 2016, o Assistente de instalação instalado inglês por padrão. Para instalar usando um idioma diferente necessária a modificação do nome de arquivo do instalador, conforme descrito aqui: [as modificações necessárias para diferentes idiomas](#modslocales).
    Para o SQL Server 2017, o idioma correto é identificado com base na localidade de instância.
4. Baixe os componentes adicionais que são necessários, como MPI ou .NET Core.
5. Opcionalmente, você pode baixar o código-fonte arquivado para os componentes de software livre, mas isso não é necessário para a instalação do SQL Server e pode ser concluído a qualquer momento. Para obter mais informações, consulte [R Server para Windows](https://docs.microsoft.com/r-server/install/r-server-install-windows).

Para obter instruções passo a passo do processo de instalação offline de serviços do R no SQL Server 2016, recomendamos que o artigo do [equipe de consultoria ao cliente do SQL Server](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/do-it-right-deploying-sql-server-r-services-on-computers-without-internet-access/). o artigo inclui capturas de tela e também abrange cenários de instalação de patches e integrada.

### <a name="step-2-run-offline-setup-using-the-sql-server-setup-wizard"></a>Etapa 2. Execute a instalação offline usando o Assistente de instalação do SQL Server

1. Execute o assistente de instalação do SQL Server.
2. Quando o Assistente de instalação exibe a página de licenciamento, clique em **aceitar**.
3. Uma caixa de diálogo abre que solicita o **caminho instalar** os pacotes necessários.
4. Clique em **procurar** para localizar a pasta que contém os arquivos de instalação que você copiou anteriormente.
5. Se os arquivos corretos forem encontrados, você poderá clicar em **Avançar** para indicar que os componentes estão disponíveis.
6. Conclua o Assistente de instalação do SQL Server.
7. Execute as etapas de pós-instalação necessárias para se certificar de que o serviço está habilitado.

## <a name="installerlocs"></a>Onde baixar componentes de aprendizado de máquina

Certifique-se de obter os arquivos que correspondem à versão do SQL Server que você está instalando.

+ [Para obter componentes de R para o SQL Server 2016](#bkmk_2016Installers)

+ [Para obter componentes de R ou Python para o SQL Server 2017](#bkmk_2017Installers)

É fornecido suporte para Python começando com o SQL Server de 2017 CTP 2.0. Em versões anteriores, incluindo o SQL Server 2016, não dão suporte a Python.

### <a name="bkmk_2017Installers"></a>Downloads do SQL Server de 2017

Versão  |Link de download  |
---------|---------|
**SQL Server 2017 CTP 1**     |
Microsoft R Open     |[SRO_3.3.0.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836819)
Microsoft R Server     |[SRS_9.0.0.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836818)
**SQL Server 2017 CTP 1.1** |
Microsoft R Open     |[SRO_3.3.2.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=834568)
Microsoft R Server     |[SRS_9.0.1.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=834567)
**SQL Server 2017 CTP 1.4** |
Microsoft R Open     |[SRO_3.3.2.100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=842483)
Microsoft R Server     |[SRS_9.0.2.100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=842482)
**SQL Server 2017 CTP 2.0** |
Microsoft R Open     |[SRO_3.3.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=842800)
Microsoft R Server     |[SRS_9.1.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=842799)
Abrir Microsoft Python     |[SPO_9.1.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=842828)
Microsoft Python Server    |[SPS_9.1.0.0__1033.cab](https://go.microsoft.com/fwlink/?LinkId=842848)
**SQL Server 2017 RC1** |
Microsoft R Open     |[SRO_3.3.3.22_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851503)|
Microsoft R Server     |[SRS_9.2.0.22_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851498)|
Abrir Microsoft Python     |[SPO_9.2.0.22_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851499)|
Microsoft Python Server    |[SPS_9.2.0.22_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851504)|
**SQL Server 2017 RC 2** |
Microsoft R Open     |[SRO_3.3.3.23_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851493)|
Microsoft R Server     |[SRS_9.2.0.23_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851505)|
Abrir Microsoft Python     |[SPO_9.2.0.23_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851506)|
Microsoft Python Server    |[SPS_9.2.0.23_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851497)|
**SQL Server 2017 RTM** |
Microsoft R Open     |[SRO_3.3.3.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851496)|
Microsoft R Server      |[SRS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851507)|
Abrir Microsoft Python     |[SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502) |
Microsoft Python Server    |[SPS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851508) |
**SQL Server 2017 CU1** |
Microsoft R Open     |Nenhuma alteração; uso anterior|
Microsoft R Server      |[SRS_9.2.0.100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851501)|
Abrir Microsoft Python     |Nenhuma alteração; uso anterior |
Microsoft Python Server    |[SPS_9.2.0.100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851500) |
**SQL Server 2017 CU2** |
Microsoft R Open     |Nenhuma alteração; uso anterior|
Microsoft R Server      |Nenhuma alteração; uso anterior|
Abrir Microsoft Python     |Nenhuma alteração; uso anterior|
Microsoft Python Server    |Nenhuma alteração; uso anterior|
**SQL Server 2017 CU3** |
Microsoft R Open     |[SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)|
Microsoft R Server      |[SRS_9.2.0.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863893)|
Abrir Microsoft Python     |Nenhuma alteração; uso anterior|
Microsoft Python Server    |[SPS_9.2.0.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863892)|
**SQL Server 2017 CU4** |
Microsoft R Open     |Nenhuma alteração; uso anterior|
Microsoft R Server      |[SRS_9.2.0.400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866212&clcid=1033)|
Abrir Microsoft Python     |Nenhuma alteração; uso anterior|
Microsoft Python Server    |[SPS_9.2.0.400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866213&clcid=1033)|

### <a name="bkmk_2016Installers"></a>Downloads do SQL Server 2016

> [!IMPORTANT]
> 
> Ao instalar o SQL Server 2016 SP1 CU4 ou CU5 SP1 offline, faça o download de SRO_3.2.2.16000_1033.cab. Se você baixou SRO_3.2.2.13000_1033.cab da 831785 FWLINK conforme indicado na caixa de diálogo de instalação, renomeie o arquivo como SRO_3.2.2.16000_1033.cab antes de instalar a atualização cumulativa.

Versão  |Link de download  |
---------|---------|
**SQL Server 2016 RTM**     |
Microsoft R Open     |[SRO_3.2.2.803_1033.cab](https://go.microsoft.com/fwlink/?LinkId=761266)
Microsoft R Server     |[SRS_8.0.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=735051)
**SQL Server 2016 CU 1**     |
Microsoft R Open     |[SRO_3.2.2.10000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=808803)
Microsoft R Server     |[SRS_8.0.3.10000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=808805)
**SQL Server 2016 CU 2**     |
Microsoft R Open     |[SRO_3.2.2.12000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=827398)
Microsoft R Server     |[SRS_8.0.3.12000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=827399)
**SQL Server 2016 CU 3**     |
Microsoft R Open     |Nenhuma alteração; uso anterior|
Microsoft R Server     | Nenhuma alteração; uso anterior |
**SQL Server 2016 CU 4**     |
Microsoft R Open     |[SRO_3.2.2.13000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=831785)|
Microsoft R Server     |[SRS_8.0.3.13000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=831676)|
**SQL Server 2016 CU 5**     |
Microsoft R Open     |Nenhuma alteração; uso anterior|
Microsoft R Server     |Nenhuma alteração; uso anterior|
**SQL Server 2016 CU 6**     |
Microsoft R Open     |Nenhuma alteração; uso anterior|
Microsoft R Server     |[SRS_8.0.3.14000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=850316)  |
**SQL Server 2016 CU 7**     |
Microsoft R Open     |Nenhuma alteração; uso anterior|
Microsoft R Server     |Nenhuma alteração; uso anterior |
**SQL Server 2016 SP 1**     |
Microsoft R Open     |[SRO_3.2.2.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824879)
Microsoft R Server     |[SRS_8.0.3.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824881)
**SQL Server 2016 SP 1 CU1**     |
Microsoft R Open     |Nenhuma alteração; uso anterior|
Microsoft R Server     |Nenhuma alteração; uso anterior|
**SQL Server 2016 SP 1 CU2**     |
Microsoft R Open     |[SRO_3.2.2.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836819)|
Microsoft R Server    |[SRS_8.0.3.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836818)|
**SQL Server 2016 SP 1 CU3**     |
Microsoft R Open     |Nenhuma alteração; uso anterior|
Microsoft R Server     |Nenhuma alteração; uso anterior|
**GDR e atualização cumulativa 4 do SQL Server 2016 SP 1**     |
Microsoft R Open     |Nenhuma alteração; uso anterior|
Microsoft R Server    |[SRS_8.0.3.17000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=850317)
**SQL Server 2016 SP 1 CU5**     |
Microsoft R Open     |Nenhuma alteração; uso anterior|
Microsoft R Server    |Nenhuma alteração; uso anterior |

Se você deseja exibir o código-fonte para o Microsoft R, ele está disponível para download como um arquivo no formato. tar: [instaladores baixar R Server](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows#download)

### <a name = "bkmk_OtherComponents"></a>Pré-requisitos adicionais

Dependendo do seu ambiente, você precisará fazer cópias locais dos instaladores dos pré-requisitos a seguir.

Componente  |Versão
---------|---------
[Provedor Microsoft AS OLE DB para SQL Server 2016](https://go.microsoft.com/fwlink/?linkid=834405)     |  13.0.1601.5
[Microsoft .NET Core](https://go.microsoft.com/fwlink/?linkid=834319)     | 1.0.1
[Microsoft MPI](https://go.microsoft.com/fwlink/?linkid=834316)     | 7.1.12437.25
[Pacote Redistribuível do Microsoft Visual C++ 2013](https://go.microsoft.com/fwlink/?linkid=799853)     | 12.0.30501.0
[Pacote Redistribuível do Microsoft Visual C++ 2015](https://go.microsoft.com/fwlink/?linkid=828641)     | 14.0.23026.0

## <a name="modslocales"></a>Instalando para idiomas diferentes

Se você baixar o. Arquivos CAB como parte da instalação do SQL Server em um computador com acesso à internet, o Assistente de instalação detecta o idioma local e altera automaticamente o idioma do instalador.

No entanto, dependendo de sua versão do SQL Server, você precisará executar etapas adicionais para instalar os componentes de R localizados em um computador sem acesso à internet.

+ **For SQL Server 2016**

   Depois de baixar os instaladores de R para um compartilhamento local, você precisará editar manualmente o nome dos arquivos de download para inserir o identificador de idioma correto para o idioma que você está instalando.

    Por exemplo, para instalar a versão japonesa do SQL Server, você deve alterar o nome do arquivo de SRS_8.0.3.0_**1033**. cab para SRS_8.0.3.0_**1041**. cab.

    > [!IMPORTANT]
    > Esse problema aplica-se somente a versões anteriores e foi corrigido em versões posteriores.
    > **Só use essa solução alternativa se o instalador retornará uma mensagem de que ele não é possível instalar o idioma correto.**

+ **For SQL Server 2017**

    Baixar o. Arquivo CAB para os componentes de R ou Python.
    
    O idioma é detectado com base na localidade do servidor. A localidade correta é instalada automaticamente com o download. Arquivo CAB.

## <a name="slipstream-upgrades"></a>Atualizações de instalação integrada

A instalação integrada refere-se à capacidade de aplicar um patch ou atualizar para uma instalação de instância com falha para corrigir problemas existentes. A vantagem desse método é que o SQL Server é atualizado ao mesmo tempo em que você executa a instalação, evitando uma reinicialização separada posterior.

+ Se o servidor não tiver acesso à Internet, você deverá baixar o instalador do SQL Server e então baixar versões correspondentes dos instaladores de componentes do R **antes** de começar o processo de atualização.  Os componentes do R não são incluídos por padrão com o SQL Server.

+ Se você está adicionando esses componentes a uma instalação existente, use a versão atualizada do instalador do SQL Server e a versão atualizada correspondente dos componentes adicionais. Quando você especificar que o recurso de R está instalado, o instalador procura a versão correspondente dos instaladores para o componentes de aprendizado de máquina.

## <a name="command-line-arguments-for-specifying-component-locations"></a>Argumentos de linha de comando para especificar a localização dos componentes

Ao executar uma instalação offline da linha de comando, você deve fornecer os seguintes argumentos de linha de comando para especificar o local dos componentes que você baixou previamente. No entanto, você não precisa definir os sinalizadores adicionais para instalar os componentes adicionais necessários; pré-requisitos, como o núcleo do .NET estão instalados silenciosamente por padrão.

**Local de instaladores**

- `/UPDATESOURCE` para especificar o local do arquivo local que contém o instalador de atualização do SQL Server
- `/MRCACHEDIRECTORY` para especificar a pasta que contém os arquivos de CAB do componente de R
- `/MPYCACHEDIRECTORY` para especificar a pasta que contém os arquivos de CAB do componente de Python

**Componentes de R no SQL Server 2016**

- `/ADVANCEDANALYTICS` Para obter suporte do mecanismo de scripts externos
- `/IACCEPTROPENLICENSETERMS="True"` para aceitar o contrato de licenciamento do R separado

**Componentes de R no SQL Server 2017**

- `/ADVANCEDANALYTICS` Para obter suporte do mecanismo de scripts externos
- `/SQL_INST_MR` Para usar o R
- `/IACCEPTROPENLICENSETERMS="True"` para aceitar o contrato de licenciamento do R separado

**Componentes de Python no SQL Server 2017**

- `/ADVANCEDANALYTICS` Para obter suporte do mecanismo de scripts externos
- `/SQL_INST_MPY` Para usar o Python
- `/IACCEPTPYTHONLICENSETERMS="True"` para aceitar o Python separado contrato de licenciamento

> [!NOTE]
> Você não pode alterar a conta de serviço para a barra inicial usando parâmetros de instalação do SQL Server. É recomendável que você instale usando as contas de serviço padrão e, em seguida, modificar a conta de serviço usando o SQL Server Configuration Manager. Depois de fazer isso, certifique-se de reiniciar o serviço Launchpad.

## <a name="see-also"></a>Consulte também

[Instalar o Microsoft R Server](https://docs.microsoft.com/r-server/install/r-server-install-windows)

Este artigo pela equipe de suporte de serviços de R demonstra como executar uma instalação autônoma ou a atualização dos serviços do R no SQL Server 2016: [implantando serviços de R em computadores sem acesso à Internet](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/do-it-right-deploying-sql-server-r-services-on-computers-without-internet-access/).
