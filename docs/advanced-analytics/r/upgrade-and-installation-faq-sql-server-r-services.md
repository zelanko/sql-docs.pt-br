---
title: Perguntas frequentes sobre atualização e instalação
description: Respostas para algumas perguntas comuns sobre a instalação de recursos de aprendizado de máquina no SQL Server.
ms.custom: seo-lt-2019
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/06/2019
ms.topic: conceptual
ms.author: davidph
author: dphansen
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 6357f98627842ab790b494cf1b4a1f9b2110ec9c
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "73727347"
---
# <a name="upgrade-and-installation-faq-for-sql-server-machine-learning-or-r-server"></a>Perguntas frequentes sobre atualização e instalação para o Machine Learning do SQL Server ou o Microsoft R Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este tópico fornece respostas para algumas perguntas comuns sobre a instalação de recursos de aprendizado de máquina no SQL Server. Ele também aborda perguntas comuns sobre atualizações.

+ Alguns problemas ocorrem apenas com atualizações de versões de pré-lançamento. Portanto, é recomendável que você identifique sua versão e edição antes de ler essas notas. Para obter informações sobre a versão, execute `@@VERSION` em uma consulta do SQL Server Management Studio.
+ Atualize para a versão mais atual ou a versão de serviço assim que possível para resolver problemas que foram corrigidos em versões recentes.

**Aplica-se a:** SQL Server 2016 R Services, Serviços de Machine Learning do SQL Server (no banco de dados)

## <a name="requirements-and-restrictions-on-older-versions-of-sql-server-2016"></a>Requisitos e restrições em versões mais antigas do SQL Server 2016 

Dependendo do build do SQL Server que você está instalando, algumas das limitações a seguir podem se aplicar:

- Em versões anteriores do SQL Server 2016 R Services, a notação 8dot3 era necessária na unidade que contém o diretório de trabalho. Se você instalou uma versão de pré-lançamento, a atualização para o SQL Server 2016 Service Pack 1 deve corrigir esse problema. Esse requisito não se aplica a versões posteriores ao SP1.

- Não é possível instalar o [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] em um cluster de failover no SQL Server 2016. No entanto, o SQL Server 2019 dá suporte a failover. Para obter mais informações, confira as [Novidades](../what-s-new-in-sql-server-machine-learning-services.md).

- EM uma VM do Azure, algumas configurações adicionais podem ser necessárias. Por exemplo, talvez seja necessário criar uma exceção de firewall para dar suporte ao acesso remoto.

- A instalação lado a lado com outra versão do R ou com outras versões do Revolution Analytics não tem suporte.

