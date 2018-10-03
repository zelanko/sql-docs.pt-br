---
title: Atualizar os componentes de R e Python em instâncias do SQL Server (serviços de Machine Learning) | Microsoft Docs
description: Atualização do R e Python no SQL Server 2016 Services ou serviços SQL Server 2017 Machine Learning usando sqlbindr.exe para ligar ao servidor do Machine Learning.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/30/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: c2677885719c0b9a54a39b1609a0c2652728820f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48078886"
---
# <a name="upgrade-machine-learning-r-and-python-components-in-sql-server-instances"></a>Atualizar os componentes do machine learning (R e Python) em instâncias do SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Integração de R e Python no SQL Server inclui pacotes de código-fonte aberto e de propriedade da Microsoft. Na manutenção do SQL Server standard, pacotes são atualizados de acordo com o ciclo de lançamento do SQL Server com correções de bugs para os pacotes existentes na versão atual, mas não há atualizações de versão principal. 

No entanto, muitos cientistas de dados estão acostumados a trabalhar com pacotes mais recentes assim que estiverem disponíveis. Para serviços SQL Server 2017 Machine Learning (no banco de dados) e SQL Server 2016 R Services (no banco de dados), você pode obter [versões mais recentes do R e Python](#version-map) pela *associação* para **Microsoft Servidor do Machine Learning**. 

## <a name="what-is-binding"></a>O que está se associando?

Associação é um processo de instalação que alterna o conteúdo das pastas R_SERVICES e PYTHON_SERVICES com mais recente executáveis, bibliotecas e nas ferramentas do [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/index).

Juntamente com os componentes atualizados vem de um comutador em modelos de manutenção. Em vez do [ciclo de vida de produto do SQL Server](https://support.microsoft.com/lifecycle/search?alpha=SQL%20Server%202017), com [atualizações cumulativas do SQL Server](https://support.microsoft.com/help/4047329/sql-server-2017-build-versions), as atualizações de serviço agora está de acordo com o [dão suporte a linha do tempo para o Microsoft R Server & máquina Servidor de aprendizado](https://docs.microsoft.com/machine-learning-server/resources-servicing-support) sobre o [ciclo de vida moderno](https://support.microsoft.com/help/30881/modern-lifecycle-policy).

Exceto para as versões do componente e as atualizações de serviço, associação não altera os conceitos básicos da sua instalação: integração do R e Python ainda é parte de uma instância do mecanismo de banco de dados, de licenciamento permanece inalterado (não há custos adicionais associados à associação) e o SQL As políticas de suporte do servidor ainda são válidas para o mecanismo de banco de dados. O restante deste artigo explica o mecanismo de ligação e como ele funciona para cada versão do SQL Server.

> [!NOTE]
> Associação se aplica a instâncias (no banco de dados) apenas que estão associadas às instâncias do SQL Server. Associação não é relevante para uma instalação (autônomo).

**Considerações de associação do SQL Server 2017**

Para serviços do SQL Server 2017 Machine Learning, você consideraria associação somente quando o Microsoft Machine Learning Server comece a oferecer pacotes adicionais ou versões mais recentes sobre o que você já tem.

**Considerações de associação do SQL Server 2016**

Para clientes do SQL Server 2016 R Services, associação fornece pacotes de R atualizados, novos pacotes não faz parte da instalação original ([MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)), e [modelos pré-treinados](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models), que pode ser ainda mais atualizado em cada nova versão principal e secundária do [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/index). Associação não dá suporte a Python, que é um recurso do SQL Server 2017. 

<a name="version-map"></a>

## <a name="version-map"></a>Mapa de versão

A tabela a seguir é um mapa de versão, mostrando as versões do pacote em veículos de lançamento para que você pode verificar os possíveis caminhos de atualização quando você associa a Microsoft Machine Learning Server (anteriormente conhecido como Microsoft R Server, antes da adição do suporte do Python iniciar no MLS 9.2.1). 

Observe que a associação não garante a versão mais recente do R ou o Anaconda. Quando você associa ao Microsoft Machine Learning Server (MLS), você pode obter a versão do R ou Python instalada por meio da instalação, que pode não ser a versão mais recente disponível na web.

[**SQL Server 2016 R Services**](../install/sql-r-services-windows-install.md)

Componente |Versão inicial | [R Server 9.0.1](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows) | [R Server 9.1](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows) | [MLS 9.2.1](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install) | [MLS 9.3](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install) |
----------|----------------|----------------|--------------|---------|-------|
Microsoft R Open (MRO) r | R 3.2.2     | R 3.3.2   |3.3.3 DO R   | R 3.4.1  | R 3.4.3 |
[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) | 8.0.3  | 9.0.1 |  9.1 |  9.2.1 |  9.3 |
[MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)| Antilhas Holandesas | 9.0.1 |  9.1 |  9.2.1 |  9.3 |
[modelos pré-treinados](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models)| Antilhas Holandesas | 9.0.1 |  9.1 |  9.2.1 |  9.3 |
[sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils)| Antilhas Holandesas | 1.0 |  1.0 |  1.0 |  1.0 |
[olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) | Antilhas Holandesas | 1.0 |  1.0 |  1.0 |  1.0 |


[**Serviços de aprendizado de máquina do SQL Server 2017**](../install/sql-machine-learning-services-windows-install.md)

Componente |Versão inicial | MLS 9.3 | | | |
----------|----------------|---------|-|-|-|-|
Microsoft R Open (MRO) r | 3.3.3 DO R | R 3.4.3 | | | |
[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) |   9.2 |  9.3 | | | |
[MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package) | 9.2  | 9.3| | | |
[sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils)| 1.0 |  1.0 | | | |
[olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) | 1.0 |  1.0 | | | |
Anaconda 4.2 em Python 3.5  | 4.2/3.5.2 | 4.2/3.5.2 | | | |
[revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) | 9.2  | 9.3| | | |
 [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) | 9.2  | 9.3| | | |
[modelos pré-treinados](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models) | 9.2 | 9.3| | | |

## <a name="how-component-upgrade-works"></a>Como funciona a atualização do componente 

Arquivos executáveis e bibliotecas de R e Python são atualizados quando você associa uma instalação existente do R e Python de Machine Learning Server. Executado pela associação a [instalador do Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install) ao executar a instalação em uma SQL Server banco de dados engine instância existente, 2016 ou 2017, tendo a integração de R ou Python. A instalação detecta os recursos existentes e solicita que você associar novamente para o Machine Learning Server. 

Durante a associação, o conteúdo de C:\Program Files\Microsoft SQL Server\MSSQL14. MSSQLSERVER\R_SERVICES e \PYTHON_SERVICES será substituído com os executáveis e bibliotecas de C:\Program programas\microsoft\ml Server\R_SERVER e \PYTHON_SERVER a mais recente.

Ao mesmo tempo, o modelo de manutenção também é invertido mecanismos de atualização do SQL Server para o ciclo de lançamento principais e secundárias mais frequente do Microsoft Machine Learning Server. Alternar as políticas de suporte é uma opção atraente para as equipes de ciência de dados que precisam de geração mais recente de R e módulos de Python para suas soluções. 

+ Sem vinculação, pacotes R e Python são corrigidos para correções de bugs quando você instala um SQL Server service pack ou atualização cumulativa (CU). 
+ Com associação, as versões mais recentes do pacote podem ser aplicadas à sua instância, independentemente do agendamento de versão de CU, sob o [política de ciclo de vida moderno](https://support.microsoft.com/help/30881/modern-lifecycle-policy) e versões do Microsoft Machine Learning Server. A política de suporte do ciclo de vida moderno oferece atualizações mais frequentes em um tempo de vida de um ano, mais curto. Pós-associação, você continuará a usar o instalador MLS para atualizações futuras do R e Python assim que estiverem disponíveis nos sites de download da Microsoft.

Associação se aplica somente recursos de R e Python. Ou seja, pacotes de código-fonte aberto para recursos de R e Python (Microsoft R Open, Anaconda) e os pacotes de proprietários RevoScaleR, revoscalepy e assim por diante. Associação não altera o modelo de suporte para a instância do mecanismo de banco de dados e não altera a versão do SQL Server.

A associação é reversível. Você pode reverter ao serviço do SQL Server pelo [desassociar a instância](#bkmk_Unbind) e reparing sua instância do mecanismo de banco de dados do SQL Server.

Etapas para associação somou, são da seguinte maneira:

+ Comece com uma instalação existente e configurada do SQL Server 2016 R Services (ou serviços de aprendizado de máquina do SQL Server 2017).
+ Determine qual versão do Microsoft Machine Learning Server tem os componentes atualizados que você deseja usar.
+ Baixe e execute a instalação dessa versão. A instalação detecta a instância existente, adiciona uma opção de associação e retorna uma lista de instâncias compatíveis.
+ Escolha a instância que você deseja vincular e, em seguida, concluir a instalação para executar a associação.

Em termos de experiência do usuário, a tecnologia e como você trabalha com ele permanece inalterado. A única diferença é a presença de pacotes mais recentes com controle de versão e possivelmente outros pacotes originalmente não está disponíveis por meio do SQL Server (por exemplo, o MicrosoftML para clientes do SQL Server 2016 R Services).

## <a name="bkmk_BindWizard"></a>Associar a MLS usando a instalação

Instalação do Microsoft Machine Learning detecta os recursos existentes e a versão do SQL Server e invoca um utilitário chamado SqlBindR.exe para alterar a associação. Internamente, SqlBindR é encadeado a instalação e usada indiretamente. Posteriormente, você pode chamar SqlBindR diretamente da linha de comando para exercitar as opções específicas.

1. No SSMS, execute `SELECT @@version` para verificar se o servidor atende aos requisitos mínimos de compilação. 

   Para SQL Server 2016 R Services, é o mínimo [Service Pack 1](https://www.microsoft.com/download/details.aspx?id=54276) e [CU3](https://support.microsoft.com/help/4019916/cumulative-update-3-for-sql-server-2016-sp1).

1. Verifique a versão de base de R e pacotes RevoScaleR para confirmar que as versões existentes são menores do que você planeja substituí-los por. Para SQL Server 2016 R Services, é de pacote básico de R 3.2.2 e RevoScaleR é 8.0.3.

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

1. Feche o SSMS e qualquer outra ferramenta de ter uma conexão aberta para o SQL Server. Associação substitui os arquivos de programa. Se o SQL Server tem sessões abertas, a associação falhará com o código de erro de ligação 6.

1. Baixe o Microsoft Machine Learning Server no computador que tem a instância que você deseja atualizar. É recomendável o [versão mais recente](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install#download-machine-learning-server-installer).

1. Descompacte a pasta e inicie ServerSetup.exe, localizado em MLSWIN93.

   ![Assistente de instalação do Microsoft Machine Learning Server](media/mls-921-installer-start.PNG)

1. Na **configurar a instalação**, confirme a atualização de componentes e examine a lista de instâncias compatíveis. 

   Esta etapa é muito importante.

   À esquerda, escolha todos os recursos que você deseja manter ou atualizar. Não é possível atualizar alguns recursos e outros não. Uma caixa de seleção vazia remove esse recurso, supondo que ela está instalada. Na captura de tela, dada uma instância do SQL Server 2016 R Services (MSSQL13), R e a versão dos modelos previamente treinados do R são selecionados. Essa configuração é válida porque o SQL Server 2016 dá suporte a R, mas não o Python.

   Se você estiver atualizando os componentes do SQL Server 2016 R Services, não selecione o recurso de Python. É possível adicionar o Python para SQL Server 2016 R Services.

   À direita, marque a caixa de seleção ao lado do nome da instância. Se nenhuma instância estiver listada, você tem uma combinação incompatível. Se você não selecionar uma instância, uma nova instalação autônoma do servidor do Machine Learning é criada e bibliotecas do SQL Server são as mesmas. Se você não pode selecionar uma instância, podem não ser em [CU3 SP1](https://support.microsoft.com/help/4019916/cumulative-update-3-for-sql-server-2016-sp1). 

    ![Assistente de instalação do Microsoft Machine Learning Server](media/mls-931-installer-mssql13.png)

1. Sobre o **contrato de licença** página, selecione **aceito os termos** para aceitar os termos de licenciamento para o Machine Learning Server. 

1. Nas páginas sucessivas, fornece consentimento para condições de licenciamento adicionais para os componentes de código-fonte aberto selecionado, como o Microsoft R Open ou a distribuição do Anaconda Python.

1. Sobre o **quase lá** página, anote a pasta de instalação. A pasta padrão é \Program Files\Microsoft\ML Server.

    Se você quiser alterar a pasta de instalação, clique em **avançado** para retornar para a primeira página do assistente. No entanto, você deve repetir todas as seleções anteriores.

Durante o processo de instalação, quaisquer bibliotecas de R ou Python usadas pelo SQL Server são substituídas e a barra inicial é atualizado para usar os componentes mais recentes. Como resultado, se a instância usada anteriormente bibliotecas na pasta R_SERVICES padrão, após a atualização dessas bibliotecas são removidas e as propriedades para o serviço Launchpad são alteradas para usar as bibliotecas no novo local.

Associação afeta o conteúdo dessas pastas: C:\Program Files\Microsoft SQL Server\MSSQL13. MSSQLSERVER\R_SERVICES\library é substituído pelo conteúdo de C:\Program programas\microsoft\ml Server\R_SERVER. A segunda pasta e seu conteúdo é criado pela instalação do Microsoft Machine Learning Server. 

Se a atualização falhar, verifique [códigos de erro SqlBindR](#sqlbindr-error-codes) para obter mais informações.

## <a name="confirm-binding"></a>Confirme se a associação

Verifique novamente a versão do R e o RevoScaleR para confirmar que você tem as versões mais recentes. Use o console de R distribuído com os pacotes de R em sua instância do mecanismo de banco de dados para obter informações do pacote:

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

Para SQL Server 2016 R Services associado ao Machine Learning Server 9.3, pacote de R Base deve ser 3.4.3, RevoScaleR deve ser 9.3 e você também deve ter o MicrosoftML 9.3. 

Se você adicionou os modelos previamente treinados, os modelos são incorporados na biblioteca do MicrosoftML e você pode chamá-los por meio de funções do MicrosoftML. Para obter mais informações, consulte [exemplos de R para o MicrosoftML](https://docs.microsoft.com/machine-learning-server/r/sample-microsoftml).

## <a name="offline-binding-no-internet-access"></a>Associação offline (sem acesso à internet)

Para sistemas com nenhuma conectividade com a internet, você pode baixar os arquivos do instalador e. cab para uma máquina conectada à internet e, em seguida, transferir arquivos para o servidor isolado. 

O instalador (ServerSetup.exe) inclui os pacotes da Microsoft (RevoScaleR, MicrosoftML, olapR, sqlRUtils). Os arquivos. cab fornecem outros componentes básicos. Por exemplo, o cab "SRO" fornece o R Open, distribuição da Microsoft de r de código-fonte aberto.

As instruções a seguir explicam como colocar os arquivos para uma instalação offline.

1. Baixe o instalador MLS. Ele baixa como um único arquivo compactado. É recomendável o [versão mais recente](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install#download-machine-learning-server-installer), mas você também pode instalar [versões anteriores](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows-offline#download-required-components).

1. Baixe arquivos. cab. Os links a seguir são para a versão 9.3. Se você precisar de versões anteriores, os links adicionais podem ser encontradas no [R Server 9.1](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows-offline#download-required-components). Lembre-se de que o Python/Anaconda só podem ser adicionado a uma instância de serviços de aprendizado de máquina do SQL Server 2017. Modelos previamente treinados existem para R e Python; . cab fornece modelos nos idiomas que você está usando.

    | Recurso | Download |
    |---------|----------|
    | R       | [SRO_3.4.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=867186&clcid=1033) |
    | Python  | [SPO_9.3.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=859054) | 
    | Modelos previamente treinados | [MLM_9.3.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=859053) |

1. Transferência de arquivos. zip e. cab para o servidor de destino.

1. No servidor, digite `%temp%` no comando executar para obter o local físico do diretório temporário. O caminho físico varia por máquina, mas geralmente é `C:\Users\<your-user-name>\AppData\Local\Temp`.

1. Coloque os arquivos. cab na pasta % temp %.

1. Descompacte o instalador.

1. Execute ServerSetup.exe e siga os prompts na tela para concluir a instalação.

## <a name="bkmk_BindCmd"></a>Operações de linha de comando

Depois de executar o Microsoft Machine Learning Server, um utilitário de linha de comando chamado SqlBindR.exe se torna disponível que você pode usar para as operações de ligação ainda mais. Por exemplo, você deve decidir reverter uma associação, você poderia executar novamente a instalação ou use o utilitário de linha de comando. Além disso, você pode usar essa ferramenta para verificar, por exemplo, compatibilidade e disponibilidade.

> [!TIP]
> Não é possível localizar SqlBindR? Você provavelmente não executou a instalação. SqlBindR está disponível somente depois de executar a instalação do Machine Learning Server.

1. Abra um prompt de comando como administrador e navegue até a pasta que contém sqlbindr.exe. O local padrão é C:\Program Files\Microsoft\MLServer\Setup

2. Digite o seguinte comando para exibir uma lista das instâncias disponíveis: `SqlBindR.exe /list`
  
   Tome nota do nome completo da instância conforme listado. Por exemplo, o nome da instância pode ser MSSQL14. MSSQLSERVER para uma instância padrão ou algo parecido com o nome do servidor. MYNAMEDINSTANCE.

3. Execute o **SqlBindR.exe** com o */BIND* argumento e especifique o nome da instância a ser atualizada, usando o nome da instância que foi retornado na etapa anterior.

   Por exemplo, para atualizar a instância padrão, digite:  `SqlBindR.exe /bind MSSQL14.MSSQLSERVER`

4. Quando a atualização for concluída, reinicie o serviço de Launchpad associado a qualquer instância que foi modificada.

## <a name="bkmk_Unbind"></a>Reverter ou desvincular uma instância

Você pode restaurar uma instância associada a uma instalação inicial dos componentes do R e Python, estabelecida pela instalação do SQL Server. Há três partes para reverter para a manutenção do SQL Server.

+ [Etapa 1: Desassociar do Microsoft Machine Learning Server](#step-1-unbind)
+ [Etapa 2: Restaure a instância para o status original](#step-2-restore)
+ [Etapa 3: Reinstalar todos os pacotes adicionadas à instalação](#step-3-reinstall-packages)

<a name="step-1-unbind"></a> 

### <a name="step-1-unbind"></a>Etapa 1: desassociar

Você tem duas opções para reverter a associação: Repetir a instalação novamente ou use o utilitário de linha de comando SqlBindR.

#### <a name="bkmk_wizunbind"></a> Desassociar usando a instalação

1. Localize o instalador para o Machine Learning Server. Se você tiver removido o instalador, talvez seja necessário baixá-lo novamente, ou copie-o de outro computador.
2. Certifique-se de executar o instalador no computador que tem a instância que você deseja desvincular.
2. O instalador identifica instâncias locais que são candidatos para a desassociação.
3. Desmarque a caixa de seleção ao lado da instância que você deseja reverter para a configuração original.
4. Aceite o contrato de licenciamento. Você deve indicar sua aceitação dos termos de licenciamento, mesmo durante a instalação.
5. Clique em **Concluir**. O processo leva algum tempo.

#### <a name="bkmk_cmdunbind"></a> Desassociar a linha de comando

1. Abra um prompt de comando e navegue até a pasta que contém **sqlbindr.exe**, conforme descrito na seção anterior.

2. Execute o comando **SqlBindR.exe** com o argumento */unbind* e especifique a instância.

   Por exemplo, o seguinte comando reverte a instância padrão:
   
    `SqlBindR.exe /unbind MSSQL14.MSSQLSERVER`

<a name="step-2-restore"></a> 

###  <a name="step-2-repair-the-sql-server-instance"></a>Etapa 2: Repare a instância do SQL Server

Execute a instalação do SQL Server para reparar a instância do mecanismo de banco de dados com os recursos de R e Python. As atualizações são preservadas, mas se você perdeu qualquer manutenção atualizações para pacotes R e Python do SQL Server, essa etapa se aplica os patches.

Como alternativa, isso é mais trabalhoso, mas também totalmente desinstalar e reinstalar a instância do mecanismo de banco de dados e, em seguida, aplique todas as atualizações de serviço.

<a name="step-3-reinstall-packages"></a> 

### <a name="step-3-add-any-third-party-packages"></a>Etapa 3: Adicionar quaisquer pacotes de terceiros

Você pode ter adicionado outros pacotes de terceiros ou de código-fonte aberto para a biblioteca de pacote. Como reverter a associação muda o local da biblioteca de pacote padrão, você deve reinstalar os pacotes à biblioteca do R e Python agora está usando. Para obter mais informações, consulte [padrão de pacotes](installing-and-managing-r-packages.md), [instalar novos pacotes de R](install-additional-r-packages-on-sql-server.md), e [instalar novos pacotes de Python](../python/install-additional-python-packages-on-sql-server.md).

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

## <a name="binding-errors"></a>Erros de ligação

Instalador de MLS e SqlBindR retornam os seguintes códigos de erro e mensagens.

|Código do erro  | Mensagem           | Detalhes               |
|------------|-------------------|-----------------------|
|Associar o erro 0 | Okey (êxito) | Associação passado sem erros. |
|Associar o erro 1 | Argumentos inválidos | Erro de sintaxe. |
|Associar o erro 2 | Ação inválida | Erro de sintaxe. |
|Associar o erro 3 | Instância inválido | Uma instância existe, mas não é válida para a associação. |
|Associar o erro 4 | Não associável | |
|Associar o erro 5 | Já vinculado | Você executou o comando *bind* , mas a instância especificada já está associada. |
|Associar o erro 6 | Falha ao vincular | Ocorreu um erro ao desassociar a instância. Esse erro pode ocorrer se você executar o instalador MLS sem selecionar todos os recursos. A associação requer que você selecione uma instância MSSQL e o R e Python, supondo que a instância é o SQL Server 2017. Esse erro também ocorrerá se SqlBindR não foi possível gravar na pasta arquivos de programa. Sessões abertas ou identificadores para o SQL Server fará com que esse erro ocorra. Se você receber esse erro, reinicie o computador e refazer as etapas de associação antes de iniciar qualquer sessão nova.|
|Associar o erro 7 | Não associado | A instância do mecanismo de banco de dados tem o R Services ou serviços do SQL Server Machine Learning. A instância não está associada a Microsoft Machine Learning Server. |
|Associar o erro 8 | Desassociar falhou | Ocorreu um erro ao desassociar a instância. |
|Associar o erro 9 | Nenhuma instância encontrada | Nenhuma instância do mecanismo de banco de dados foi encontrada neste computador. |

## <a name="known-issues"></a>Problemas conhecidos

Esta seção lista problemas conhecidos específicos para usar do utilitário SqlBindR.exe ou de atualizações de Machine Learning Server que podem afetar as instâncias do SQL Server.

### <a name="restoring-packages-that-were-previously-installed"></a>Restauração de pacotes que foram instalados anteriormente

Se você atualizou para o Microsoft R Server 9.0.1, a versão do SqlBindR.exe para essa versão Falha ao restaurar os pacotes originais ou componentes do R completamente, exigindo que o usuário executar o reparo do SQL Server na instância do se aplicam a todas as versões de serviço e, em seguida, reiniciar a instância.

Versão mais recente do SqlBindR restaurar os recursos originais do R, eliminando a necessidade de reinstalação dos componentes do R ou patch novamente o servidor automaticamente. No entanto, você deve instalar as atualizações de pacote de R que podem ter sido adicionadas após a instalação inicial.

Se você tiver usado as funções de gerenciamento de pacote para instalar e compartilhar o pacote, essa tarefa é muito mais fácil: você pode usar comandos de R para sincronizar os pacotes instalados no sistema de arquivos usando registros no banco de dados e vice-versa. Para obter mais informações, consulte [gerenciamento de pacotes de R para SQL Server](install-additional-r-packages-on-sql-server.md).

### <a name="problems-with-multiple-upgrades-from-sql-server"></a>Problemas com várias atualizações do SQL Server

Se anteriormente você tiver atualizado uma instância do SQL Server 2016 R Services para 9.0.1, quando você executar o novo instalador do Microsoft R Server 9.1.0, ele exibe uma lista de todas as instâncias válidas e, em seguida, por padrão, seleciona instâncias associadas anteriormente. Se você continuar, as instâncias associadas anteriormente serão desvinculadas. Como resultado, o 9.0.1 anteriores instalação é removida, incluindo qualquer relacionadas a pacotes, mas a nova versão do Microsoft R Server (9.1.0) não está instalada.

Como alternativa, você pode modificar a instalação existente do R Server da seguinte maneira:
1. No painel de controle, abra **adicionar ou remover programas**.
2. Localize o Microsoft R Server e, em seguida, clique em **alterar/modificar**.
3. Quando o instalador é iniciado, selecione as instâncias que você deseja associar a 9.1.0.

Microsoft Machine Learning Server 9.2.1 e 9.3 não tem esse problema.

### <a name="binding-or-unbinding-leaves-multiple-temporary-folders"></a>Associar ou desassociar deixa várias pastas temporárias

Às vezes, a ligação e desvinculação operações não conseguir limpar pastas temporárias.
Se você encontrar pastas com um nome assim, você pode removê-lo após a conclusão da instalação: R_SERVICES_<guid>

> [!NOTE]
> Certifique-se de aguardar até que a instalação for concluída. Pode levar muito tempo para remover as bibliotecas de R associados com uma versão e, em seguida, adicionar as novas bibliotecas de R. Quando a operação for concluída, as pastas temporárias são removidas.

## <a name="see-also"></a>Confira também

+ [Instale o Machine Learning Server para Windows (conectado à Internet)](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)
+ [Instale o Machine Learning Server para Windows (offline)](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-offline)
+ [Problemas conhecidos no Machine Learning Server](https://docs.microsoft.com/machine-learning-server/resources-known-issues)
+ [Lançamentos de recursos de versão anterior do R Server](https://docs.microsoft.com/r-server/whats-new-in-r-server)
+ [Recursos preteridos, descontinuados ou foi alterados](https://docs.microsoft.com/machine-learning-server/resources-deprecated-features)
