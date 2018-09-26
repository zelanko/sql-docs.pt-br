---
title: Perguntas frequentes sobre atualização e instalação para o SQL Server Machine Learning | Microsoft Docs
ms.custom: sqlseattle
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/15/2018
ms.topic: conceptual
ms.author: heidist
author: HeidiSteen
manager: cgronlun
ms.openlocfilehash: 37cd28b895c66d6ddcf1517e79ef6bf4537e2a96
ms.sourcegitcommit: b7fd118a70a5da9bff25719a3d520ce993ea9def
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2018
ms.locfileid: "46712298"
---
# <a name="upgrade-and-installation-faq-for-sql-server-machine-learning-or-r-server"></a>Perguntas frequentes sobre atualização e instalação para o aprendizado de máquina do SQL Server ou Microsoft R Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este tópico fornece respostas para perguntas comuns sobre a instalação dos recursos do SQL Server de aprendizado de máquina. Ele também aborda dúvidas comuns sobre as atualizações.

+ Alguns problemas ocorrem apenas com as atualizações de versões de pré-lançamento. Portanto, é recomendável que você identificar sua versão e edição primeiro antes de ler estas notas. Para obter informações de versão, execute `@@VERSION` em uma consulta do SQL Server Management Studio.
+ Atualize para a versão mais recente ou a versão de serviço assim que possível para resolver quaisquer problemas que foram corrigidos em versões recentes.

**Aplica-se a:** SQL Server 2016 R Services, SQL Server 2017 serviços de Machine Learning (no banco de dados)

## <a name="requirements-and-restrictions-on-older-versions-of-sql-server-2016"></a>Requisitos e restrições em versões anteriores do SQL Server 2016 

Dependendo da compilação do SQL Server que você está instalando, algumas das limitações a seguir podem se aplicar:

- Em versões anteriores do SQL Server 2016 R Services, a notação 8dot3 era necessário na unidade que contém o diretório de trabalho. Se você instalou uma versão de pré-lançamento, a atualização para o SQL Server 2016 Service Pack 1 deve corrigir esse problema. Esse requisito não se aplica às versões após o SP1.

