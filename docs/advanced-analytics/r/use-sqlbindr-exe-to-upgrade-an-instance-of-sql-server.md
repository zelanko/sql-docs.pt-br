---
title: "Atualizar os componentes de aprendizado de máquina em uma instância do SQL Server | Microsoft Docs"
ms.custom: 
ms.date: 07/31/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server (starting with 2016 CTP3)
ms.assetid: 4da80998-f929-4fad-a86f-87d09c1a79ef
caps.latest.revision: 15
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2d9d7ddd95bdbcf6efca98ed94bc305924902b98
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="upgrade-machine-learning-components-in-a-sql-server-instance"></a>Atualizar os componentes de aprendizado de máquina em uma instância do SQL Server

Servidor de aprendizado de máquina Microsoft para Windows inclui uma ferramenta que você pode usar para atualizar os componentes de R associados a uma instância do SQL Server. Há duas versões da ferramenta: um assistente e um utilitário de linha de comando.

Este artigo descreve como usar essas ferramentas para atualizar uma instância do SQL Server compatível com e como reverter uma instância que foi atualizada anteriormente.

Você não precisa usar este processo de atualização, se você deseja obter as atualizações como parte de atualizações do SQL Server. Sempre que você instala um novo service pack ou uma versão de serviço, componentes de aprendizado de máquina são automaticamente atualizados para a versão mais recente. Somente use esse proess se você deseja atualizar os componentes em um ritmo mais rápido que o affored por versões de serviço do SLQ Server.

**Aplica-se a:** R Services do SQL Server 2016, SQL Server 2017 serviços de aprendizado de máquina

> [!NOTE]
> No momento da redação deste artigo, atualizações se aplicam apenas às instâncias do SQL Server 2016 compatíveis.  Embora a atualização é compatível com SQL Server 2017, uma nova versão do Microsoft Server de aprendizado de máquina usar para atualizações não foi liberada.

## <a name="upgrade-an-instance"></a>Atualizar uma instância

O processo de atualização é conhecido como **associação**, pois ele altera o modelo de suporte para componentes de aprendizado de máquina do SQL Server usar a nova política de ciclo de vida modernos. No entanto, a atualização não altera o modelo de suporte para o banco de dados do SQL Server.

