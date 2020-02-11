---
title: Atualizar componentes do R e do Python
description: Atualize o R e o Python nos Serviços de Machine Learning do SQL Server ou nos SQL Server R Services usando sqlbindr.exe para associar-se ao Machine Learning Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 07/30/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: abc14f78a969abd4adbbb2dcf12b4ee316614d23
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "69634547"
---
# <a name="upgrade-machine-learning-r-and-python-components-in-sql-server-instances"></a>Atualizar componentes de aprendizado de máquina (R e Python) em instâncias do SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

A integração do R e do Python no SQL Server inclui pacotes de software livre e de propriedade da Microsoft. Em serviços de SQL Server padrão, os pacotes são atualizados de acordo com o ciclo de lançamento do SQL Server com correções de bug dos pacotes existentes na versão atual, mas sem atualizações de versão principal. 

No entanto, muitos cientistas de dados estão acostumados a trabalhar com pacotes mais recentes conforme eles se tornam disponíveis. Para os Serviços de Machine Learning do SQL Server (no banco de dados) e os SQL Server R Services (no banco de dados), você pode obter [versões mais recentes do R e do Python](#version-map)*associando-se* ao **Microsoft Machine Learning Server**. 

## <a name="what-is-binding"></a>O que é associação?

A associação é um processo de instalação que altera o conteúdo de suas pastas R_SERVICES e PYTHON_SERVICES com executáveis, bibliotecas e ferramentas mais recentes do [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/index).

Junto com os componentes atualizados vem uma opção em modelos de serviço. Em vez do [ciclo de vida do produto do SQL Server](https://support.microsoft.com/lifecycle/search?alpha=SQL%20Server%202017), com as [atualizações cumulativas do SQL Server](https://support.microsoft.com/help/4047329/sql-server-2017-build-versions), suas atualizações de serviço agora estão em conformidade com a [Linha do tempo de suporte para Microsoft R Server e Machine Learning Server](https://docs.microsoft.com/machine-learning-server/resources-servicing-support) no [Ciclo de vida moderno](https://support.microsoft.com/help/30881/modern-lifecycle-policy).

Exceto para versões de componente e atualizações de serviço, a associação não altera os conceitos básicos de sua instalação: A integração do R e do Python ainda faz parte de uma instância do mecanismo de banco de dados, o licenciamento é inalterado (nenhum custo adicional vinculado à associação) e as políticas de suporte do SQL Server ainda são mantidas para o mecanismo de banco de dados. O restante deste artigo explica o mecanismo de associação e como ele funciona para cada versão do SQL Server.

> [!NOTE]
> A associação aplica-se a instâncias (no banco de dados) que estão somente associadas a instâncias do SQL Server. A associação não é relevante para uma instalação (Autônoma).

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
**Considerações de associação do SQL Server 2017**

Para os Serviços de Machine Learning do SQL Server, você consideraria associar somente quando o Microsoft Machine Learning Server começasse a oferecer pacotes adicionais ou versões mais recentes sobre o que você já tem.
::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
**Considerações de associação do SQL Server 2016**

Para clientes dos SQL Server 2016 R Services, a associação fornece pacotes do R atualizados, novos pacotes que não fazem parte da instalação original ([MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)) e [modelos pré-treinados](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models). Todos eles podem ser atualizados em cada lançamento principal e secundário do [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/index). A associação não oferece suporte ao Python, que é um recurso do SQL Server 2017.
::: moniker-end

<a name="version-map"></a>

## <a name="version-map"></a>Mapa de versão

A tabela a seguir é um mapa de versão, mostrando as versões do pacote em diferentes veículos de lançamento para você poder determinar possíveis caminhos de atualização quando associa um Microsoft Machine Learning Server (anteriormente conhecido como R Server, antes da adição do suporte ao Python da versão MLS 9.2.1 em diante). 

Observe que a associação não garante a versão mais recente do R ou do Anaconda. Ao associar-se ao MLS (Microsoft Machine Learning Server), você obtém a versão do R ou Python instalada por meio da Instalação, que pode não ser a versão mais recente disponível na Web.

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
[**SQL Server 2016 R Services**](../install/sql-r-services-windows-install.md)

Componente |Versão inicial | [R Server 9.0.1](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows) | [R Server 9.1](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows) | [MLS 9.2.1](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install) | [MLS 9.3](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install) |
----------|----------------|----------------|--------------|---------|-------|
MRO (Microsoft R Open) pelo R | R 3.2.2     | R 3.3.2   |R 3.3.3   | R 3.4.1  | R 3.4.3 |
[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) | 8.0.3  | 9.0.1 |  9.1 |  9.2.1 |  9.3 |
[MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)| n.d. | 9.0.1 |  9.1 |  9.2.1 |  9.3 |
[modelos pré-treinados](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models)| n.d. | 9.0.1 |  9.1 |  9.2.1 |  9.3 |
[sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils)| n.d. | 1.0 |  1.0 |  1.0 |  1.0 |
[olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) | n.d. | 1.0 |  1.0 |  1.0 |  1.0 |
::: moniker-end

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
[**Serviços de Machine Learning do SQL Server**](../install/sql-machine-learning-services-windows-install.md)

Componente |Versão inicial | MLS 9.3 | | | |
----------|----------------|---------|-|-|-|-|
MRO (Microsoft R Open) pelo R | R 3.3.3 | R 3.4.3 | | | |
[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) |   9.2 |  9.3 | | | |
[MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package) | 9.2  | 9.3| | | |
[sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils)| 1.0 |  1.0 | | | |
[olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) | 1.0 |  1.0 | | | |
Anaconda 4.2 no Python 3.5  | 4.2/3.5.2 | 4.2/3.5.2 | | | |
[revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) | 9.2  | 9.3| | | |
[microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) | 9.2  | 9.3| | | |
[modelos pré-treinados](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models) | 9.2 | 9.3| | | |
::: moniker-end

## <a name="how-component-upgrade-works"></a>Como funciona a atualização de componentes 

As bibliotecas e os executáveis do R e do Python são atualizados quando você associa uma instalação existente do R e do Python ao Machine Learning Server. A associação é executada pelo [instalador do Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install) quando você executa a Instalação em uma instância do mecanismo de banco de dados do SQL Server existente que tem a integração do R ou do Python. A Instalação detecta os recursos existentes e solicita que você se associe novamente ao Machine Learning Server. 

Durante a associação, o conteúdo de `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES` e `\PYTHON_SERVICES` é substituído pelos executáveis e bibliotecas mais recentes de `C:\Program Files\Microsoft\ML Server\R_SERVER` e `\PYTHON_SERVER`.

Ao mesmo tempo, o modelo de serviço também é invertido dos mecanismos de Atualização do SQL Server para o ciclo de lançamento principal e secundário mais frequente do Microsoft Machine Learning Server. Alternar as políticas de suporte é uma opção atraente para equipes de ciência de dados que exigem uma geração mais recente de módulos do R e Python para suas soluções. 

+ Sem a associação, o patch dos pacotes do R e do Python são aplicados para correções de bug quando você instala um service pack do SQL Server ou CU (atualização cumulativa). 
+ Com a associação, versões de pacote mais recentes podem ser aplicadas à sua instância, independentemente do agendamento de lançamento da CU, nos termos da [Política de Ciclo de Vida Moderno](https://support.microsoft.com/help/30881/modern-lifecycle-policy), e lançamentos do Microsoft Machine Learning Server. A política de suporte ao Ciclo de Vida Moderno oferece atualizações mais frequentes durante um período mais curto de um ano. Após a associação, você continuará usando o instalador do MLS para atualizações futuras do R e do Python à medida que elas estiverem disponíveis nos sites de download da Microsoft.

A associação aplica-se apenas aos recursos do R e do Python. Isto é, pacotes de software livre para recursos do R e do Python (Microsoft R Open, Anaconda) e os pacotes proprietários RevoScaleR, revoscalepy e assim por diante. A associação não altera o modelo de suporte da instância do mecanismo de banco de dados e não altera a versão do SQL Server.

A associação é reversível. Você pode reverter para a manutenção do SQL Server [desassociando a instância](#bkmk_Unbind) e reparando a instância do mecanismo de banco de dados do SQL Server.

Resumidamente, as etapas para associação são as seguintes:

+ Comece com uma instalação configurada existente do SQL Server R Services ou dos Serviços de Machine Learning do SQL Server.
+ Determine qual versão do Microsoft Machine Learning Server tem os componentes atualizados que você deseja usar.
+ Baixe e execute a Instalação dessa versão. A Instalação detecta a instância existente, adiciona uma opção de associação e retorna uma lista de instâncias compatíveis.
+ Escolha a instância que você deseja associar e conclua a instalação para executar a associação.

Em termos de experiência do usuário, a tecnologia e a maneira como você trabalha com ela não mudaram. A única diferença é a presença de pacotes com versão mais recente e, possivelmente, pacotes adicionais que não estavam originalmente disponíveis por meio do SQL Server.

## <a name="bkmk_BindWizard"></a>Associar-se ao MLS usando a Instalação

A Instalação do Microsoft Machine Learning detecta os recursos existentes e a versão do SQL Server e invoca um utilitário chamado SqlBindR.exe para alterar a associação. Internamente, o SqlBindR é encadeado na Instalação e usado indiretamente. Posteriormente, você pode chamar SqlBindR diretamente da linha de comando para exercer opções específicas.

1. No SSMS, execute `SELECT @@version` para verificar se o servidor atende aos requisitos mínimos de build. 

   Para SQL Server 2016 R Services, o mínimo é o [Service Pack 1](https://www.microsoft.com/download/details.aspx?id=54276) e a [CU3](https://support.microsoft.com/help/4019916/cumulative-update-3-for-sql-server-2016-sp1).

1. Verifique a versão dos pacotes R base e RevoScaleR para confirmar se as versões existentes são menores do que aquelas pelas quais você planeja substituí-las. 

    ```sql
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

1. Feche o SSMS e outras ferramentas que têm uma conexão aberta com o SQL Server. A associação substitui arquivos de programa. Se o SQL Server tiver sessões abertas, a associação falhará com o código de erro de associação 6.

1. Baixe o Microsoft Machine Learning Server para o computador que tem a instância que você deseja atualizar. Recomendamos a [versão mais recente](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install#download-machine-learning-server-installer).

1. Descompacte a pasta e inicie ServerSetup.exe, localizado em MLSWIN93.

   ![Assistente de instalação do Microsoft Machine Learning Server](media/mls-921-installer-start.PNG)

1. Em **Configurar a instalação**, confirme os componentes a serem atualizados e examine a lista de instâncias compatíveis. 

   Esta etapa é muito importante.

   À esquerda, escolha todos os recursos que você deseja manter ou atualizar. Não é possível atualizar alguns recursos e não outros. Uma caixa de seleção vazia remove esse recurso, supondo que ele esteja instalado no momento. Na captura de tela, considerando uma instância dos SQL Server 2016 R Services (MSSQL13), o R e a versão do R dos modelos pré-treinados são selecionados. Essa configuração é válida porque o SQL Server 2016 dá suporte ao R, mas não ao Python.

   Se você está atualizando componentes nos SQL Server 2016 R Services, não selecione o recurso do Python. Não é possível adicionar o Python aos SQL Server 2016 R Services.

   À direita, marque a caixa de seleção ao lado do nome da instância. Se nenhuma instância estiver listada, você terá uma combinação incompatível. Se você não selecionar uma instância, uma nova instalação autônoma do Machine Learning Server será criada e as bibliotecas do SQL Server não serão alteradas. Se não for possível selecionar uma instância, talvez ela não esteja na [CU3 do SP1](https://support.microsoft.com/help/4019916/cumulative-update-3-for-sql-server-2016-sp1). 

    ![Configurar a etapa de instalação](media/mls-931-installer-mssql13.png)

1. Na página **Contrato de licença**, selecione **Aceito esses termos** para aceitar os termos de licenciamento do Machine Learning Server. 

1. Em páginas sucessivas, forneça consentimento para condições de licenciamento adicionais para componentes de software livre selecionados, como o Microsoft R Open ou a distribuição Python Anaconda.

1. Na página **Quase lá**, anote a pasta de instalação. A pasta padrão é \Arquivos de Programas\Microsoft\ML Server.

    Se desejar alterar a pasta de instalação, clique em **Avançado** para voltar para a primeira página do assistente. No entanto, você deve repetir todas as seleções anteriores.

Durante o processo de instalação, as bibliotecas do R ou Python usadas pelo SQL Server são substituídas e o Launchpad é atualizado para usar os componentes mais recentes. Como resultado, se a instância tiver usado anteriormente bibliotecas na pasta R_SERVICES padrão, após a atualização, as bibliotecas serão removidas e as propriedades do serviço Launchpad serão alterados para usar as bibliotecas na nova localização.

A associação afeta o conteúdo destas pastas: C:\Arquivos de Programas\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library é substituída pelo conteúdo de C:\Arquivos de Programas\Microsoft\ML Server\R_SERVER. A segunda pasta e seu conteúdo são criados pela Instalação do Microsoft Machine Learning Server. 

Se a atualização falhar, verifique os [códigos de erro do SqlBindR](#sqlbindr-error-codes) para obter mais informações.

## <a name="confirm-binding"></a>Confirmar associação

Verifique novamente a versão do R e do RevoScaleR para confirmar se você tem versões mais recentes. Use o console do R distribuído com os pacotes do R em sua instância de mecanismo de banco de dados para obter informações sobre o pacote:

```sql
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

Para os SQL Server 2016 R Services associados ao Machine Learning Server 9.3, o pacote R Base deve ser 3.4.3, RevoScaleR deve ser 9.3 e você também deve ter o MicrosoftML 9.3. 

Se você adicionou os modelos pré-treinados, os modelos são inseridos na biblioteca MicrosoftML e você pode chamá-los por meio de funções MicrosoftML. Para obter mais informações, confira [Exemplos do R para MicrosoftML](https://docs.microsoft.com/machine-learning-server/r/sample-microsoftml).

## <a name="offline-binding-no-internet-access"></a>Associação offline (sem acesso à Internet)

Para sistemas sem conectividade com a Internet, você pode baixar o instalador e os arquivos .cab para um computador conectado à Internet e transferir os arquivos para o servidor isolado. 

O instalador (ServerSetup.exe) inclui os pacotes da Microsoft (RevoScaleR, MicrosoftML, olapR, sqlRUtils). Os arquivos .cab fornecem outros componentes principais. Por exemplo, o cab “SRO” fornece o R Open, a distribuição do R de software livre da Microsoft.

As instruções a seguir explicam como inserir os arquivos para uma instalação offline.

1. Baixe o instalador do MLS. Ele é baixado como um arquivo compactado único. Recomendamos a [versão mais recente](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install#download-machine-learning-server-installer), mas você também pode instalar [versões anteriores](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows-offline#download-required-components).

1. Baixe os arquivos .cab. Os links a seguir são para a versão 9.3. Se você precisar de versões anteriores, poderão ser encontrados links adicionais no [R Server 9.1](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows-offline#download-required-components). Lembre-se de que o Python/Anaconda só podem ser adicionados a uma instância dos Serviços de Machine Learning do SQL Server. Há modelos pré-treinados para o R e o Python; o .cab fornece modelos nas linguagens que você está usando.

    | Recurso | Baixar |
    |---------|----------|
    | R       | [SRO_3.4.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=867186&clcid=1033) |
    | Python  | [SPO_9.3.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=859054) | 
    | Modelos previamente treinados | [MLM_9.3.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=859053) |

1. Transfira arquivos .zip e .cab para o servidor de destino.

1. No servidor, digite `%temp%` em Executar comando para obter a localização física do diretório temporário. O caminho físico varia de acordo com o computador, mas geralmente é `C:\Users\<your-user-name>\AppData\Local\Temp`.

1. Coloque os arquivos .cab na pasta %temp%.

1. Descompacte o Instalador.

1. Execute ServerSetup.exe e siga os prompts na tela para concluir a instalação.

## <a name="bkmk_BindCmd"></a>Operações de linha de comando

Após executar o Microsoft Machine Learning Server, um utilitário de linha de comando chamado SqlBindR.exe fica disponível para você poder usar outras operações de associação. Por exemplo, se você decidir reverter uma associação, poderá executar novamente a Instalação ou usar o utilitário de linha de comando. Além disso, você pode usar essa ferramenta para verificar se há compatibilidade e disponibilidade da instância.

> [!TIP]
> Não é possível localizar o SqlBindR? Você provavelmente não executou a Instalação. O SqlBindR está disponível somente após executar a Instalação do Machine Learning Server.

1. Abra um prompt de comando como administrador e navegue até a pasta que contém sqlbindr.exe. A localização padrão é C:\Arquivos de Programas\Microsoft\MLServer\Setup

2. Digite o seguinte comando para exibir uma lista das instâncias disponíveis: `SqlBindR.exe /list`
  
   Tome nota do nome completo da instância conforme listado. Por exemplo, o nome da instância pode ser MSSQL14.MSSQLSERVER para uma instância padrão ou algo como SERVERNAME.MYNAMEDINSTANCE.

3. Execute o comando **SqlBindR.exe** com o argumento */bind* e especifique o nome da instância a ser atualizada, usando o nome da instância que foi retornado na etapa anterior.

   Por exemplo, para atualizar a instância padrão, digite: `SqlBindR.exe /bind MSSQL14.MSSQLSERVER`

4. Quando a atualização tiver sido concluída, reinicie o serviço Launchpad associado a qualquer instância que foi modificada.

## <a name="bkmk_Unbind"></a>Reverter ou desassociar uma instância

Você pode restaurar uma instância associada para uma instalação inicial dos componentes do R e do Python, estabelecida pela Instalação do SQL Server. Há três partes para reverter para os serviços do SQL Server.

+ [Etapa 1: Desassociar-se do Microsoft Machine Learning Server](#step-1-unbind)
+ [Etapa 2: Restaurar a instância para o status original](#step-2-restore)
+ [Etapa 3: Reinstalar pacotes que você adicionou à instalação](#step-3-reinstall-packages)

<a name="step-1-unbind"></a> 

### <a name="step-1-unbind"></a>Etapa 1: Desassociar

Você tem duas opções para reverter a associação: executar novamente a instalação ou usar o utilitário de linha de comando do SqlBindR.

#### <a name="bkmk_wizunbind"></a> Desassociar usando a Instalação

1. Localize o instalador para o Machine Learning Server. Se você tiver removido o instalador, talvez precise baixá-lo novamente ou copiá-lo de outro computador.
2. Execute o instalador no computador que tem a instância que você deseja desassociar.
2. O instalador identifica as instâncias locais que são candidatas à desassociação.
3. Desmarque a caixa de seleção ao lado da instância que você deseja reverter para a configuração original.
4. Aceite o contrato de licenciamento. Você deverá indicar sua aceitação dos termos de licenciamento mesmo quando estiver instalando.
5. Clique em **Concluir**. O processo leva algum tempo.

#### <a name="bkmk_cmdunbind"></a> Desassociar usando a linha de comando

1. Abra um prompt de comando e navegue até a pasta que contém **sqlbindr.exe**, conforme descrito na seção anterior.

2. Execute o comando **SqlBindR.exe** com o argumento */unbind* e especifique a instância.

   Por exemplo, o comando a seguir reverte a instância padrão:
   
    `SqlBindR.exe /unbind MSSQL14.MSSQLSERVER`

<a name="step-2-restore"></a> 

###  <a name="step-2-repair-the-sql-server-instance"></a>Etapa 2: Reparar a instância do SQL Server

Execute a Instalação do SQL Server para reparar a instância do mecanismo de banco de dados que tem os recursos do R e do Python. As atualizações existentes são preservadas, mas, se você perdeu atualizações de serviço do SQL Server para os pacotes do R e do Python, esta etapa aplica esses patches.

Como alternativa, isso é mais trabalhoso, mas você também pode desinstalar totalmente e reinstalar a instância do mecanismo de banco de dados e aplicar todas as atualizações de serviço.

<a name="step-3-reinstall-packages"></a> 

### <a name="step-3-add-any-third-party-packages"></a>Etapa 3: Adicionar pacotes de terceiros

Você pode ter adicionado outros pacotes de software livre ou de terceiros à sua biblioteca de pacotes. Como reverter a associação alterna a localização da biblioteca de pacotes padrão, você deve instalar novamente os pacotes na biblioteca que o R e o Python estão usando agora. Para obter mais informações, confira [Informações sobre pacotes do R](../package-management/r-package-information.md) e [instalação](../package-management/install-additional-r-packages-on-sql-server.md) e [Informações sobre pacotes do Python](../package-management/python-package-information.md) e [instalação](../package-management/install-additional-python-packages-on-sql-server.md).

## <a name="sqlbindrexe-command-syntax"></a>Sintaxe de comando do SqlBindR.exe

### <a name="usage"></a>Uso

`sqlbindr [/list] [/bind <SQL_instance_ID>] [/unbind <SQL_instance_ID>]`

### <a name="parameters"></a>parâmetros

|Nome|Descrição|
|------|------|
|*list*| Exibe uma lista de todas as IDs de instância do Banco de Dados SQL no computador atual|
|*bind*| Atualiza a instância do Banco de Dados SQL especificada para a última versão do R Server e garante que a instância obtém automaticamente as atualizações futuras do R Server|
|*unbind*|Desinstala a última versão do R Server da instância do Banco de Dados SQL especificada e impede que atualizações futuras do R Server afetem a instância|

<a name="sqlbindr-error-codes"><a/>

## <a name="binding-errors"></a>Erros de associação

O Instalador do MLS e o SqlBindR retornam os seguintes códigos de erro e mensagens.

|Código do erro  | Mensagem           | Detalhes               |
|------------|-------------------|-----------------------|
|Erro de associação 0 | Ok (êxito) | Associação aprovada sem erros. |
|Erro de associação 1 | Argumentos inválidos | Erro de sintaxe. |
|Erro de associação 2 | Ação inválida | Erro de sintaxe. |
|Erro de associação 3 | Instância inválida | Existe uma instância, mas não é válida para associação. |
|Erro de associação 4 | Não associável | |
|Erro de associação 5 | Já associado | Você executou o comando *bind* , mas a instância especificada já está associada. |
|Erro de associação 6 | Falha na associação | Ocorreu um erro ao desassociar a instância. Esse erro poderá ocorrer se você tiver executado o instalador do MLS sem selecionar nenhum recurso. A associação requer que você selecione uma instância do MSSQL e o R e o Python, supondo que a instância é o SQL Server 2017. Esse erro também poderá ocorrer se o SqlBindR não puder ser gravado na pasta Arquivos de Programas. Sessões ou identificadores abertos para o SQL Server gerarão esse erro. Se você receber esse erro, reinicialize o computador e refaça as etapas de associação antes de iniciar novas sessões.|
|Erro de associação 7 | Não associado | A instância do mecanismo de banco de dados tem os R Services ou os Serviços de Machine Learning do SQL Server. A instância não está associada ao Microsoft Machine Learning Server. |
|Erro de associação 8 | Falha na desassociação | Ocorreu um erro ao desassociar a instância. |
|Erro de associação 9 | Nenhuma instância encontrada | Nenhuma instância do mecanismo de banco de dados foi encontrada neste computador. |

## <a name="known-issues"></a>Problemas conhecidos

Esta seção lista problemas conhecidos para o uso do utilitário SqlBindR.exe ou para atualizações do Machine Learning Server que podem afetar as instâncias do SQL Server.

### <a name="restoring-packages-that-were-previously-installed"></a>Restaurar pacotes que foram instalados anteriormente

Se você tiver atualizado para o Microsoft R Server 9.0.1, a versão do SqlBindR.exe para essa versão não restaurou completamente os pacotes originais ou componentes do R, exigindo que o usuário execute o reparo do SQL Server na instância, aplique todas as versões do serviço e reinicie a instância.

A versão mais recente do SqlBindR restaura automaticamente os recursos originais do R, acabando com a necessidade de reinstalar os componentes do R ou aplicar patch novamente ao servidor. No entanto, você deve instalar as atualizações de pacote do R que podem ter sido adicionadas após a instalação inicial.

Se você tiver usado as funções de gerenciamento de pacotes para instalar e compartilhar o pacote, essa tarefa será muito mais fácil: você poderá usar os comandos do R para sincronizar os pacotes instalados no sistema de arquivos usando os registros no banco de dados e vice-versa. Para obter mais informações, confira [Gerenciamento de Pacotes do R para o SQL Server](../r/install-additional-r-packages-on-sql-server.md).

### <a name="problems-with-multiple-upgrades-from-sql-server"></a>Problemas com várias atualizações do SQL Server

Se você tiver atualizado anteriormente uma instância dos SQL Server 2016 R Services para a 9.0.1, quando você executar o novo instalador para Microsoft R Server 9.1.0, ele exibirá uma lista de todas as instâncias válidas e, por padrão, selecionará instâncias associadas anteriormente. Se você continuar, as instâncias associadas anteriormente serão desassociadas. Como resultado, a instalação anterior da versão 9.0.1 é removida, incluindo todos os pacotes relacionados, mas a nova versão do Microsoft R Server (9.1.0) não é instalada.

Como uma alternativa, você pode modificar a instalação existente do R Server da seguinte maneira:
1. No Painel de Controle, abra **Adicionar ou Remover Programas**.
2. Localize o Microsoft R Server e clique em **Alterar/Modificar**.
3. Quando o instalador for iniciado, selecione as instâncias que deseja associar à versão 9.1.0.

O Microsoft Machine Learning Server 9.2.1 e 9.3 não têm esse problema.

### <a name="binding-or-unbinding-leaves-multiple-temporary-folders"></a>A associação ou a desassociação deixa várias pastas temporárias

Às vezes, as operações de associação e de desassociação falham ao limpar pastas temporárias.
Se você encontrar pastas com um nome como este, poderá removê-lo depois que a instalação for concluída: R_SERVICES_<guid>

> [!NOTE]
> Aguarde até que a instalação seja concluída. Pode demorar um pouco para remover bibliotecas do R associadas a uma versão e adicionar as novas bibliotecas do R. Quando a operação for concluída, as pastas temporárias serão removidas.

## <a name="see-also"></a>Confira também

+ [Instalar o Machine Learning Server para Windows (conectado à Internet)](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)
+ [Instalar o Machine Learning Server para Windows (offline)](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-offline)
+ [Problemas Conhecidos no Machine Learning Server](https://docs.microsoft.com/machine-learning-server/resources-known-issues)
+ [Anúncios de recursos de uma versão anterior do R Server](https://docs.microsoft.com/r-server/whats-new-in-r-server)
+ [Recursos preteridos, descontinuados ou alterados](https://docs.microsoft.com/machine-learning-server/resources-deprecated-features)