- Desabilite a verificação de vírus antes de iniciar a instalação. Após a conclusão da instalação, recomendamos suspender a verificação de vírus nas pastas usadas pelo [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]. Preferivelmente, suspenda a verificação em toda a árvore do [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)].

 - Instalando o Microsoft R Server em uma instância do SQL Server instalada no Windows Core. Na versão RTM do SQL Server 2016, havia um problema conhecido ao adicionar o Microsoft R Server a uma instância no Windows Server Core Edition. Esse problema foi corrigido. Se tiver esse problema, aplique a correção descrita no [KB3164398](https://support.microsoft.com/kb/3164398) para adicionar o recurso do R à instância existente no Windows Server Core. Para obter mais informações, consulte [Não é possível instalar o Microsoft R Server (Autônomo) em um sistema operacional Windows Server Core](https://support.microsoft.com/kb/3168691).


## <a name="offline-installation-of-machine-learning-components-for-a-localized-version-of-sql-server-2016"></a>Instalação offline de componentes de aprendizado de máquina para uma versão localizada do SQL Server 2016

As versões de lançamento antecipado do SQL Server 2016 falhavam ao instalar arquivos .cab específicos de localidade durante a instalação offline sem uma conexão com a Internet. Esse problema foi corrigido em versões posteriores, mas, se o instalador retornar uma mensagem informando que não pode instalar o idioma correto, você poderá editar o nome do arquivo para permitir que a instalação continue.

+ Edite manualmente o arquivo do instalador para garantir que o idioma correto esteja instalado. Por exemplo, para instalar a versão japonesa do SQL Server, altere o nome do arquivo de SRS_8.0.3.0_**1033**.cab para SRS_8.0.3.0_**1041**.cab.
+ O identificador de idioma usado para os componentes de aprendizado de máquina deve ser o mesmo que o do idioma de instalação do SQL Server; caso contrário, você não conseguirá concluir a instalação.

## <a name="pre-release-versions-support-policies-upgrade-and-known-issues"></a>Versões de pré-lançamento: políticas de suporte, atualização e problemas conhecidos

Não há mais suporte para novas instalações de nenhuma versão de pré-lançamento do [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]. Se estiver usando uma versão de pré-lançamento, atualize assim que possível.

Esta seção contém instruções detalhadas para cenários de atualização específicos.

### <a name="how-to-upgrade-sql-server"></a>Como atualizar o SQL Server

Você pode atualizar sua versão do SQL Server executando novamente o assistente de instalação.

+ [Atualizar o SQL Server](../../database-engine/install-windows/upgrade-sql-server.md)
+ [Atualizar o SQL Server usando o assistente de instalação](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)

Você pode atualizar apenas os componentes de aprendizado de máquina usando um processo chamado associação: 
+ [Usar SqlBindR para atualizar os componentes de aprendizado de máquina](../install/upgrade-r-and-python.md)

### <a name="end-of-support-for-in-place-upgrades-from-prerelease-versions"></a>Fim do suporte para atualizações in-loco de versões de pré-lançamento

Não há mais suporte para atualizações de versões de pré-lançamento do SQL Server 2016. Isso inclui o SQL Server 2016 CTP3, CTP3.1, CTP3.2, RC0 e RC1.

As versões a seguir foram instaladas com versões de pré-lançamento do SQL Server 2016.

| Versão | Build         |
|---------|---------------|
| CTP 3.0 | 13.0.xxx      |
| CTP 3.1 | 13.0.801.12   |
| CTP 3.2 | 13.0.900.73   |
| CTP 3.3 | 13.0.1000.281 |
| RC1     | 13.0.1200.242 |
| RC2     | 13.0.1300.275 |
| RC3     | 13.0.1400.361 |

Se tiver dúvidas sobre qual versão está usando, execute `@@VERSION` em uma consulta do SQL Server Management Studio.

De modo geral, o processo de atualização é o seguinte:

1. Fazer backup de scripts e dados.
2. Desinstalar a versão de pré-lançamento.
3. Instalar a versão de lançamento.

A desinstalação de uma versão de pré-lançamento dos componentes de aprendizado de máquina do SQL Server pode ser complexa e pode exigir a execução de um script especial. Contate o suporte técnico para obter ajuda.

###  <a name="bkmk_Uninstall"></a> Desinstalar antes de atualizar de uma versão anterior do Microsoft R Server

Se você tiver instalado uma versão de pré-lançamento do Microsoft R Server, será necessário desinstalá-la antes de atualizar para uma versão mais nova.

1.  No **Painel de Controle**, clique em **Adicionar/Remover Programas**e selecione `Microsoft SQL Server 2016 <version number>`.

2.  Na caixa de diálogo com opções para **Adicionar**, **Reparar**ou **Remover** componentes, selecione **Remover**.
  
3.  Na página **Selecionar Recursos** em **Recursos Compartilhados**, selecione **R Server (Autônomo)** . Clique em **Avançar**e em **Concluir** para desinstalar apenas os componentes selecionados.

## <a name="r-services-and-r-server-standalone-side-by-side-errors"></a>Erros do R Services e do R Server (autônomo) lado a lado 

Em versões anteriores do SQL Server 2016, a instalação do R Server (autônomo) e do R Services (no banco de dados) ao mesmo tempo às vezes fazia com que a instalação falhasse com uma mensagem de "acesso negado". Esse problema foi corrigido no Service Pack 1 para o SQL Server 2016.

Se você tiver encontrado esse erro e precisar atualizar esses recursos, execute uma instalação integrada do SQL Server 2016 com o SP1. Há duas maneiras de resolver o problema, sendo que ambas exigem desinstalar e reinstalar.

1. Desinstale o R Services (no banco de dados) e verifique se as contas de usuário do SQLRUserGroup foram removidas.

2. Reinicie o servidor e reinstale o R Server (autônomo).

3. Execute a instalação do SQL Server mais uma vez e, dessa vez, selecione **Adicionar Recursos ao SQL Server Existente**.

4. Escolha a instância e, em seguida, selecione a opção **R Services (no banco de dados)** para ser adicionada.

Se esse procedimento não resolver o problema, tente a seguinte solução alternativa:

1. Desinstale o R Services (no banco de dados) e o R Server (autônomo) ao mesmo tempo.

2. Remova as contas de usuário locais (SQLRUserGroup).

3. Reinicie o servidor.

4. Execute a instalação do SQL Server e adicione apenas o recurso do R Services (no banco de dados). Não selecione o **R Server (autônomo)** .

De modo geral, recomendamos que você não instale o R Services (no banco de dados) e o R Server (autônomo) no mesmo computador. No entanto, supondo que o servidor tenha capacidade suficiente, você pode descobrir que o R Server Autônomo pode ser útil como uma ferramenta de desenvolvimento. Outro cenário possível é que você precise usar os recursos de operacionalização do R Server, mas também queira acessar dados do SQL Server sem movimentação de dados.

## <a name="incompatible-version-of-r-client-and-r-server"></a>Versão incompatível do Cliente do R e R Server

Se você instalar o Microsoft R Client e usá-lo para executar o R em um contexto de computação remota do SQL Server, poderá receber um erro como este:

*Você está executando a versão 9.0.0 do Microsoft R Client em seu computador, que é incompatível com o Microsoft R Server versão 8.0.3. Baixe e instale uma versão compatível.*

No SQL Server 2016, era necessário que a versão do R que estava sendo executada no SQL Server R Services fosse exatamente a mesma das bibliotecas no Microsoft R Client. Esse requisito foi removido em versões posteriores. No entanto, é recomendável que você sempre obtenha as versões mais recentes dos componentes de aprendizado de máquina e instale todos os service packs. 

Se você tem uma versão anterior do Microsoft R Server e deseja assegurar a compatibilidade com o Microsoft R Client 9.0.0, é necessário instalar as atualizações descritas neste [artigo de suporte](https://support.microsoft.com/kb/3210262).


## <a name="installation-fails-with-error-only-one-revolution-enterprise-product-can-be-installed-at-a-time"></a>A instalação falha com o erro “Apenas um único produto do Revolution Enterprise pode ser instalado por vez”.

Você poderá receber esse erro se tiver uma instalação mais antiga dos produtos da Revolution Analytics ou uma versão de pré-lançamento do SQL Server R Services. É necessário desinstalar todas as versões anteriores antes de instalar uma versão mais nova do Microsoft R Server. Não há suporte para a instalação lado a lado com outras versões das ferramentas do Revolution Enterprise.

No entanto, há suporte para instalações lado a lado ao usar um R Server Autônomo com o [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] ou o SQL Server 2016.

## <a name="registry-cleanup-to-uninstall-older-components"></a>Limpeza do Registro para desinstalar componentes mais antigos

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

 [Serviços de Machine Learning do SQL Server (no banco de dados)](../r/sql-server-r-services.md)

 [Machine Learning Server do SQL Server (autônomo)](../r/r-server-standalone.md)
