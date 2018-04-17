---
title: Instalar componentes de aprendizado de máquina do SQL Server sem acesso à internet | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 3ba344147b5d57a1c0168fbb5be93ae24b02b179
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="install-sql-server-machine-learning-components-without-internet-access"></a>Instalar componentes sem acesso à internet de aprendizado de máquina do SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Por padrão, instaladores de se conectar a sites de download da Microsoft para obter necessária e componentes atualizados para aprendizado no SQL Server do computador. Se as restrições de firewall impedir que o instalador alcançar esses sites, você pode usar um dispositivo conectado à internet para baixar os arquivos, transferir arquivos para um servidor offline e, em seguida, execute a instalação.

## <a name="get-the-installation-media"></a>Obtenha a mídia de instalação

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

> [!NOTE]  
> Para instalações locais, você deve executar a Instalação como um administrador. Se você instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de um compartilhamento remoto, deverá usar uma conta de domínio que tenha permissões de leitura e de execução no compartilhamento remoto.  
 
 ###  <a name="bkmk_ga_instalpatch"></a> Instalar o requisito de patch 

A Microsoft identificou um problema com a versão específica dos binários do Tempo de Execução Microsoft VC++ 2013 que são instalados como um pré-requisito pelo SQL Server. Se essa atualização para os binários do Tempo de Execução de VC não for instalada, o SQL Server poderá apresentar problemas de estabilidade em determinados cenários. Antes de instalar o SQL Server, siga as instruções em [Notas de Versão do SQL Server](../../sql-server/sql-server-2016-release-notes.md#bkmk_ga_instalpatch) para ver se seu computador precisa de um patch para os binários de tempo de execução do VC.  


## <a name="download-cab-files"></a>Baixar arquivos. cab

Em um servidor conectado à internet, baixe os arquivos. cab necessários para uma instalação offline. O programa de instalação usa os arquivos. cab para instalar recursos complementares.

Versão  |Link de download  |
---------|---------|
**Versão inicial do SQL Server 2017** |
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
**Atualização Cumulativa do SQL Server 2016 4**     |
Microsoft R Open     |[SRO_3.2.2.13000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=831785)|
Microsoft R Server     |[SRS_8.0.3.13000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=831676)|
**SQL Server 2016 CU 5**     |
Microsoft R Open     |Nenhuma alteração; uso anterior|
Microsoft R Server     |Nenhuma alteração; uso anterior|
**Atualização Cumulativa do SQL Server 2016 6**     |
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

## <a name="transfer-files"></a>Transferência de arquivos

Transferência de mídia de instalação do SQL Server compactada e os arquivos que você já baixou para o computador no qual você está instalando a instalação.

Colocar arquivos CAB em uma pasta conveniente como **Downloads** ou pasta temp do usuário de instalação: C:\Users < nome de usuário > \AppData\Local\Temp.

Coloque o arquivo de en_sql_server_2017.iso em uma pasta conveniente. Clique duas vezes em **setup.exe** para iniciar a instalação.

### <a name="run-setup"></a>Executar a instalação

Quando você executa a instalação do SQL Server em um computador desconectado da internet, a instalação adiciona um **instalação Offline** página ao Assistente de forma que você pode especificar o local dos arquivos. cab que você copiou na etapa anterior.

1. Inicie o Assistente de instalação do SQL Server.

2. Quando o Assistente de instalação exibe a página de licenciamento de software livre R ou componentes de Python, clique em **aceitar**. Aceitação dos termos de licença permite que você vá para a próxima etapa.

3. No **instalação Offline** página **caminho instalar**, especifique a pasta que contém os arquivos. cab que você copiou anteriormente.

4. Continuar a seguir as instruções na tela para concluir a instalação.

Após a instalação for concluída, reinicie o serviço e, em seguida, configure o servidor para habilitar a execução do script conforme descrito em [instalar o SQL Server 2017 Machine Learning Services (no banco de dados)](sql-machine-learning-services-windows-install.md) ou [instalar o SQL Server Serviços de R de 2016 (no banco de dados)](sql-r-services-windows-install.md).

## <a name="slipstream-upgrades-for-offline-servers"></a>Atualizações de instalação integrada para servidores offline

A instalação integrada refere-se à capacidade de aplicar um patch ou atualizar para uma instalação de instância com falha para corrigir problemas existentes. A vantagem desse método é que o SQL Server é atualizado ao mesmo tempo em que você executa a instalação, evitando uma reinicialização separada posterior.

+ Se o servidor não tiver acesso à Internet, você deverá baixar o instalador do SQL Server e então baixar versões correspondentes dos instaladores de componentes do R **antes** de começar o processo de atualização.  Os componentes do R não são incluídos por padrão com o SQL Server.

+ Se você está adicionando esses componentes a uma instalação existente, use a versão atualizada do instalador do SQL Server e a versão atualizada correspondente dos componentes adicionais. Quando você especificar que o recurso de R está instalado, o instalador procura a versão correspondente dos instaladores para o componentes de aprendizado de máquina.

## <a name="get-help"></a>Obter ajuda

Precisa de ajuda com a instalação ou atualização? Para obter respostas a perguntas comuns e problemas conhecidos, consulte o seguinte artigo:

* [Atualização e instalação perguntas Frequentes – serviços de aprendizado de máquina](../r/upgrade-and-installation-faq-sql-server-r-services.md)

Para verificar o status da instalação da instância e corrigir problemas comuns, tente esses relatórios personalizados.

* [Relatórios personalizados do SQL Server R Services](../r/monitor-r-services-using-custom-reports-in-management-studio.md)

Este artigo pela equipe de suporte de serviços de R demonstra como executar uma instalação autônoma ou a atualização dos serviços do R no SQL Server 2016: [implantando serviços de R em computadores sem acesso à Internet](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/do-it-right-deploying-sql-server-r-services-on-computers-without-internet-access/).


## <a name="next-steps"></a>Próximas etapas

Os desenvolvedores de R podem começar com alguns exemplos simples e conheça os fundamentos de como funciona o R com o SQL Server. Para a próxima etapa, consulte os links a seguir:

+ [Tutorial: Executar R no T-SQL](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [Tutorial: Análise de no banco de dados para os desenvolvedores de R](../tutorials/sqldev-in-database-r-for-sql-developers.md)

Os desenvolvedores de Python podem Saiba como usar o Python com o SQL Server por esses tutoriais a seguir:

+ [Tutorial: Executar Python em T-SQL](../tutorials/run-python-using-t-sql.md)
+ [Tutorial: Análise de no banco de dados para desenvolvedores Python](../tutorials/sqldev-in-database-python-for-sql-developers.md)

Para exibir exemplos de aprendizado de máquina com base em cenários do mundo real, consulte [tutoriais de aprendizado de máquina](../tutorials/machine-learning-services-tutorials.md).

