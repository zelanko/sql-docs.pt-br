---
title: "Atualizar os componentes de aprendizado de máquina em uma instância do SQL Server | Microsoft Docs"
ms.custom: 
ms.date: 10/31/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server (starting with 2016 CTP3)
ms.assetid: 4da80998-f929-4fad-a86f-87d09c1a79ef
caps.latest.revision: "15"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: 424e7d86a00901c22220d19e86b1bbced698d850
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="upgrade-machine-learning-components-in-a-sql-server-instance"></a>Atualizar os componentes de aprendizado de máquina em uma instância do SQL Server

Este artigo explica o processo de _associação_, que pode ser usado para atualizar a componentes usados no SQL Server de aprendizado de máquina. O processo de ligação de bloqueios do servidor em um ritmo de atualização com base em versões do servidor de aprendizado de máquina, em vez de usar o SQL Server de versão e agenda de atualização.

> [!IMPORTANT]
> Você não precisa usar este processo de atualização, se você deseja obter as atualizações como parte de atualizações do SQL Server. Sempre que você instala um novo service pack ou uma versão de serviço, componentes de aprendizado de máquina são automaticamente atualizados para a versão mais recente. Usar somente o _associação_ processar, se você deseja atualizar os componentes em um ritmo mais rápido do que é permitida por versões de serviço do SQL Server.

