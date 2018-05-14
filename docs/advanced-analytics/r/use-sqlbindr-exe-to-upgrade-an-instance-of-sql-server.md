---
title: Atualizar os componentes de R e Python em instâncias do SQL Server R (serviços de aprendizado de máquina) | Microsoft Docs
description: Atualização do R e Python no SQL Server 2016 R Services ou serviços de aprendizado de máquina do SQL Server de 2017 usando sqlbindr.exe para ligar ao servidor de aprendizado de máquina.
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/05/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: aa67fbf2480de093ffe2f919e9c50ee2d5082b83
ms.sourcegitcommit: df382099ef1562b5f2d1cd506c1170d1db64de41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/12/2018
---
# <a name="upgrade-machine-learning-r-and-python-components-in-sql-server-instances"></a>Atualizar os componentes da máquina de aprendizado (R e Python) em instâncias do SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Integração do R e Python no SQL Server inclui pacotes de código-fonte aberto e o proprietário da Microsoft. Em manutenção padrão do SQL Server, pacotes R e Python são atualizados de acordo com o ciclo de versão do SQL Server, com correções de bugs para os pacotes existentes na versão atual. 

A maioria dos cientistas de dados estiver acostumados a trabalhar com pacotes mais recentes assim que estiverem disponíveis. Para serviços do aprendizado de máquina 2017 SQL Server (no banco de dados) e SQL Server 2016 R Services (no banco de dados), você pode obter versões mais recentes do R e Python, alterando o *associação* de serviço do SQL Server [Microsoft Servidor de aprendizado de máquina](https://docs.microsoft.com/en-us/machine-learning-server/index) e [política de suporte do ciclo de vida modernos](https://support.microsoft.com/help/30881/modern-lifecycle-policy).

Associação não altera os conceitos básicos da sua instalação: integração de R e Python ainda faz parte de uma instância do mecanismo de banco de dados, licenciamento permanece inalterado (sem custos adicionais associados à associação), e ainda manter políticas de suporte do SQL Server para o banco de dados mecanismo. Mas reassociação alterar como os pacotes de R e Python são atendidos. O restante deste artigo explica o mecanismo de associação e como ele funciona para cada versão do SQL Server.

> [!NOTE]
> Associação se aplica apenas instâncias (no banco de dados). Associação não é relevante para a instalação (autônomo).

**SQL Server 2017**

Para SQL Server 2017 Machine Learning Services consideraria associação somente quando o servidor de aprendizado de máquina do Microsoft começa a oferecem pacotes adicionais ou versões mais recentes sobre o que você já tem.

**SQL Server 2016**

Há dois caminhos para obtenção de novos e atualizados para clientes de serviços do SQL Server 2016 R, pacotes de R. Um envolve a atualização para o SQL Server 2017; o segundo, associação para o servidor de aprendizado de máquina do Microsoft.

Atualizar para o SQL Server 2017 obtém os pacotes de R nas versões incluídas dessa versão, além de recursos de Python. Como alternativa, é de associação é atualizado pacotes de R, o que mais podem ser atualizados em cada nova versão principal e secundário do servidor de aprendizado de máquina do Microsoft. 

Associação não dá suporte a Python, que é um recurso do SQL Server 2017. 

**Atualizações de componentes disponíveis por meio do Microsoft Server de aprendizado de máquina**

A tabela a seguir é um mapa de versão, mostrando a versão instalada com o SQL Server, com as possíveis atualizações quando você associar ao servidor de aprendizado de máquina Microsoft (anteriormente conhecido como R Server antes da adição de suporte de Python a partir do MLS 9.2.1). 

Observe que a associação não garante a versão mais recente do R ou Anaconda. Quando você associa a Microsoft Server de aprendizado de máquina, que obter a versão de R ou Python instalada por meio da instalação, o que pode ou não ser a versão mais recente disponível na web.

[**SQL Server 2016 R Services**](../install/sql-r-services-windows-install.md)

Componente |Versão inicial | R Server 9.0.1 | R Server 9.1 | MLS 9.2.1 | MLS 9.3 |
----------|----------------|----------------|--------------|---------|-------|
Microsoft R Open (MRO) r | R 3.2.2     | R 3.3.2   |R 3.3.3   | R 3.4.1  | R 3.4.3 |
[RevoScaleR](https://docs.microsoft.com/achine-learning-server/r-reference/revoscaler/revoscaler) | 8.0.3  | 9.0.1 |  9.1 |  9.2.1 |  9.3 |
[MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)| n.d. | 9.0.1 |  9.1 |  9.2.1 |  9.3 |
[modelos de pré-treinado](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models)| n.d. | 9.0.1 |  9.1 |  9.2.1 |  9.3 |
[sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils)| n.d. | 1.0 |  1.0 |  1.0 |  1.0 |
[olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) | n.d. | 1.0 |  1.0 |  1.0 |  1.0 |


[**Serviços de aprendizado de máquina do SQL Server de 2017**](../install/sql-machine-learning-services-windows-install.md)

Componente |Versão inicial | MLS 9.3 | | | |
----------|----------------|---------|-|-|-|-|
Microsoft R Open (MRO) r | R 3.3.3 | R 3.4.3 | | | |
[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) |   9.2 |  9.3 | | | |
[MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package) | 9.2  | 9.3| | | |
[sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils)| 1.0 |  1.0 | | | |
[olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) | 1.0 |  1.0 | | | |
Anaconda 4.2 em Python 3.5  | 4.2/3.5.2 | 4.2/3.5.2 | | | |
[revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) | 9.2  | 9.3| | | |
 [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) | 9.2  | 9.3| | | |
[modelos de pré-treinado](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models) | 9.2 | 9.3| | | |

## <a name="how-component-upgrade-works"></a>Como funciona a atualização do componente

Atualização de componente é por meio de *associação* uma instância do SQL Server 2016 R Services (ou uma instância de serviços de aprendizado de máquina do SQL Server 2017) para [Microsoft Server de aprendizado de máquina](https://docs.microsoft.com/machine-learning-server/index). 

Servidor de aprendizado de máquina do Microsoft é um produto de servidor de local separadas do SQL Server, mas com o mesmo interpretadores e pacotes. Associação trocas out o mecanismo de atualização de serviço do SQL Server para que você possa usar os R e Python pacotes de envio com o Microsoft Server de aprendizado de máquina, que geralmente são mais recentes do que aqueles instalados pelo SQL Server. Políticas de suporte de alternância é uma opção atraente para equipes de ciência de dados que exigem a geração mais recente R e módulos Python para suas soluções. 

Associação é executada o [instalador MLS](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install). O instalador de atualizações de pacotes específicos de R e Python, mas não substitui a sua instância do SQL Server no banco de dados com um autônomo, a instalação de servidor desconectada.

+ Sem vinculação, pacotes R e Python são corrigir para correções de bugs quando você instala um SQL Server service pack ou atualização cumulativa (CU). 
+ Com associação, versões mais recentes do pacote podem ser aplicadas à sua instância, independentemente do agendamento de atualizações Cumulativas de versão, no [modernos política de ciclo de vida](https://support.microsoft.com/help/30881/modern-lifecycle-policy) e versões do Microsoft Server de aprendizado de máquina. A política de suporte do ciclo de vida modernos oferece mais frequentes atualizações em um tempo de vida de um ano, mais curto. Pós-associação, você continuará a usar o instalador MLS atualizações futuras de R e Python conforme elas se tornam disponíveis no servidor de aprendizado de máquina do Microsoft.

Associação se aplica somente recursos R e Python. Ou seja, pacotes de código-fonte aberto para os recursos de R e Python (Microsoft R Open, Anaconda) e o proprietários pacotes RevoScaleR, revoscalepy e assim por diante. A associação não altera o modelo de suporte para a instância do mecanismo de banco de dados e não altera a versão do SQL Server.

A associação é reversível. Você pode reverter ao serviço do SQL Server por [desassociar a instância](#bkmk_Unbind) e reparing sua instância do mecanismo de banco de dados do SQL Server.

Etapas para a associação somou, são da seguinte maneira:

+ Iniciar com uma instalação existente e configurada do SQL Server 2016 R Services (ou serviços de aprendizado de máquina do SQL Server 2017).
+ Determine qual versão do servidor de aprendizado de máquina do Microsoft tem os componentes atualizados que você deseja usar.
+ Baixe e execute a instalação dessa versão. A instalação detecta a instância existente, adiciona uma opção de associação e retorna uma lista de instâncias compatíveis.
+ Escolha a instância que você deseja vincular e, em seguida, concluir a instalação para executar a associação.

Em termos de experiência do usuário, a tecnologia e como trabalhar com ele permanece inalterado. A única diferença é a presença de pacotes versão mais recente e possivelmente adicionais originalmente não está disponível por meio do SQL Server (como MicrosoftML para clientes do SQL Server 2016 R Services).

## <a name="bkmk_BindWizard"></a>Associar a MLS usando a instalação

Instalação de aprendizado de máquina do Microsoft detecta os recursos existentes e a versão do SQL Server e invoca um utilitário chamado SqlBindR.exe para alterar a associação. Internamente, SqlBindR é encadeada para a instalação e usada indiretamente. Posteriormente, você pode chamar SqlBindR diretamente da linha de comando para exercer opções específicas.

1. No SSMS, execute `SELECT @@version` para verificar se o servidor atende aos requisitos mínimos de compilação. 

   Para serviços do SQL Server 2016 R, é o mínimo [Service Pack 1](https://www.microsoft.com/download/details.aspx?id=54276) e [CU3](https://support.microsoft.com/help/4019916/cumulative-update-3-for-sql-server-2016-sp1).

1. Verifique a versão de base de R e pacotes de RevoScaleR para confirmar as versões existentes são menores do que você planeja substituí-los por. Para serviços do SQL Server 2016 R, é de pacote básico de R 3.2.2 e RevoScaleR é 8.0.3.

    ```SQL
    EXECUTE sp_execute_external_script
    @language=N'R'
    ,@script = N'str(OutputDataSet);
    packagematrix <- installed.packages();
    Name <- packagematrix[,1];
    Version <- packagematrix[,3];
    OutputDataSet <- data.frame(Name, Version);'
    , @input_data_1 = N''
    WITH RESULT SETS ((PackageName nvarchar(250), PackageVersion nvarchar(max) ))
    ```

1. Baixe o Microsoft Server de aprendizado de máquina no computador que tem a instância que você deseja atualizar. É recomendável a [versão mais recente](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install#download-machine-learning-server-installer).

1. Descompacte a pasta e iniciar ServerSetup.exe, localizado em MLSWIN93.

   ![Assistente de instalação do servidor de aprendizado de máquina do Microsoft](media/mls-921-installer-start.PNG)

1. Em **configura a instalação**, confirme os componentes para atualizar e revisar a lista de instâncias compatíveis. 

   À esquerda, escolha todos os recursos que você deseja manter ou atualizar. Não é possível atualizar alguns recursos e outros não. Uma caixa de seleção vazia remove esse recurso, supondo que ele está instalado. Captura de tela, fornecida como uma instância do SQL Server 2016 R Services (MSSQL13), R e a versão de R dos modelos previamente treinados são selecionadas. Essa configuração é válida porque o SQL Server 2016 dá suporte a R, mas não Python.

   À direita, selecione a caixa de seleção ao lado do nome de instância. Se nenhuma instância estiver listada, você tem uma combinação incompatível. Se você não selecionar uma instância, uma nova instalação autônoma do servidor de aprendizado de máquina é criada e bibliotecas do SQL Server não foram modificadas. Se você não pode selecionar uma instância, não pode ser em [SP1 CU3](https://support.microsoft.com/help/4019916/cumulative-update-3-for-sql-server-2016-sp1). 

    ![Assistente de instalação do servidor de aprendizado de máquina do Microsoft](media/mls-931-installer-mssql13.png)

1. Sobre o **contrato de licença** página, selecione **aceito esses termos** para aceitar os termos de licenciamento para o servidor de aprendizado de máquina. 

1. Nas páginas sucessivas, forneça seu consentimento para condições de licenciamento adicionais para os componentes de código-fonte selecionado, como Microsoft R Open ou a distribuição Anaconda Python.

1. Sobre o **quase lá** página, anote a pasta de instalação. A pasta padrão é \Program Files\Microsoft\ML Server.

    Se você quiser alterar a pasta de instalação, clique em **avançado** para retornar para a primeira página do assistente. No entanto, você deve repetir todas as seleções anteriores.

Durante o processo de instalação, quaisquer bibliotecas de R ou Python usadas pelo SQL Server são substituídas e barra inicial é atualizado para usar os componentes mais recentes. Como resultado, se a instância usada anteriormente bibliotecas na pasta padrão R_SERVICES, após a atualização dessas bibliotecas são removidas e as propriedades para o serviço Launchpad são alteradas para usar as bibliotecas no novo local.

Associação afeta o conteúdo dessas pastas: C:\Program Files\Microsoft SQL mssql13. MSSQLSERVER\R_SERVICES\library é substituído pelo conteúdo de C:\Program Files\Microsoft\ML Server\R_SERVER. A segunda pasta e seu conteúdo é criado pela instalação do servidor do Microsoft Machine Learning. 

Verifique se a atualização falhar, [códigos de erro SqlBindR](#sqlbindr-error-codes) para obter mais informações.

## <a name="confirm-binding"></a>Confirme a associação

Verificar a versão do R e o RevoScaleR para confirmar que você tem as versões mais recentes. Use o console de R distribuído com os pacotes de R em sua instância do mecanismo de banco de dados para obter informações de pacote:

```SQL
EXECUTE sp_execute_external_script
@language=N'R'
,@script = N'str(OutputDataSet);
packagematrix <- installed.packages();
Name <- packagematrix[,1];
Version <- packagematrix[,3];
OutputDataSet <- data.frame(Name, Version);'
, @input_data_1 = N''
WITH RESULT SETS ((PackageName nvarchar(250), PackageVersion nvarchar(max) ))
```

Para SQL Server 2016 R Services associado ao 9.3 de servidor de aprendizado de máquina, pacote R Base deve ser 3.4.1 RevoScaleR deve ser 9.3 e você também deve ter MicrosoftML 9.3. 

Se você adicionou os modelos previamente treinados, os modelos são inseridos na biblioteca do MicrosoftML e você pode chamá-los por meio das funções MicrosoftML. Para obter mais informações, consulte [exemplos de R para MicrosoftML](https://docs.microsoft.com/machine-learning-server/r/sample-microsoftml).

## <a name="offline-binding-no-internet-access"></a>Associação offline (sem acesso à internet)

Para sistemas com nenhuma conectividade com a internet, você pode baixar os arquivos. cab e de instalador para um computador conectado à internet e, em seguida, transferir arquivos para o servidor isolado. 

O instalador (ServerSetup.exe) inclui os pacotes do Microsoft (RevoScaleR, MicrosoftML, olapR, sqlRUtils). Os arquivos. cab fornecem outros componentes principais. Por exemplo, o cab "SRO" fornece R Open, distribuição da Microsoft de software livre R.

As instruções a seguir explicam como colocar os arquivos para uma instalação offline.

1. Baixe o instalador MLS. Ele baixa como um único arquivo compactado. É recomendável a [versão mais recente](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install#download-machine-learning-server-installer), mas você também pode instalar [versões anteriores](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows-offline#download-required-components).

1. Baixe arquivos. cab. Os links a seguir são para a versão 9.3. Se você precisar de versões anteriores, os links adicionais podem ser encontradas em [R Server 9.1](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows-offline#download-required-components). Lembre-se de que o Python/Anaconda só podem ser adicionado a uma instância de serviços de aprendizado de máquina do SQL Server de 2017. Existem modelos previamente treinados para R e Python; o CAB fornece modelos nos idiomas que você está usando.

    | Recurso | Download |
    |---------|----------|
    | R       | [SRO_3.4.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=867186&clcid=1033) |
    | Python  | [SPO_9.3.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=859054) | 
    | Modelos previamente treinados | [MLM_9.3.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=859053) |

1. Transferência de arquivos. zip e. cab para o servidor de destino.

1. No servidor, digite `%temp%` no comando executar para obter o local físico do diretório temporário. O caminho físico varia por máquina, mas é normalmente `C:\Users\<your-user-name>\AppData\Local\Temp`.

1. Coloque os arquivos. cab na pasta % temp %.

1. Descompacte o instalador.

1. Execute ServerSetup.exe e siga as instruções na tela para concluir a instalação.

## <a name="bkmk_BindCmd"></a>Operações de linha de comando

Depois de executar o Microsoft Server de aprendizado de máquina, um utilitário de linha de comando chamado SqlBindR.exe se torna disponível que você pode usar para obter mais operações de associação. Por exemplo, se você decidir reverter uma associação, você pode executar novamente a instalação ou use o utilitário de linha de comando. Além disso, você pode usar essa ferramenta para verificar para a instância de compatibilidade e disponibilidade.

> [!TIP]
> Não é possível localizar SqlBindR? Você provavelmente não executou a instalação. SqlBindR está disponível somente depois de executar a instalação do Server aprendizado de máquina.

1. Abra um prompt de comando como administrador e navegue até a pasta que contém sqlbindr.exe. O local padrão é C:\Program Files\Microsoft\MLServer\Setup

2. Digite o seguinte comando para exibir uma lista das instâncias disponíveis: `SqlBindR.exe /list`
  
   Tome nota do nome completo da instância conforme listado. Por exemplo, o nome da instância pode ser MSSQL14. MSSQLSERVER para uma instância padrão ou algo parecido com o nome do servidor. MYNAMEDINSTANCE.

3. Execute o **SqlBindR.exe** com o */associar* argumento e especifique o nome da instância para atualizar, usando o nome de instância que foi retornado na etapa anterior.

   Por exemplo, para atualizar a instância padrão, digite:  `SqlBindR.exe /bind MSSQL14.MSSQLSERVER`

4. Quando a atualização for concluída, reinicie o serviço de barra inicial associado a qualquer instância que foi modificada.

## <a name="bkmk_Unbind"></a>Reverter ou desvincular uma instância

Você pode restaurar uma instância associada a uma instalação inicial dos componentes do R e Python, estabelecidos pela instalação do SQL Server. Há três partes para reverter para a manutenção do SQL Server.

+ [Etapa 1: Desvincular de servidor de aprendizado de máquina da Microsoft](#step-1-unbind)
+ [Etapa 2: Restaurar a instância para o status original](#step-2-restore)
+ [Etapa 3: Reinstalar todos os pacotes adicionados à instalação do](#step-3-reinstall-packages)

<a name="step-1-unbind"></a> 

### <a name="step-1-unbind"></a>Etapa 1: desvincular

Você tem duas opções para reverter a associação: execute novamente a instalação novamente ou use o utilitário de linha de comando SqlBindR.

#### <a name="bkmk_wizunbind"></a> Desassocie usando a instalação

1. Localize o instalador para o servidor de aprendizado de máquina. Se você tiver removido o instalador, talvez seja necessário baixá-lo novamente, ou copie-o de outro computador.
2. Certifique-se de executar o instalador no computador que tem a instância que você deseja desassociar.
2. O instalador identifica as instâncias locais que são candidatos para a desassociação.
3. Desmarque a caixa de seleção ao lado de instância que você deseja reverter para a configuração original.
4. Aceite o contrato de licença. Você deve indicar a aceitação dos termos de licenciamento mesmo durante a instalação.
5. Clique em **Concluir**. O processo leva algum tempo.

#### <a name="bkmk_cmdunbind"></a> Desassocie usando a linha de comando

1. Abra um prompt de comando e navegue até a pasta que contém **sqlbindr.exe**, conforme descrito na seção anterior.

2. Execute o comando **SqlBindR.exe** com o argumento */unbind* e especifique a instância.

   Por exemplo, o comando a seguir reverte a instância padrão:
   
    `SqlBindR.exe /unbind MSSQL14.MSSQLSERVER`

<a name="step-2-restore"></a> 

###  <a name="step-2-repair-the-sql-server-instance"></a>Etapa 2: Repare a instância do SQL Server

Execute a instalação do SQL Server para reparar a instância do mecanismo de banco de dados com os recursos de R e Python. Atualizações existentes são preservadas, mas se você perdeu todas as atualizações para pacotes de R e Python de manutenção do SQL Server, essa etapa se aplica os patches.

Como alternativa, isso é mais trabalho, mas também totalmente desinstalar e reinstalar a instância do mecanismo de banco de dados e, em seguida, aplicar todas as atualizações de serviço.

<a name="step-3-reinstall-packages"></a> 

### <a name="step-3-add-any-third-party-packages"></a>Etapa 3: Adicionar todos os pacotes de terceiros

Você pode adicionar outros pacotes de código-fonte aberto ou de terceiros à sua biblioteca de pacote. Como reverter a associação alterna o local da biblioteca de pacote padrão, você deve reinstalar os pacotes para a biblioteca de R e Python agora está usando. Para obter mais informações, consulte [padrão pacotes](installing-and-managing-r-packages.md), [instalar novos pacotes de R](install-additional-r-packages-on-sql-server.md), e [instalar novos pacotes do Python](../python/install-additional-python-packages-on-sql-server.md).

## <a name="known-issues"></a>Problemas conhecidos

Esta seção lista os problemas conhecidos específicos para usar o utilitário SqlBindR.exe ou atualizações do servidor de aprendizado de máquina que podem afetar a instâncias do SQL Server.

### <a name="restoring-packages-that-were-previously-installed"></a>Restaurando os pacotes que foram instalados anteriormente

Se você atualizar para o Microsoft R Server 9.0.1, a versão do SqlBindR.exe para que a versão falhou ao restaurar os pacotes originais ou componentes de R completamente, exigindo que o usuário executar o reparo do SQL Server na instância, se aplicam a todas as versões de serviço e reinicie a instância.

Versão mais recente do SqlBindR restaurar os recursos de R originais, eliminando a necessidade de reinstalação dos componentes de R ou patch novamente o servidor automaticamente. No entanto, você deve instalar as atualizações de pacote de R que talvez tenham sido adicionadas após a instalação inicial.

Se você tiver usado as funções de gerenciamento de pacote para instalar e compartilhar o pacote, essa tarefa é muito mais fácil: você pode usar comandos de R para sincronizar os pacotes instalados no sistema de arquivos usando registros no banco de dados e vice-versa. Para obter mais informações, consulte [gerenciamento de pacotes de R para o SQL Server](r-package-management-for-sql-server-r-services.md).

### <a name="problems-with-multiple-upgrades-from-sql-server"></a>Problemas com várias atualizações do SQL Server

Se anteriormente você tiver atualizado uma instância do SQL Server 2016 R Services para 9.0.1, quando você executar o instalador de novo para o Microsoft R Server 9.1.0, exibe uma lista de todas as instâncias válidas e, em seguida, por padrão, seleciona instâncias associadas anteriormente. Se você continuar, as instâncias associadas anteriormente serão desvinculadas. Como resultado, o 9.0.1 anteriores instalação é removida, incluindo as relacionadas a pacotes, mas a nova versão do Microsoft R Server (9.1.0) não está instalada.

Como alternativa, você pode modificar a instalação existente do servidor de R da seguinte maneira:
1. No painel de controle, abra **adicionar ou remover programas**.
2. Localize o Microsoft R Server e, em seguida, clique em **alteração/modificação**.
3. Quando o instalador é iniciado, selecione as instâncias que você deseja associar a 9.1.0.

Microsoft Server de aprendizado de máquina 9.2.1 e 9.3 não têm esse problema.

### <a name="binding-or-unbinding-leaves-multiple-temporary-folders"></a>Associação ou desvincular deixa várias pastas temporárias

Às vezes, a associação e operações de desvinculação falharem Limpar pastas temporárias.
Se você encontrar pastas com um nome assim, você poderá removê-lo após a conclusão da instalação: R_SERVICES_<guid>

> [!NOTE]
> Certifique-se de aguardar até que a instalação for concluída. Ele pode levar muito tempo para remover bibliotecas de R associados com uma versão e, em seguida, adicionar novas bibliotecas de R. Quando a operação for concluída, as pastas temporárias são removidas.

## <a name="sqlbindrexe-command-syntax"></a>Sintaxe do comando SqlBindR.exe

### <a name="usage"></a>Uso

`sqlbindr [/list] [/bind <SQL_instance_ID>] [/unbind <SQL_instance_ID>]`

### <a name="parameters"></a>Parâmetros

|Nome|Description|
|------|------|
|*list*| Exibe uma lista de todas as IDs de instância do Banco de Dados SQL no computador atual|
|*bind*| Atualiza a instância do Banco de Dados SQL especificada para a última versão do R Server e garante que a instância obtém automaticamente as atualizações futuras do R Server|
|*unbind*|Desinstala a última versão do R Server da instância do Banco de Dados SQL especificada e impede que atualizações futuras do R Server afetem a instância|

<a name="sqlbinder-error-codes"><a/>

## <a name="binding-errors"></a>Erros de associação

Instalador de MLS e SqlBindR retornam os seguintes códigos de erro e mensagens.

|Código do erro  | Mensagem           | Detalhes               |
|------------|-------------------|-----------------------|
|Associar o erro 0 | Okey (êxito) | Associação passado sem erros. |
|Associar o erro 1 | Argumentos inválidos | Erro de sintaxe. |
|Associar o erro 2 | Ação inválida | Erro de sintaxe. |
|Associar o erro 3 | Instância inválida | Uma instância existe, mas não é válida para associação. |
|Associar o erro 4 | Não associável | |
|Associar o erro 5 | Já vinculado | Você executou o comando *bind* , mas a instância especificada já está associada. |
|Associar o erro 6 | Falha na ligação | Ocorreu um erro ao desconectar a instância. Esse erro pode ocorrer se você executar o instalador MLS sem selecionar todos os recursos. Associação requer que você selecionar uma instância MSSQL e R e Python, supondo que a instância do SQL Server 2017.|
|Associar o erro 7 | Não associado | A instância do mecanismo de banco de dados tem R Services ou serviços de aprendizado de máquina do SQL Server. A instância não está associada ao servidor de aprendizado de máquina do Microsoft. |
|Associar o erro 8 | Desassocie falha | Ocorreu um erro ao desconectar a instância. |
|Associar o erro 9 | Nenhuma instância encontrada | Nenhuma instância do mecanismo de banco de dados foi encontrada neste computador. |


## <a name="see-also"></a>Consulte também

+ [Instalar Machine Learning Server para Windows (conectados à Internet)](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)
+ [Instalar Machine Learning Server para Windows (offline)](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-offline)
+ [Problemas conhecidos no servidor de aprendizado de máquina](https://docs.microsoft.com/machine-learning-server/resources-known-issues)
+ [Anúncios de recurso da versão anterior do servidor de R](https://docs.microsoft.com/r-server/whats-new-in-r-server)
+ [Recursos preteridos, descontinuados ou alterados](https://docs.microsoft.com/machine-learning-server/resources-deprecated-features)