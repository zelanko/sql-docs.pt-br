---
title: Atualizar os componentes do R e do Python
description: Atualize R e Python nos serviços SQL Server 2016 ou SQL Server 2017 Serviços de Machine Learning usando o sqlbinder. exe para associar ao Machine Learning Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: def007433075920e419f0bf77be5977d1145f793
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68344964"
---
# <a name="upgrade-machine-learning-r-and-python-components-in-sql-server-instances"></a>Atualizar componentes de aprendizado de máquina (R e Python) em instâncias de SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

A integração do R e do Python no SQL Server inclui pacotes de software livre e de propriedade da Microsoft. Em serviços de SQL Server padrão, os pacotes são atualizados de acordo com o ciclo de versão do SQL Server, com correções de bugs em pacotes existentes na versão atual, mas sem atualizações de versões principais. 

No entanto, muitos cientistas de dados estão acostumados a trabalhar com pacotes mais recentes à medida que se tornam disponíveis. Para SQL Server 2017 Serviços de Machine Learning (no banco de dados) e SQL Server 2016 R Services (no banco de dados), você pode obter [versões mais recentes do R e do Python](#version-map) *ligando* -se ao **Microsoft Machine Learning Server**. 

## <a name="what-is-binding"></a>O que é Associação?

A associação é um processo de instalação que alterna o conteúdo de suas pastas R_SERVICES e PYTHON_SERVICES com executáveis, bibliotecas e ferramentas mais recentes do [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/index).

Junto com os componentes atualizados vem um switch em modelos de serviço. Em vez do [ciclo de vida do SQL Server produto](https://support.microsoft.com/lifecycle/search?alpha=SQL%20Server%202017), com [SQL Server atualizações cumulativas](https://support.microsoft.com/help/4047329/sql-server-2017-build-versions), suas atualizações de serviço agora estão em conformidade com a [linha do tempo de suporte para Microsoft R Server & Machine Learning Server](https://docs.microsoft.com/machine-learning-server/resources-servicing-support) no [ciclo de vida moderno](https://support.microsoft.com/help/30881/modern-lifecycle-policy).

Exceto para versões de componente e atualizações de serviço, a associação não altera os conceitos básicos de sua instalação: A integração do R e do Python ainda faz parte de uma instância do mecanismo de banco de dados, o licenciamento é inalterado (sem custos adicionais associados à associação) e as políticas de suporte do SQL Server ainda são mantidas para o mecanismo de banco de dados. O restante deste artigo explica o mecanismo de associação e como ele funciona para cada versão do SQL Server.

> [!NOTE]
> A associação se aplica a instâncias (no banco de dados) somente que estão associadas a instâncias de SQL Server. A associação não é relevante para uma instalação (autônoma).

**Considerações de associação do SQL Server 2017**

Para SQL Server 2017 Serviços de Machine Learning, você consideraria a vinculação somente quando Microsoft Machine Learning Server começar a oferecer pacotes adicionais ou versões mais recentes sobre o que você já tem.

**Considerações de associação do SQL Server 2016**

Para clientes de 2016 SQL Server R Services, a associação fornece pacotes R atualizados, novos pacotes que não fazem parte da instalação original ([MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)) e modelos pré- [treinados](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models), todos os quais podem ser atualizados em cada nova versão principal e secundária do [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/index). A associação não oferece suporte ao Python, que é um recurso SQL Server 2017. 

<a name="version-map"></a>

## <a name="version-map"></a>Mapa de versão

A tabela a seguir é um mapa de versão, mostrando as versões de pacote em veículos de lançamento, para que você possa determinar possíveis caminhos de atualização ao associar a Microsoft Machine Learning Server (anteriormente conhecido como servidor R, antes da adição do suporte do Python iniciando em MLS 9.2.1). 

Observe que a associação não garante a versão mais recente do R ou do Anaconda. Ao ligar-se a Microsoft Machine Learning Server (MLS), você obtém a versão do R ou do Python instalada por meio da instalação, que pode não ser a versão mais recente disponível na Web.

[**SQL Server 2016 R Services**](../install/sql-r-services-windows-install.md)

Componente |Versão inicial | [9.0.1 do R Server](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows) | [R Server 9,1](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows) | [MLS 9.2.1](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install) | [MLS 9,3](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install) |
----------|----------------|----------------|--------------|---------|-------|
Microsoft R Open (MRO) sobre R | R 3.2.2     | R 3.3.2   |R 3.3.3   | R 3.4.1  | R 3.4.3 |
[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) | 8.0.3  | 9.0.1 |  9,1 |  9.2.1 |  9,3 |
[MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)| NA | 9.0.1 |  9,1 |  9.2.1 |  9,3 |
[modelos pretreinados](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models)| NA | 9.0.1 |  9,1 |  9.2.1 |  9,3 |
[sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils)| NA | 1.0 |  1.0 |  1.0 |  1.0 |
[olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) | NA | 1.0 |  1.0 |  1.0 |  1.0 |


[**SQL Server 2017 Serviços de Machine Learning**](../install/sql-machine-learning-services-windows-install.md)

Componente |Versão inicial | MLS 9,3 | | | |
----------|----------------|---------|-|-|-|-|
Microsoft R Open (MRO) sobre R | R 3.3.3 | R 3.4.3 | | | |
[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) |   9,2 |  9,3 | | | |
[MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package) | 9,2  | 9,3| | | |
[sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils)| 1.0 |  1.0 | | | |
[olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) | 1.0 |  1.0 | | | |
Anaconda 4,2 sobre Python 3,5  | 4.2/3.5.2 | 4.2/3.5.2 | | | |
[revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) | 9,2  | 9,3| | | |
 [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) | 9,2  | 9,3| | | |
[modelos pretreinados](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models) | 9,2 | 9,3| | | |

## <a name="how-component-upgrade-works"></a>Como funciona a atualização de componentes 

As bibliotecas e os executáveis do r e Python são atualizados quando você associa uma instalação existente do R e do Python ao Machine Learning Server. A associação é executada pelo [instalador de Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install) quando você executa a instalação em uma instância existente do mecanismo de banco de dados do SQL Server, 2016 ou 2017, tendo a integração do R ou do Python. A instalação detecta os recursos existentes e solicita que você reassocie a Machine Learning Server. 

Durante a associação, o conteúdo de C:\Program Files\Microsoft SQL Server\MSSQL14. O MSSQLSERVER\R_SERVICES e o \PYTHON_SERVICES são substituídos pelos executáveis e bibliotecas mais recentes de C:\Program Programas\microsoft\ml Server\R_SERVER e \PYTHON_SERVER.

Ao mesmo tempo, o modelo de serviço também é invertido de SQL Server mecanismos de atualização para o ciclo de lançamento principal e secundário mais frequente de Microsoft Machine Learning Server. A alternância de políticas de suporte é uma opção atraente para equipes de ciência de dados que exigem módulos R e Python de geração mais recentes para suas soluções. 

+ Sem associação, os pacotes R e Python são corrigidos para correções de bugs quando você instala um SQL Server service pack ou uma atualização cumulativa (CU). 
+ Com a associação, as versões mais recentes do pacote podem ser aplicadas à sua instância, independentemente do horário de lançamento da CU, sob a [política de ciclo de vida moderna](https://support.microsoft.com/help/30881/modern-lifecycle-policy) e as versões do Microsoft Machine Learning Server. A política de suporte ao ciclo de vida moderno oferece atualizações mais frequentes em um ciclo de vida mais curto e de um ano. Após a associação, você continuaria a usar o instalador do MLS para atualizações futuras do R e do Python à medida que eles estiverem disponíveis nos sites de download da Microsoft.

A associação aplica-se somente aos recursos do R e do Python. Ou seja, pacotes de código-fonte aberto para recursos de R e Python (Microsoft R Open, Anaconda) e os pacotes proprietários RevoScaleR, revoscalepy e assim por diante. A associação não altera o modelo de suporte para a instância do mecanismo de banco de dados e não altera a versão do SQL Server.

A associação é reversível. Você pode reverter para SQL Server manutenção desassociando [a instância](#bkmk_Unbind) e reparingndo sua instância do mecanismo de banco de dados SQL Server.

Somadas, as etapas para associação são as seguintes:

+ Inicie com uma instalação existente configurada do SQL Server 2016 R Services (ou SQL Server 2017 Serviços de Machine Learning).
+ Determine qual versão do Microsoft Machine Learning Server tem os componentes atualizados que você deseja usar.
+ Baixe e execute a instalação para essa versão. A instalação detecta a instância existente, adiciona uma opção de associação e retorna uma lista de instâncias compatíveis.
+ Escolha a instância que você deseja associar e, em seguida, conclua a instalação para executar a associação.

Em termos de experiência do usuário, a tecnologia e como você trabalha com ela não é alterada. A única diferença é a presença de pacotes com versão mais recente e, possivelmente, pacotes adicionais que não estavam originalmente disponíveis por meio de SQL Server (como MicrosoftML para clientes de SQL Server 2016 R Services).

## <a name="bkmk_BindWizard"></a>Associar a MLS usando a instalação

A instalação do Microsoft Machine Learning detecta os recursos existentes e SQL Server versão e invoca um utilitário chamado sqlbindr. exe para alterar a associação. Internamente, o sqlbindr é encadeado para a instalação e usado indiretamente. Posteriormente, você pode chamar sqlbindr diretamente da linha de comando para exercer opções específicas.

1. No SSMS, execute `SELECT @@version` para verificar se o servidor atende aos requisitos mínimos de compilação. 

   Para SQL Server R Services 2016, o mínimo é [Service Pack 1](https://www.microsoft.com/download/details.aspx?id=54276) e [Cu3](https://support.microsoft.com/help/4019916/cumulative-update-3-for-sql-server-2016-sp1).

1. Verifique a versão dos pacotes R base e RevoScaleR para confirmar se as versões existentes são menores do que você planeja substituí-las. Para SQL Server R Services 2016, o pacote base do R é 3.2.2 e RevoScaleR é 8.0.3.

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

1. Feche o SSMS e todas as outras ferramentas que têm uma conexão aberta com o SQL Server. A vinculação substitui os arquivos de programa. Se SQL Server tiver sessões abertas, a associação falhará com o código de erro de ligação 6.

1. Baixe Microsoft Machine Learning Server no computador que tem a instância que você deseja atualizar. Recomendamos a [versão mais recente](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install#download-machine-learning-server-installer).

1. Descompacte a pasta e inicie o Server. exe, localizado em MLSWIN93.

   ![Assistente de instalação do Microsoft Machine Learning Server](media/mls-921-installer-start.PNG)

1. Em **Configurar a instalação**, confirme os componentes a serem atualizados e examine a lista de instâncias compatíveis. 

   Esta etapa é muito importante.

   À esquerda, escolha todos os recursos que você deseja manter ou atualizar. Não é possível atualizar alguns recursos e não outros. Uma caixa de seleção vazia remove esse recurso, supondo que ele esteja instalado no momento. Na captura de tela, dada uma instância de SQL Server MSSQL13 (2016 R Services), R e a versão R dos modelos pré-treinados são selecionadas. Esta configuração é válida porque SQL Server 2016 dá suporte a R, mas não a Python.

   Se você estiver atualizando componentes do SQL Server R Services 2016, não selecione o recurso Python. Não é possível adicionar Python a SQL Server 2016 R Services.

   À direita, marque a caixa de seleção ao lado do nome da instância. Se nenhuma instância estiver listada, você terá uma combinação incompatível. Se você não selecionar uma instância do, uma nova instalação autônoma do Machine Learning Server será criada e as bibliotecas de SQL Server não serão alteradas. Se você não puder selecionar uma instância, ela poderá não estar no [SP1 Cu3](https://support.microsoft.com/help/4019916/cumulative-update-3-for-sql-server-2016-sp1). 

    ![Configurar etapa de instalação](media/mls-931-installer-mssql13.png)

1. Na página **contrato de licença** , selecione aceito **estes termos** para aceitar os termos de licença para Machine Learning Server. 

1. Em páginas sucessivas, forneça consentimento para condições de licenciamento adicionais para todos os componentes de software livre selecionados, como o Microsoft R Open ou a distribuição Python Anaconda.

1. Na página **quase lá** , anote a pasta de instalação. A pasta padrão é \Program Programas\microsoft\ml Server.

    Se você quiser alterar a pasta de instalação, clique em **avançado** para retornar à primeira página do assistente. No entanto, você deve repetir todas as seleções anteriores.

Durante o processo de instalação, todas as bibliotecas de R ou Python usadas pelo SQL Server são substituídas e o Launchpad é atualizado para usar os componentes mais recentes. Como resultado, se a instância usou anteriormente as bibliotecas na pasta padrão R_SERVICES, após a atualização, essas bibliotecas serão removidas e as propriedades do serviço Launchpad serão alteradas para usar as bibliotecas no novo local.

A associação afeta o conteúdo dessas pastas: C:\Arquivos de Programas\microsoft SQL Server\MSSQL13. MSSQLSERVER\R_SERVICES\library é substituído pelo conteúdo de C:\Program Programas\microsoft\ml Server\R_SERVER. A segunda pasta e seu conteúdo são criados pela instalação do Microsoft Machine Learning Server. 

Se a atualização falhar, verifique os [códigos de erro](#sqlbindr-error-codes) do sqlbindr para obter mais informações.

## <a name="confirm-binding"></a>Confirmar Associação

Verifique novamente a versão do R e do RevoScaleR para confirmar que você tem versões mais recentes. Use o console do R distribuído com os pacotes do R em sua instância do mecanismo de banco de dados para obter informações do pacote:

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

Para SQL Server R Services 2016 associado a Machine Learning Server 9,3, o pacote base do R deve ser 3.4.3, RevoScaleR deve ser 9,3 e você também deve ter MicrosoftML 9,3. 

Se você adicionou os modelos pré-treinados, os modelos serão inseridos na biblioteca MicrosoftML e você poderá chamá-los por meio de funções MicrosoftML. Para obter mais informações, consulte [exemplos de R para MicrosoftML](https://docs.microsoft.com/machine-learning-server/r/sample-microsoftml).

## <a name="offline-binding-no-internet-access"></a>Associação offline (sem acesso à Internet)

Para sistemas sem conectividade com a Internet, você pode baixar o instalador e os arquivos. cab em um computador conectado à Internet e, em seguida, transferir arquivos para o servidor isolado. 

O instalador (Server. exe) inclui os pacotes da Microsoft (RevoScaleR, MicrosoftML, olapr, sqlRUtils). Os arquivos. cab fornecem outros componentes principais. Por exemplo, o cab "SRO" fornece R Open, a distribuição da Microsoft do R de software livre.

As instruções a seguir explicam como posicionar os arquivos para uma instalação offline.

1. Baixe o instalador do MLS. Ele é baixado como um único arquivo compactado. Recomendamos a [versão mais recente](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install#download-machine-learning-server-installer), mas você também pode instalar [versões anteriores](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows-offline#download-required-components).

1. Baixe arquivos. cab. Os links a seguir são para a versão 9,3. Se você precisar de versões anteriores, links adicionais podem ser encontrados no [R Server 9,1](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows-offline#download-required-components). Lembre-se de que o Python/Anaconda só pode ser adicionado a uma instância de Serviços de Machine Learning SQL Server 2017. Existem modelos pré-treinados para R e Python; o. cab fornece modelos nos idiomas que você está usando.

    | Recurso | Download |
    |---------|----------|
    | R       | [SRO_3.4.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=867186&clcid=1033) |
    | Python  | [SPO_9.3.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=859054) | 
    | Modelos previamente treinados | [MLM_9.3.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=859053) |

1. Transfira arquivos. zip e. cab para o servidor de destino.

1. No servidor, digite `%temp%` o comando executar para obter o local físico do diretório temporário. O caminho físico varia de acordo com a máquina, mas `C:\Users\<your-user-name>\AppData\Local\Temp`geralmente é.

1. Coloque os arquivos. cab na pasta% Temp%.

1. Descompacte o instalador.

1. Execute Server. exe e siga os prompts na tela para concluir a instalação.

## <a name="bkmk_BindCmd"></a>Operações de linha de comando

Depois de executar Microsoft Machine Learning Server, um utilitário de linha de comando chamado sqlbindr. exe torna-se disponível para que você possa usar para operações de ligação adicionais. Por exemplo, se você decidir reverter uma associação, poderá executar novamente a instalação ou usar o utilitário de linha de comando. Além disso, você pode usar essa ferramenta para verificar a compatibilidade e a disponibilidade da instância.

> [!TIP]
> Não é possível localizar o sqlbindr? Você provavelmente não executou a instalação. O sqlbindr está disponível somente após a execução da instalação do Machine Learning Server.

1. Abra um prompt de comando como administrador e navegue até a pasta que contém sqlbindr.exe. O local padrão é C:\Program Files\Microsoft\MLServer\Setup

2. Digite o seguinte comando para exibir uma lista das instâncias disponíveis: `SqlBindR.exe /list`
  
   Tome nota do nome completo da instância conforme listado. Por exemplo, o nome da instância pode ser MSSQL14. MSSQLSERVER para uma instância padrão ou algo como SERVERname. MYNAMEDINSTANCE.

3. Execute o comando sqlbindr **. exe** com o argumento */BIND* e especifique o nome da instância a ser atualizada, usando o nome da instância que foi retornado na etapa anterior.

   Por exemplo, para atualizar a instância padrão, digite:`SqlBindR.exe /bind MSSQL14.MSSQLSERVER`

4. Quando a atualização for concluída, reinicie o serviço Launchpad associado a qualquer instância que tenha sido modificada.

## <a name="bkmk_Unbind"></a>Reverter ou desassociar uma instância

Você pode restaurar uma instância associada para uma instalação inicial dos componentes do R e do Python, estabelecida pela instalação do SQL Server. Há três partes para reverter para o serviço de SQL Server.

+ [Etapa 1: Desassociar de Microsoft Machine Learning Server](#step-1-unbind)
+ [Etapa 2: Restaurar a instância para o status original](#step-2-restore)
+ [Etapa 3: Reinstale os pacotes que você adicionou à instalação](#step-3-reinstall-packages)

<a name="step-1-unbind"></a> 

### <a name="step-1-unbind"></a>Etapa 1: Desvincular

Você tem duas opções para reverter a associação: executar novamente a instalação ou usar o utilitário de linha de comando sqlbindr.

#### <a name="bkmk_wizunbind"></a>Desassociar usando a instalação

1. Localize o instalador para Machine Learning Server. Se você tiver removido o instalador, talvez seja necessário baixá-lo novamente ou copiá-lo de outro computador.
2. Certifique-se de executar o instalador no computador que tem a instância que você deseja desassociar.
2. O instalador identifica as instâncias locais que são candidatos à desvinculação.
3. Desmarque a caixa de seleção ao lado da instância que você deseja reverter para a configuração original.
4. Aceite o contrato de licenciamento. Você deve indicar sua aceitação de termos de licenciamento mesmo ao instalar o.
5. Clique em **Finalizar**. O processo leva algum tempo.

#### <a name="bkmk_cmdunbind"></a>Desassociar usando a linha de comando

1. Abra um prompt de comando e navegue até a pasta que contém **sqlbindr.exe**, conforme descrito na seção anterior.

2. Execute o comando **SqlBindR.exe** com o argumento */unbind* e especifique a instância.

   Por exemplo, o comando a seguir reverte a instância padrão:
   
    `SqlBindR.exe /unbind MSSQL14.MSSQLSERVER`

<a name="step-2-restore"></a> 

###  <a name="step-2-repair-the-sql-server-instance"></a>Etapa 2: Reparar a instância de SQL Server

Execute SQL Server instalação para reparar a instância do mecanismo de banco de dados que tem os recursos R e Python. As atualizações existentes são preservadas, mas se você tiver perdido alguma atualização de serviço de SQL Server para pacotes R e Python, essa etapa aplicará esses patches.

Como alternativa, isso é mais trabalho, mas você também pode desinstalar e reinstalar completamente a instância do mecanismo de banco de dados e aplicar todas as atualizações de serviço.

<a name="step-3-reinstall-packages"></a> 

### <a name="step-3-add-any-third-party-packages"></a>Etapa 3: Adicionar pacotes de terceiros

Você pode ter adicionado outros pacotes de código-fonte aberto ou de terceiros à biblioteca de pacotes. Como a reversão da Associação alterna o local da biblioteca de pacotes padrão, você deve reinstalar os pacotes na biblioteca que o R e o Python estão usando agora. Para obter mais informações, consulte [pacotes padrão](../package-management/default-packages.md), [instalar novos pacotes de R](../r/install-additional-r-packages-on-sql-server.md)e [instalar novos pacotes do python](../python/install-additional-python-packages-on-sql-server.md).

## <a name="sqlbindrexe-command-syntax"></a>Sintaxe do comando sqlbindr. exe

### <a name="usage"></a>Uso

`sqlbindr [/list] [/bind <SQL_instance_ID>] [/unbind <SQL_instance_ID>]`

### <a name="parameters"></a>Parâmetros

|Nome|Descrição|
|------|------|
|*list*| Exibe uma lista de todas as IDs de instância do Banco de Dados SQL no computador atual|
|*bind*| Atualiza a instância do Banco de Dados SQL especificada para a última versão do R Server e garante que a instância obtém automaticamente as atualizações futuras do R Server|
|*unbind*|Desinstala a última versão do R Server da instância do Banco de Dados SQL especificada e impede que atualizações futuras do R Server afetem a instância|

<a name="sqlbindr-error-codes"><a/>

## <a name="binding-errors"></a>Erros de associação

O instalador de MLS e o sqlbindr retornam os seguintes códigos de erro e mensagens.

|Código do erro  | Message           | Detalhes               |
|------------|-------------------|-----------------------|
|Erro de ligação 0 | Ok (êxito) | Associação aprovada sem erros. |
|Erro de ligação 1 | Argumentos inválidos | Erro de sintaxe. |
|Erro de ligação 2 | Ação inválida | Erro de sintaxe. |
|Erro de ligação 3 | Instância inválida | Existe uma instância, mas não é válida para associação. |
|Erro de ligação 4 | Não vinculável | |
|Erro de ligação 5 | Já associado | Você executou o comando *bind* , mas a instância especificada já está associada. |
|Erro de ligação 6 | Falha na ligação | Ocorreu um erro ao desassociar a instância. Esse erro pode ocorrer se você executar o instalador do MLS sem selecionar nenhum recurso. A associação requer que você selecione uma instância MSSQL e R e Python, supondo que a instância é SQL Server 2017. Esse erro também ocorrerá se o sqlbinderr não pôde gravar na pasta arquivos de programas. As sessões ou identificadores abertos para SQL Server farão com que esse erro ocorra. Se você receber esse erro, reinicialize o computador e refaça as etapas de associação antes de iniciar novas sessões.|
|Erro de ligação 7 | Não associado | A instância do mecanismo de banco de dados tem R Services ou SQL Server Serviços de Machine Learning. A instância não está associada a Microsoft Machine Learning Server. |
|Erro de ligação 8 | Falha ao desassociar | Ocorreu um erro ao desassociar a instância. |
|Erro de ligação 9 | Nenhuma instância encontrada | Nenhuma instância do mecanismo de banco de dados foi encontrada neste computador. |

## <a name="known-issues"></a>Problemas conhecidos

Esta seção lista os problemas conhecidos específicos ao uso do utilitário sqlbinder. exe ou às atualizações de Machine Learning Server que podem afetar SQL Server instâncias.

### <a name="restoring-packages-that-were-previously-installed"></a>Restaurando pacotes que foram instalados anteriormente

Se você atualizou para Microsoft R Server 9.0.1, a versão do sqlbinder. exe para essa versão não pôde restaurar completamente os pacotes originais ou os componentes do R, exigindo que o usuário execute SQL Server reparar na instância, aplique todas as versões de serviço e reinicie a instância.

A versão mais recente do sqlbindr restaura automaticamente os recursos originais do R, eliminando a necessidade de reinstalação de componentes do R ou reformular o servidor. No entanto, você deve instalar todas as atualizações de pacote do R que podem ter sido adicionadas após a instalação inicial.

Se você usou as funções de gerenciamento de pacote para instalar e compartilhar o pacote, essa tarefa é muito mais fácil: você pode usar comandos do R para sincronizar pacotes instalados no sistema de arquivos usando registros no banco de dados e vice-versa. Para obter mais informações, consulte [Gerenciamento de pacotes de R para SQL Server](../r/install-additional-r-packages-on-sql-server.md).

### <a name="problems-with-multiple-upgrades-from-sql-server"></a>Problemas com várias atualizações do SQL Server

Se você atualizou uma instância do SQL Server 2016 R Services para 9.0.1, ao executar o novo instalador para Microsoft R Server 9.1.0, ele exibirá uma lista de todas as instâncias válidas e, por padrão, selecionará as instâncias associadas anteriormente. Se você continuar, as instâncias associadas anteriormente serão desassociadas. Como resultado, a instalação anterior do 9.0.1 é removida, incluindo todos os pacotes relacionados, mas a nova versão do Microsoft R Server (9.1.0) não está instalada.

Como alternativa, você pode modificar a instalação existente do R Server da seguinte maneira:
1. No painel de controle, abra **Adicionar ou remover programas**.
2. Localize Microsoft R Server e clique em **alterar/modificar**.
3. Quando o instalador for iniciado, selecione as instâncias que você deseja associar a 9.1.0.

Microsoft Machine Learning Server 9.2.1 e 9,3 não têm esse problema.

### <a name="binding-or-unbinding-leaves-multiple-temporary-folders"></a>A vinculação ou desvinculação deixa várias pastas temporárias

Às vezes, as operações de vinculação e desvinculação falham ao limpar pastas temporárias.
Se você encontrar pastas com um nome como este, poderá removê-lo após a conclusão da instalação: R_SERVICES_<guid>

> [!NOTE]
> Certifique-se de aguardar até que a instalação seja concluída. Pode levar muito tempo para remover bibliotecas de R associadas a uma versão e, em seguida, adicionar as novas bibliotecas de R. Quando a operação for concluída, as pastas temporárias serão removidas.

## <a name="see-also"></a>Confira também

+ [Instalar o Machine Learning Server para Windows (conectado à Internet)](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)
+ [Instalar o Machine Learning Server para Windows (offline)](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-offline)
+ [Problemas conhecidos no Machine Learning Server](https://docs.microsoft.com/machine-learning-server/resources-known-issues)
+ [Anúncios de recursos da versão anterior do R Server](https://docs.microsoft.com/r-server/whats-new-in-r-server)
+ [Recursos preteridos, descontinuados ou alterados](https://docs.microsoft.com/machine-learning-server/resources-deprecated-features)