Se a qualquer momento em que você deseja parar de atualizar a agenda do servidor de aprendizado de máquina, você deve _desassociar_ a instância, conforme descrito em [nesta seção](#bkmk_Unbind)e desinstalar o servidor de aprendizado de máquina.

**Aplica-se a:** R Services do SQL Server 2016, SQL Server 2017 serviços de aprendizado de máquina

## <a name="binding-vs-upgrading"></a>Associação ou atualizar

O processo de atualização de componentes de aprendizado de máquina é conhecido como **associação**, pois ele altera o modelo de suporte para componentes de aprendizado de máquina do SQL Server usar a nova política de ciclo de vida do Software moderno. 

Em geral, alternar para o novo modelo de licenciamento garante que seus cientistas de dados sempre podem usar a versão mais recente de R ou Python. Para obter mais informações sobre os termos da política de ciclo de vida moderna, consulte [linha do tempo de suporte para o Microsoft R Server](https://docs.microsoft.com/machine-learning-server/resources-servicing-support).

> [!NOTE]
> A atualização não altera o modelo de suporte para o banco de dados do SQL Server e não altera a versão do SQL Server.

Quando você associa uma instância, várias coisas acontecem:

+ O modelo de suporte é alterado. Em vez de depender de versões de serviço do SQL Server, suporte se baseia a nova política de ciclo de vida modernos.
+ Os componentes de aprendizado de máquina associados à instância são atualizados automaticamente com cada versão, na etapa de bloqueio com a versão atual em que a nova política de ciclo de vida modernos. 
+ Novos pacotes de R ou Python podem ser adicionados. Por exemplo, as atualizações anteriores com base no Microsoft R Server 9.1 adicionados novos pacotes de R, como [MicrosoftML](../using-the-microsoftml-package.md), [olapR](../r/how-to-create-mdx-queries-using-olapr.md), e [sqlrutils](../r/how-to-create-a-stored-procedure-using-sqlrutils.md).
+ A instância não poderá mais ser atualizada manualmente, exceto para a adição de novos pacotes.
+ Você recebe a opção de instalar modelos pré-treinado fornecidos pela Microsoft.

## <a name="bkmk_prereqs"></a>Prerequisites

Comece identificando as instâncias que são candidatos para uma atualização. Se você executar o instalador e selecione a opção de associação, ele retorna uma lista de instâncias que são compatíveis com a atualização.

Consulte a tabela a seguir para obter uma lista de atualizações com suporte e requisitos.

| Versão do SQL Server| Atualização com suporte| Observações|
|-----|-----|------|
| SQL Server 2016| Servidor de aprendizado de máquina 9.2.1| Requer pelo menos Service Pack 1 e CU3. R Services deve ser instalado e habilitado.|
| SQL Server 2017| Servidor de aprendizado de máquina 9.2.1| Serviços de aprendizado de máquina (no banco de dados) deve ser instalados e habilitados. |

## <a name="bind-or-upgrade-an-instance"></a>Associar ou atualizar uma instância

Máquina de aprendizado Server para Windows inclui uma ferramenta que você pode usar para atualizar a máquina de aprendizado de linguagens e ferramentas associadas a uma instância do SQL Server. Há duas versões da ferramenta: um assistente e um utilitário de linha de comando.

Antes de executar o assistente ou a ferramenta de linha de comando, você deve baixar a versão mais recente do instalador autônomo para componentes de aprendizado de máquina.

+ [Instalar servidor 9.2.1 para Windows de aprendizado de máquina](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)

+ [Baixar os componentes necessários para a instalação offline](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-offline)

### <a name="bkmk_BindWizard"></a>Atualizar usando o novo Assistente de instalação

1. Inicie o instalador de novo para o servidor de aprendizado de máquina. Certifique-se de executar o instalador no computador que tem a instância que você deseja atualizar.

    ![Assistente de instalação do servidor de aprendizado de máquina do Microsoft](media/mls-921-installer-start.PNG)

2. Na página, **configura a instalação**, confirme os componentes para atualizar e revisar a lista de instâncias compatíveis. Se nenhuma instância for exibida, verifique o [pré-requisitos](#bkmk_prereqs).

    Para atualizar uma instância, selecione a caixa de seleção ao lado do nome de instância. Se você não selecionar uma instância, uma instalação separada do servidor de aprendizado de máquina é criada e bibliotecas do SQL Server não foram modificadas.

    ![Assistente de instalação do servidor de aprendizado de máquina do Microsoft](media/configure-the-installation.PNG)

3. Sobre o **contrato de licença** página, selecione **aceito esses termos** para aceitar os termos de licenciamento para o servidor de aprendizado de máquina. 

4. Nas páginas sucessivas, forneça seu consentimento para condições de licenciamento adicionais para os componentes de software livre selecionado, como Microsoft R Open ou a distribuição Anaconda Python.

5. Sobre o **quase lá** página, anote a pasta de instalação. A pasta padrão é `~\Program Files\Microsoft\ML Server`.

    Se você quiser alterar a pasta de instalação, clique em **avançado** para retornar para a primeira página do assistente. No entanto, você deve repetir todas as seleções anteriores.

6. Se você estiver instalando os componentes offline, você pode solicitado para o local dos componentes de aprendizado de máquina necessário, como o Microsoft R Open, servidor de Python e Python aberto.

Durante o processo de instalação, quaisquer bibliotecas de R ou Python usadas pelo SQL Server são substituídas e barra inicial é atualizado para usar os componentes mais recentes. Como resultado, se a instância usada anteriormente bibliotecas na pasta padrão R_SERVICES, após a atualização dessas bibliotecas são removidas e as propriedades para o serviço Launchpad são alteradas para usar as bibliotecas no novo local.

### <a name="bkmk_BindCmd"></a>Atualizar usando a linha de comando

Se você não quiser usar o assistente, você pode instalar o servidor de aprendizado de máquina e, em seguida, execute a ferramenta de SqlBindR.exe da linha de comando para atualizar a instância.

> [!TIP]
> 
> Não é possível localizar SqlBindR.exe? Você provavelmente não baixou os componentes listados acima. Este utilitário está disponível somente com o Windows installer para o servidor de aprendizado de máquina.

1. Abra um prompt de comando como administrador e navegue até a pasta que contém sqlbindr.exe. O local padrão é`C:\Program Files\Microsoft\MLServer\Setup`

2. Digite o seguinte comando para exibir uma lista das instâncias disponíveis: `SqlBindR.exe /list`
  
   Tome nota do nome completo da instância conforme listado. Por exemplo, o nome da instância pode ser `MSSQL14.MSSQLSERVER` para uma instância padrão ou algo parecido com `SERVERNAME.MYNAMEDINSTANCE`.

3. Execute o **SqlBindR.exe** com o */associar* argumento e especifique o nome da instância para atualizar, usando o nome de instância que foi retornado na etapa anterior.

   Por exemplo, para atualizar a instância padrão, digite:`SqlBindR.exe /bind MSSQL14.MSSQLSERVER`

4. Quando a atualização for concluída, reinicie o serviço de barra inicial associado a qualquer instância que foi modificada.

## <a name="bkmk_Unbind"></a>Reverter ou desvincular uma instância

Se você decidir que não deseja atualizar a componentes usando o servidor de aprendizado de máquina de aprendizado de máquina, você deve primeiro _desassociar_ a instância e, em seguida, desinstalar servidor de aprendizado de máquina.

+ Desassocie a instância

    Você pode desassociar a instância e reverter para as bibliotecas originais instaladas pelo SQL Server, usando qualquer um destes dois métodos:

    + [Use o Assistente de instalação](#bkmk_wizunbind) para o servidor de aprendizado de máquina e desmarque todos os recursos na instância
    + [Use o utilitário SqlBindR](#bkmk_cmdunbind) com o `/unbind` argumento, seguido pelo nome da instância.

    Quando o processo de desvinculação for concluído, atualizações com base no servidor de aprendizado de máquina de aprendizado de máquina futuras não será aplicada à instância.

+ Desinstalar o servidor de aprendizado de máquina

    Para obter instruções, consulte [desinstalar Machine Learning Server para Windows](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-uninstall). 

### <a name="bkmk_wizunbind"></a>Desassocie usando o Assistente

1. Localize o instalador para o servidor de aprendizado de máquina. Se você tiver removido o instalador, talvez seja necessário baixá-lo novamente, ou copie-o de outro computador.
2. Certifique-se de executar o instalador no computador que tem a instância que você deseja desassociar.
2. O instalador identifica as instâncias locais que são candidatos para a desassociação.
3. Desmarque a caixa de seleção ao lado de instância que você deseja reverter para a configuração original.
4. Aceite o contrato de licença. Você deve indicar a aceitação dos termos de licenciamento mesmo durante a instalação.
5. Clique em **Concluir**. O processo leva algum tempo.

### <a name="bkmk_cmdunbind"></a>Desassocie usando a linha de comando

1. Abra um prompt de comando e navegue até a pasta que contém **sqlbindr.exe**, conforme descrito na seção anterior.

2. Execute o comando **SqlBindR.exe** com o argumento */unbind* e especifique a instância.

   Por exemplo, o comando a seguir reverte a instância padrão:
   
    `SqlBindR.exe /unbind MSSQL14.MSSQLSERVER`

## <a name="known-issues"></a>Problemas conhecidos

Esta seção lista os problemas conhecidos específicos para usar o utilitário SqlBindR.exe ou atualizações do servidor de aprendizado de máquina que podem afetar a instâncias do SQL Server.

### <a name="restoring-packages-that-were-previously-installed"></a>Restaurando os pacotes que foram instalados anteriormente

O utilitário de atualização que foi incluído com o Microsoft R Server 9.0.1, o utilitário não restaurou os pacotes originais ou componentes de R completamente, exigindo que o usuário executar o reparo da instância, se aplicam a todas as versões de serviço e, em seguida, reinicie a instância.

No entanto, a versão mais recente do utilitário atualização restaura automaticamente os recursos de R originais. Portanto, você não precisa reinstalar os componentes de R ou patch novamente o servidor. No entanto, você deve instalar todos os pacotes R que talvez tenham sido adicionados após a instalação inicial.

Se você tiver usado as funções de gerenciamento de pacote para instalar e compartilhar o pacote, essa tarefa é muito mais fácil: você pode usar comandos de R para sincronizar os pacotes instalados no sistema de arquivos usando registros no banco de dados e vice-versa. Para obter mais informações, consulte [gerenciamento de pacotes de R para o SQL Server](r-package-management-for-sql-server-r-services.md).

### <a name="problems-with-multiple-upgrades-from-sql-server"></a>Problemas com várias atualizações do SQL Server

Se anteriormente você tiver atualizado uma instância do SQL Server 2016 R Services para 9.0.1, quando você executar o instalador de novo para o Microsoft R Server 9.1.0, exibe uma lista de todas as instâncias válidas e, em seguida, por padrão, seleciona instâncias associadas anteriormente. Se você continuar, as instâncias associadas anteriormente serão desvinculadas. Como resultado, o 9.0.1 anteriores instalação é removida, incluindo as relacionadas a pacotes, mas a nova versão do Microsoft R Server (9.1.0) não está instalada.

Como alternativa, você pode modificar a instalação existente do servidor de R da seguinte maneira:
1. No painel de controle, abra **adicionar ou remover programas**.
2. Localize o Microsoft R Server e, em seguida, clique em **alteração/modificação**.
3. Quando o instalador é iniciado, selecione as instâncias que você deseja associar a 9.1.0.

### <a name="binding-or-unbinding-leaves-multiple-temporary-folders"></a>Associação ou desvincular deixa várias pastas temporárias

Às vezes, a associação e operações de desvinculação falharem Limpar pastas temporárias.
Se você encontrar pastas com um nome assim, você pode removê-lo após a conclusão da instalação:`R_SERVICES_<guid>`

> [!NOTE]
> Certifique-se de aguardar até que a instalação for concluída. Ele pode levar muito tempo para remover bibliotecas de R associados com uma versão e, em seguida, adicionar novas bibliotecas de R. Quando a operação for concluída, as pastas temporárias são removidas.

## <a name="sqlbindrexe-command-syntax"></a>sintaxe do comando sqlbindr.exe

### <a name="usage"></a>Uso

`sqlbindr [/list] [/bind <SQL_instance_ID>] [/unbind <SQL_instance_ID>]`

### <a name="parameters"></a>Parâmetros

|Nome|Description|
|------|------|
|*list*| Exibe uma lista de todas as IDs de instância do Banco de Dados SQL no computador atual|
|*bind*| Atualiza a instância do Banco de Dados SQL especificada para a última versão do R Server e garante que a instância obtém automaticamente as atualizações futuras do R Server|
|*unbind*|Desinstala a última versão do R Server da instância do Banco de Dados SQL especificada e impede que atualizações futuras do R Server afetem a instância|

### <a name="errors"></a>Erros

A ferramenta retorna as seguintes mensagens de erro:

|Erro|Resolução|
|------|------|
|Erro ao associar a instância| A instância não pôde ser associada. Contate o suporte para obter assistência.|
|A instância já está associada| Você executou o comando *bind* , mas a instância especificada já está associada. Escolha outra instância.|
|A instância não está associada| Você executou o comando *unbind* , mas a instância especificada não está associada. Escolha uma instância diferente que seja compatível.|
|ID de instância SQL inválida| Você pode ter digitado o nome da instância incorretamente. Execute o comando novamente com o argumento *list* para ver as IDs de instância disponíveis.|
|Nenhuma instância encontrada| Este computador não tem uma instância do SQL Server R Services.|
|A instância deve ter uma versão compatível do SQL R Services (no Banco de Dados) instalada.| Consulte os requisitos de compatibilidade neste tópico para obter detalhes.|
|Erro ao desassociar a instância| A instância não pôde ser desassociada. Contate o suporte para obter assistência.|
|Erro inesperado| Outros erros. Contate o suporte para obter assistência.  |
|Nenhuma instância SQL encontrada| Este computador não tem uma instância do SQL Server. |

Para obter mais informações, consulte as notas de versão para o Microsoft R Server:

+ [Problemas conhecidos no servidor de aprendizado de máquina](https://docs.microsoft.com/machine-learning-server/resources-known-issues)

+ [Anúncios de recurso da versão anterior do servidor de R](https://docs.microsoft.com/r-server/whats-new-in-r-server)

+ [Recursos preteridos, descontinuados ou alterados](https://docs.microsoft.com/machine-learning-server/resources-deprecated-features)