- Atualmente, não é possível instalar [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] em um cluster de failover. No entanto, visualização de 2019 do SQL Server oferece suporte a failover se você quiser avaliar esse capablity em um ambiente de teste. Para obter mais informações, consulte [What's New](../what-s-new-in-sql-server-machine-learning-services.md).

- Em uma VM do Azure, alguma configuração adicional pode ser necessária. Por exemplo, você talvez precise criar uma exceção de firewall para dar suporte a acesso remoto.

- Não há suporte para a instalação lado a lado com outra versão do R ou com outras versões do Revolution Analytics.

- Desabilite o antivírus antes de iniciar a instalação. Após a instalação for concluída, é recomendável suspender a verificação de vírus nas pastas usadas pelo [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]. Preferencialmente, suspender a verificação em todo o [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] árvore.

 - Instalando o Microsoft R Server em uma instância do SQL Server instalada no núcleo do Windows. Na versão RTM do SQL Server 2016, houve um problema conhecido ao adicionar o Microsoft R Server a uma instância no Windows Server Core edition. Esse problema foi corrigido. Se você encontrar esse problema, você pode aplicar a correção descrita no [KB3164398](https://support.microsoft.com/kb/3164398) para adicionar o recurso do R para a instância existente no Windows Server Core. Para obter mais informações, consulte [Não é possível instalar o Microsoft R Server (Autônomo) em um sistema operacional Windows Server Core](https://support.microsoft.com/kb/3168691).


## <a name="offline-installation-of-machine-learning-components-for-a-localized-version-of-sql-server-2016"></a>Instalação offline dos componentes de aprendizado de máquina para uma versão localizada do SQL Server 2016

Versões de versão antecipada do SQL Server 2016 não conseguiu instalar arquivos. cab de específica de localidade durante a instalação offline sem uma conexão de internet. Esse problema foi corrigido nas versões posteriores, mas se o instalador retornar uma mensagem informando que não é possível instalar o idioma correto, você pode editar o nome do arquivo para permitir que a instalação continuar.

+ Edite manualmente o arquivo do instalador para garantir que o idioma correto está instalado. Por exemplo, para instalar a versão japonesa do SQL Server, você alteraria o nome do arquivo de SRS_8.0.3.0_**1033**. cab para SRS_8.0.3.0_**1041**. cab.
+ O identificador de idioma usado para os componentes de aprendizado de máquina deve ser o mesmo que o idioma da instalação do SQL Server, ou você não pode concluir a instalação.

## <a name="pre-release-versions-support-policies-upgrade-and-known-issues"></a>Versões de pré-lançamento: suporte a políticas, atualização e problemas conhecidos

Novas instalações de qualquer versão de pré-lançamento do [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] não é mais suportada. Se você estiver usando uma versão de pré-lançamento, a atualização assim que possível.

Esta seção contém instruções detalhadas para cenários de atualização específicos.

### <a name="how-to-upgrade-sql-server"></a>Como atualizar o SQL Server

Você pode atualizar sua versão do SQL Server ao executar novamente o Assistente de instalação.

+ [Atualizar o SQL Server](../../database-engine/install-windows/upgrade-sql-server.md)
+ [Atualize o SQL Server usando o Assistente de instalação](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)

Você pode atualizar apenas a componentes usando um processo chamado associação de aprendizado de máquina: 
+ [Usar o SqlBindR para atualizar os componentes de aprendizado de máquina](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)

### <a name="end-of-support-for-in-place-upgrades-from-prerelease-versions"></a>Fim do suporte para atualizações in-loco das versões de pré-lançamento

Não há suporte para atualizações de versões de pré-lançamento do SQL Server 2016. Isso inclui o SQL Server 2016 CTP3, CTP3.1, CTP3.2, RC0 ou RC1.

As seguintes versões foram instaladas com as versões de pré-lançamento do SQL Server 2016.

| Versão | Compilação         |
|---------|---------------|
| CTP 3.0 | 13.0.xxx      |
| CTP 3.1 | 13.0.801.12   |
| CTP 3.2 | 13.0.900.73   |
| CTP 3.3 | 13.0.1000.281 |
| RC1     | 13.0.1200.242 |
| RC2     | 13.0.1300.275 |
| RC3     | 13.0.1400.361 |

Se você tiver alguma dúvida sobre qual versão você está usando, execute `@@VERSION` em uma consulta do SQL Server Management Studio.

Em geral, o processo de atualização é da seguinte maneira:

1. Fazer backup de dados e scripts.
2. Desinstale a versão de pré-lançamento.
3. Instale uma versão de lançamento.

Desinstalar uma versão de pré-lançamento do SQL Server componentes de aprendizado de máquina podem ser complexos e pode exigir a execução de um script especial. Contate o suporte técnico para obter ajuda.

###  <a name="bkmk_Uninstall"></a> Desinstalar antes da atualização de uma versão anterior do Microsoft R Server

Se você tiver instalado uma versão de pré-lançamento do Microsoft R Server, será necessário desinstalá-la antes de atualizar para uma versão mais nova.

1.  No **Painel de Controle**, clique em **Adicionar/Remover Programas**e selecione `Microsoft SQL Server 2016 <version number>`.

2.  Na caixa de diálogo com opções para **Adicionar**, **Reparar**ou **Remover** componentes, selecione **Remover**.
  
3.  Na página **Selecionar Recursos** em **Recursos Compartilhados**, selecione **R Server (Autônomo)**. Clique em **Avançar**e em **Concluir** para desinstalar apenas os componentes selecionados.

## <a name="r-services-and-r-server-standalone-side-by-side-errors"></a>Serviços de R e erros de lado a lado do R Server (autônomo) 

Em versões anteriores do SQL Server 2016, a instalação do R Server (autônomo) e do R Services (no banco de dados) ao mesmo tempo, às vezes, causou falha com uma mensagem de "acesso negado" na instalação. Esse problema foi corrigido no Service Pack 1 para SQL Server 2016.

Se você encontrou este erro e precisa atualizar esses recursos, execute uma instalação integrada do SQL Server 2016 com SP1. Há duas maneiras de resolver o problema, ambas exigem que a desinstalação e reinstalação.

1. Desinstale o R Services (no banco de dados) e verifique se que as contas de usuário para SQLRUserGroup são removidas.

2. Reinicie o servidor e, em seguida, reinstale o Microsoft R Server (autônomo).

3. Uma vez de execução do SQL Server instalação mais e desta vez selecione **adicionar recursos ao SQL Server existente**.

4. Escolha a instância e, em seguida, selecione a **R Services (no banco de dados)** opção para adicionar.

Se esse procedimento não conseguir resolver o problema, experimente a seguinte solução alternativa:

1. Desinstale o R Services (no banco de dados) e o R Server (autônomo) ao mesmo tempo.

2. Remova as contas de usuário local (SQLRUserGroup).

3. Reinicie o servidor.

4. Execute a instalação do SQL Server e adicionar somente o recurso R Services (no banco de dados). Não marque **R Server (autônomo)**.

Em geral, é recomendável que você não instalar o R Services (no banco de dados) e o R Server (autônomo) no mesmo computador. No entanto, supondo que o servidor tem capacidade suficiente, você pode achar que r Server autônomo pode ser útil como uma ferramenta de desenvolvimento. Outro cenário possível é que você precisa usar os recursos de operacionalização do R Server, mas também querem acessar dados do SQL Server sem a movimentação de dados.

## <a name="incompatible-version-of-r-client-and-r-server"></a>Versão incompatível do Cliente do R e R Server

Se você instala o Microsoft R Client e usá-lo para executar o R no contexto de computação remoto do SQL Server, você poderá receber um erro como este:

*Você está executando a versão 9.0.0 do cliente do Microsoft R em seu computador, o que é incompatível com o Microsoft R Server versão 8.0.3. Baixe e instale uma versão compatível.*

No SQL Server 2016, era necessário que a versão do R que estava em execução no SQL Server R Services ser exatamente o mesmo que as bibliotecas de cliente do Microsoft R. Esse requisito foi removido em versões posteriores. No entanto, é recomendável que você sempre obtenha as versões mais recentes dos componentes de aprendizado de máquina e instale todos os service packs. 

Se você tiver uma versão anterior do Microsoft R Server e precisa garantir a compatibilidade com o cliente do Microsoft R 9.0.0, instalar as atualizações que são descritas neste [artigo de suporte](https://support.microsoft.com/kb/3210262).


## <a name="installation-fails-with-error-only-one-revolution-enterprise-product-can-be-installed-at-a-time"></a>A instalação falha com o erro “Apenas um único produto do Revolution Enterprise pode ser instalado por vez”.

Você poderá receber esse erro se tiver uma instalação mais antiga dos produtos da Revolution Analytics ou uma versão de pré-lançamento do SQL Server R Services. É necessário desinstalar todas as versões anteriores antes de instalar uma versão mais nova do Microsoft R Server. Não há suporte para a instalação lado a lado com outras versões das ferramentas do Revolution Enterprise.

No entanto, há suporte para instalações lado a lado ao usar um R Server Autônomo com o [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] ou o SQL Server 2016.

## <a name="registry-cleanup-to-uninstall-older-components"></a>Limpeza de registro para desinstalar os componentes mais antigos

Se você tiver problemas ao remover uma versão mais antiga, talvez será necessário editar o Registro para remover as chaves relacionadas.

> [!IMPORTANT]
> Esse problema se aplicará somente se você tiver instalado uma versão de pré-lançamento do Microsoft R Server ou uma versão CTP do SQL Server 2016 R Services.
  
1. Abra o Registro do Windows e localize esta chave: `HKLM\Software\Microsoft\Windows\CurrentVersion\Uninstall`.
2. Exclua as seguintes entradas, se houver, e se a chave contiver apenas o valor `sEstimatedSize2`:
  
    -   E0B2C29E-B8FC-490B-A043-2CAE75634972        (para o 8.0.2)
  
    -   46695879-954E-4072-9D32-1CC84D4158F4        (para o 8.0.1)
  
    -   2DF16DF8-A2DB-4EC6-808B-CB5A302DA91B        (para o 8.0.0)
  
    -   5A2A1571-B8CD-4AAF-9303-8DF463DABE5A        (para o 7.5.0)

## <a name="see-also"></a>Confira também

 [(No banco de dados) de serviços de aprendizado de máquina do SQL Server](../r/sql-server-r-services.md)

 [SQL Server Machine Learning Server (autônomo)](../r/r-server-standalone.md)