Em geral, esse sistema licenciamento garante que seus cientistas de dados sempre usem a versão mais recente de R. Para obter mais informações sobre os termos da Política de ciclo de vida moderno, consulte [Linha do tempo de suporte para o Microsoft R Server](https://msdn.microsoft.com/microsoft-r/rserver-servicing-support).

Quando você associa uma instância, várias coisas acontecem:

+ O modelo de suporte é alterado. Em vez de depender de versões de serviço do SQL Server, suporte se baseia a nova política de ciclo de vida modernos.
+ A componentes associados com a instância de aprendizado de máquina será atualizada automaticamente com cada versão, na etapa de bloqueio com a versão atual em que a nova política de ciclo de vida modernos. 
+ Novos pacotes de R ou Python podem ser adicionados. Por exemplo, as atualizações anteriores do Microsoft R Server adicionados novos pacotes de R, como [MicrosoftML](../using-the-microsoftml-package.md), [olapR](../r/how-to-create-mdx-queries-using-olapr.md), e [sqlrutils](../r/how-to-create-a-stored-procedure-using-sqlrutils.md).
+ A instância não poderá mais ser atualizada manualmente, exceto para a adição de novos pacotes.
+ Você tem a opção para adicionar modelos de pré-treinado.

Se você decidir posteriormente que deseja interromper a atualização da instância em cada versão, você deve **desassociar** a instância, conforme descrito em [nesta seção](#bkmk_Unbind)e, em seguida, desinstale a máquina de aprendizado atualizações conforme descrito neste artigo: [executar Microsoft R Server para Windows](https://msdn.microsoft.com/microsoft-r/rserver-install-windows). Quando o processo for concluído, atualizações com base no servidor de aprendizado de máquina de aprendizado de máquina futuras não será aplicada à instância.

### <a name="bkmk_prereqs"></a>Pré-requisitos para atualização

1. Identificar instâncias candidatas a uma atualização.
    + SQL Server 2016 com o R Services instalado
    + Pelo menos Service Pack 1 mais CU3

2. Obter **Microsoft R Server**, baixando o Windows installer separado.

    [Como instalar o R Server 9.0.1 no Windows usando o instalador autônomo do Windows Installer](https://msdn.microsoft.com/microsoft-r/rserver-install-windows#howtoinstall)

> [!TIP]
> 
> Não é possível localizar SqlBindR.exe? Você provavelmente não baixou R Server ainda. Este utilitário está disponível somente com o Windows installer para o Microsoft R Server.

### <a name="bkmk_BindWizard"></a>Atualizar usando o novo Assistente de instalação

1. Inicie o novo instalador para o servidor do R no computador que tem a instância que você deseja atualizar.
  ![Assistente de instalação do Microsoft R Server](media/r-server-installer-01.PNG)
2. Aceite o contrato de licença para o Microsoft R Server 9.1.0 e, em seguida, clique em **próximo**.
3. Aceite as condições de licenciamento para os componentes de software livre R e clique em **próximo**.
4. Em **Selecionar pasta de instalação**, aceite os padrões ou especificar um local diferente em que as bibliotecas de R serão instaladas. 
5. O instalador identificará todas as instâncias locais que são candidatos para a associação. Se nenhuma instância for mostrada, isso significa que nenhuma instância válida foi encontrada. Talvez seja necessário corrigir o servidor ou verifique se o R Services foi instalado.
6. Marque a caixa de seleção ao lado de qualquer instância que você deseja atualizar e, em seguida, clique em **próximo**.
7. O processo pode demorar um pouco.
    
    Durante a instalação, as bibliotecas de R usadas pelo SQL Server R Services são substituídas com as bibliotecas do Microsoft R Server 9.1.0.
    
    Barra inicial não é afetado pelo processo, mas as bibliotecas na pasta R_SERVICES serão removidas e as propriedades para o serviço serão alteradas para usar as bibliotecas em `C:\Program Files\Microsoft\R Server\R_SERVER`.

### <a name="bkmk_BindCmd"></a>Atualizar usando a linha de comando

Depois que o Microsoft R Server tiver sido instalado, você pode executar a ferramenta de SqlBindR.exe da linha de comando.

1. Abra um prompt de comando como administrador e navegue até a pasta que contém sqlbindr.exe. O local padrão é`C:\Program Files\Microsoft\R Server\Setup`
2. Digite o seguinte comando para exibir uma lista das instâncias disponíveis: `SqlBindR.exe /list`
  
   Tome nota do nome completo da instância conforme listado. Por exemplo, o nome da instância pode ser `MSSQL13.MSSQLSERVER` para a instância padrão ou algo parecido com `SERVERNAME.MYNAMEDINSTANCE`.
3. Execute o comando **SqlBindR.exe** com o argumento */bind* e especifique o nome da instância a atualizar, conforme retornado na etapa anterior.

   Por exemplo, para atualizar a instância padrão, digite:`SqlBindR.exe /bind MSSQL13.MSSQLSERVER`
4. Quando a atualização tiver sido concluída, reinicie o serviço de Launchpad associado a qualquer instância que tenha sido modificada.


## <a name="bkmk_Unbind"></a>Reverter ou desvincular uma instância

Para restaurar uma instância do SQL Server para usar as bibliotecas originais instaladas pelo SQL Server, você deve executar uma **desassociar** operação. Você pode fazer isso executando novamente o Assistente de instalação para o Microsoft R Server, ou executando o utilitário SqlBindR da linha de comando.

Ao desvincular é concluída, as bibliotecas do Microsoft R Server 9.1.0 são removidas e as bibliotecas de R originais usadas pelo SQL Server R Services são restauradas.

As propriedades do Launchpad do SQL Server são editadas para usar as bibliotecas de R na pasta padrão para R_SERVICES, em `C:\Program Files\Microsoft\R Server\R_SERVER`.

### <a name="unbind-using-the-wizard"></a>Desassocie usando o Assistente

1. Baixe o novo instalador para o Microsoft R Server 9.1.0.
2. Execute o instalador no computador que tem a instância que você deseja desassociar.
2. O instalador identificará as instâncias locais que são candidatos para a desassociação.
3. Desmarque a caixa de seleção ao lado de instância que você deseja reverter para a configuração original do SQL Server R Services.
4. Aceite o contrato de licença para o Microsoft R Server 9.1.0. Você deve aceitar o contrato de licença, mesmo se você estiver removendo o R Server.
5. Clique em **Concluir**. O processo leva algum tempo.

### <a name="unbind-using-the-command-line"></a>Desassocie usando a linha de comando

1. Abra um prompt de comando e navegue até a pasta que contém **sqlbindr.exe**, conforme descrito na seção anterior.

2. Execute o comando **SqlBindR.exe** com o argumento */unbind* e especifique a instância.

   Por exemplo, o comando a seguir reverte a instância padrão:
   
    `SqlBindR.exe /unbind MSSQL13.MSSQLSERVER`

## <a name="known-issues"></a>Problemas conhecidos

Esta seção lista os problemas conhecidos específicos para usar o utilitário SqlBindR.exe ou atualizações usando o utilitário de instalação do Microsoft R Server que afetam as instâncias do SQL Server.

### <a name="restoring-packages-that-were-previously-installed"></a>Restaurando os pacotes que foram instalados anteriormente

O utilitário de atualização que foi incluído com o Microsoft R Server 9.0.1, o utilitário não restaurou os pacotes originais ou componentes de R completamente, exigindo que o usuário executar o reparo da instância, se aplicam a todas as versões de serviço e, em seguida, reinicie a instância.

No entanto, a versão mais recente do utilitário atualização, para o Microsoft R Server 9.1.0, restaurará automaticamente os recursos de R originais. Portanto, você não precisa reinstalar os componentes de R ou patch novamente o servidor. No entanto, você ainda precisará instalar todos os pacotes R que talvez tenham sido adicionados após a instalação inicial.

Se você tiver usado as funções de gerenciamento de pacote para instalar e compartilhar o pacote, essa tarefa é muito mais fácil: você pode usar comandos de R para sincronizar os pacotes instalados no sistema de arquivos usando registros no banco de dados e vice-versa. Para obter mais informações, consulte [instalando e Gerenciando pacotes de R](installing-and-managing-r-packages.md)

### <a name="cannot-perform-upgrade-from-901"></a>Não é possível executar a atualização do 9.0.1

Se anteriormente você tiver atualizado uma instância do SQL Server 2016 R Services para 9.0.1, quando você executar o instalador de novo para o Microsoft R Server 9.1.0, exibirá uma lista de todas as instâncias válidas e, em seguida, por padrão, selecionar instâncias associadas anteriormente. Se você continuar, as instâncias associadas anteriormente serão desvinculadas. Como resultado, o 9.0.1 anteriores instalação é removida, incluindo as relacionadas a pacotes, mas a nova versão do Microsoft R Server (9.1.0) não está instalada.

Como alternativa, você pode modificar a instalação existente do servidor de R da seguinte maneira:
1. No painel de controle, abra **adicionar ou remover programas**.
2. Localize o Microsoft R Server e, em seguida, clique em **alteração/modificação**.
3. Quando o instalador é iniciado, selecione as instâncias que você deseja associar a 9.1.0.

### <a name="binding-or-unbinding-leaves-multiple-temporary-folders"></a>Associação ou desvincular deixa várias pastas temporárias

Às vezes, a associação e operações de desvinculação falharem Limpar pastas temporárias.
Se você encontrar pastas com um nome assim, você pode removê-lo após a conclusão da instalação:`R_SERVICES_<guid>`

> [!NOTE]
> Certifique-se de aguardar até que a instalação for concluída. Ele pode levar muito tempo para remover bibliotecas de R associados com uma versão e, em seguida, adicionar novas bibliotecas de R. Quando a operação for concluída, pastas temporárias serão removidas.

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

+ [Novidades no servidor de R](https://docs.microsoft.com/r-server/whats-new-in-r-server)

+ [R Server problemas conhecidos](https://docs.microsoft.com/r-server/resources-known-issues)

