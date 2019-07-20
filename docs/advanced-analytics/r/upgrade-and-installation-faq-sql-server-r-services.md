---
title: Perguntas frequentes sobre atualização e instalação (FAQ)
ms.custom: sqlseattle
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
ms.author: davidph
author: dphansen
ms.openlocfilehash: 71a6149f1d89a4a1df114f376c250c203a8721cf
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68344913"
---
# <a name="upgrade-and-installation-faq-for-sql-server-machine-learning-or-r-server"></a>Perguntas frequentes sobre atualização e instalação para SQL Server Machine Learning ou R Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este tópico fornece respostas para algumas perguntas comuns sobre a instalação de recursos de aprendizado de máquina no SQL Server. Ele também aborda perguntas comuns sobre atualizações.

+ Alguns problemas ocorrem apenas com atualizações de versões de pré-lançamento. Portanto, é recomendável que você identifique sua versão e edição primeiro antes de ler essas notas. Para obter informações de versão, `@@VERSION` execute em uma consulta de SQL Server Management Studio.
+ Atualize para a versão mais atual ou a versão de serviço assim que possível para resolver os problemas que foram corrigidos em versões recentes.

**Aplica-se a:** SQL Server 2016 R Services, SQL Server 2017 Serviços de Machine Learning (no banco de dados)

## <a name="requirements-and-restrictions-on-older-versions-of-sql-server-2016"></a>Requisitos e restrições em versões mais antigas do SQL Server 2016 

Dependendo da compilação de SQL Server que você está instalando, algumas das limitações a seguir podem se aplicar:

- Nas versões anteriores do SQL Server R Services 2016, a notação 8dot3 era necessária na unidade que contém o diretório de trabalho. Se você instalou uma versão de pré-lançamento, a atualização para SQL Server 2016 Service Pack 1 deve corrigir esse problema. Esse requisito não se aplica a versões posteriores ao SP1.

- No momento, não é [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] possível instalar o em um cluster de failover. No entanto, SQL Server versão prévia do 2019 fornecerá suporte a failover se você quiser avaliar esse recurso em um ambiente de teste. Para obter mais informações, consulte [o que há de novo](../what-s-new-in-sql-server-machine-learning-services.md).

- Em uma VM do Azure, algumas configurações adicionais podem ser necessárias. Por exemplo, talvez seja necessário criar uma exceção de firewall para dar suporte ao acesso remoto.

- Não há suporte para a instalação lado a lado com outra versão do R ou com outras versões da análise de revolução.

- Desabilite a verificação de vírus antes de iniciar a instalação. Após a conclusão da instalação, recomendamos suspender a verificação de vírus nas pastas [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]usadas pelo. Preferivelmente, suspenda a verificação [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] em toda a árvore.

 - Instalação do Microsoft R Server em uma instância do SQL Server instalada no Windows Core. Na versão RTM do SQL Server 2016, houve um problema conhecido ao adicionar Microsoft R Server a uma instância no Windows Server Core Edition. Esse problema foi corrigido. Se você encontrar esse problema, poderá aplicar a correção descrita em [KB3164398](https://support.microsoft.com/kb/3164398) para adicionar o recurso de R à instância existente no Windows Server Core. Para obter mais informações, consulte [Não é possível instalar o Microsoft R Server (Autônomo) em um sistema operacional Windows Server Core](https://support.microsoft.com/kb/3168691).


## <a name="offline-installation-of-machine-learning-components-for-a-localized-version-of-sql-server-2016"></a>Instalação offline de componentes do Machine Learning para uma versão localizada do SQL Server 2016

As versões de lançamento antecipado do SQL Server 2016 falharam ao instalar arquivos. cab específicos da localidade durante a instalação offline sem uma conexão com a Internet. Esse problema foi corrigido em versões posteriores, mas se o instalador retornar uma mensagem informando que não pode instalar o idioma correto, você poderá editar o nome do arquivo para permitir que a instalação continue.

+ Edite manualmente o arquivo do instalador para garantir que o idioma correto esteja instalado. Por exemplo, para instalar a versão japonesa do SQL Server, você alteraria o nome do arquivo de SRS_ 8.0.3.0 _**1033**. cab para srs_ 8.0.3.0 _**1041**. cab.
+ O identificador de idioma usado para os componentes de Machine Learning deve ser o mesmo que o idioma de instalação do SQL Server ou não é possível concluir a instalação.

## <a name="pre-release-versions-support-policies-upgrade-and-known-issues"></a>Versões de pré-lançamento: suporte a políticas, atualização e problemas conhecidos

Novas instalações de qualquer versão de pré-lançamento do [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] não são mais suportadas. Se você estiver usando uma versão de pré-lançamento, atualize assim que possível.

Esta seção contém instruções detalhadas para cenários de atualização específicos.

### <a name="how-to-upgrade-sql-server"></a>Como atualizar SQL Server

Você pode atualizar sua versão do SQL Server executando novamente o assistente de instalação.

+ [Atualizar o SQL Server](../../database-engine/install-windows/upgrade-sql-server.md)
+ [Atualizar SQL Server usando o assistente de instalação](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)

Você pode atualizar apenas os componentes do Machine Learning usando um processo chamado associação: 
+ [Usar o sqlbindr para atualizar os componentes do Machine Learning](../install/upgrade-r-and-python.md)

### <a name="end-of-support-for-in-place-upgrades-from-prerelease-versions"></a>Fim do suporte para atualizações in-loco de versões de pré-lançamento

Não há mais suporte para atualizações de versões de pré-lançamento do SQL Server 2016. Isso inclui SQL Server 2016 CTP3, CTP 3.1, CTP 3.2, RC0 ou RC1.

As versões a seguir foram instaladas com versões de pré-lançamento do SQL Server 2016.

| Version | Build         |
|---------|---------------|
| CTP 3.0 | 13.0.xxx      |
| CTP 3.1 | 13.0.801.12   |
| CTP 3.2 | 13.0.900.73   |
| CTP 3.3 | 13.0.1000.281 |
| RC1     | 13.0.1200.242 |
| RC2     | 13.0.1300.275 |
| RC3     | 13.0.1400.361 |

Se você tiver alguma dúvida sobre qual versão está usando, execute `@@VERSION` em uma consulta de SQL Server Management Studio.

Em geral, o processo de atualização é o seguinte:

1. Fazer backup de scripts e dados.
2. Desinstale a versão de pré-lançamento.
3. Instale uma versão de lançamento.

A desinstalação de uma versão de pré-lançamento do SQL Server componentes de aprendizado de máquina pode ser complexa e pode exigir a execução de um script especial. Contate o suporte técnico para obter ajuda.

###  <a name="bkmk_Uninstall"></a>Desinstalar antes de atualizar de uma versão mais antiga do Microsoft R Server

Se você tiver instalado uma versão de pré-lançamento do Microsoft R Server, será necessário desinstalá-la antes de atualizar para uma versão mais nova.

1.  No **Painel de Controle**, clique em **Adicionar/Remover Programas**e selecione `Microsoft SQL Server 2016 <version number>`.

2.  Na caixa de diálogo com opções para **Adicionar**, **Reparar**ou **Remover** componentes, selecione **Remover**.
  
3.  Na página **Selecionar Recursos** em **Recursos Compartilhados**, selecione **R Server (Autônomo)** . Clique em **Avançar**e em **Concluir** para desinstalar apenas os componentes selecionados.

## <a name="r-services-and-r-server-standalone-side-by-side-errors"></a>Erros lado a lado do r Services e do R Server (autônomo) 

Em versões anteriores do SQL Server 2016, a instalação do R Server (autônomo) e do R Services (no banco de dados) às vezes fazia com que a instalação falhasse com uma mensagem de "acesso negado". Esse problema foi corrigido no Service Pack 1 para SQL Server 2016.

Se você encontrou esse erro e precisa atualizar esses recursos, execute uma instalação integrada do SQL Server 2016 com SP1. Há duas maneiras de resolver o problema, e ambos exigem desinstalar e reinstalar o.

1. Desinstale o R Services (no banco de dados) e verifique se as contas de usuário para SQLRUserGroup foram removidas.

2. Reinicie o servidor e reinstale o R Server (autônomo).

3. Execute SQL Server configuração mais uma vez e, desta vez, selecione **Adicionar recursos ao SQL Server existente**.

4. Escolha a instância e, em seguida, selecione a opção **R Services (no banco de dados)** a ser adicionada.

Se esse procedimento não resolver o problema, tente a seguinte solução alternativa:

1. Desinstale o R Services (no banco de dados) e o R Server (autônomo) ao mesmo tempo.

2. Remova as contas de usuário local (SQLRUserGroup).

3. Reinicie o servidor.

4. Execute SQL Server instalação e adicione apenas o recurso R Services (no banco de dados). Não selecione o **servidor R (autônomo)** .

Em geral, recomendamos que você não instale o R Services (no banco de dados) e o servidor R (autônomo) no mesmo computador. No entanto, supondo que o servidor tenha capacidade suficiente, você pode achar que o R Server autônomo pode ser útil como uma ferramenta de desenvolvimento. Outro cenário possível é que você precise usar os recursos de operacionalização do R Server, mas também deseja acessar dados de SQL Server sem movimentação de dados.

## <a name="incompatible-version-of-r-client-and-r-server"></a>Versão incompatível do Cliente do R e R Server

Se você instalar Microsoft R Client e usá-lo para executar o R em um contexto de computação de SQL Server remota, poderá obter um erro como este:

*Você está executando a versão 9.0.0 do Microsoft R Client em seu computador, que é incompatível com o Microsoft R Server versão 8.0.3. Baixe e instale uma versão compatível.*

No SQL Server 2016, era necessário que a versão do R que estava sendo executada no SQL Server R Services fosse exatamente a mesma das bibliotecas em Microsoft R Client. Esse requisito foi removido em versões posteriores. No entanto, é recomendável que você sempre obtenha as versões mais recentes dos componentes do Machine Learning e instale todos os Service Packs. 

Se você tiver uma versão anterior do Microsoft R Server e precisar garantir a compatibilidade com Microsoft R Client 9.0.0, instale as atualizações descritas neste artigo de [suporte](https://support.microsoft.com/kb/3210262).


## <a name="installation-fails-with-error-only-one-revolution-enterprise-product-can-be-installed-at-a-time"></a>A instalação falha com o erro “Apenas um único produto do Revolution Enterprise pode ser instalado por vez”.

Você poderá receber esse erro se tiver uma instalação mais antiga dos produtos da Revolution Analytics ou uma versão de pré-lançamento do SQL Server R Services. É necessário desinstalar todas as versões anteriores antes de instalar uma versão mais nova do Microsoft R Server. Não há suporte para a instalação lado a lado com outras versões das ferramentas do Revolution Enterprise.

No entanto, há suporte para instalações lado a lado ao usar um R Server Autônomo com o [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] ou o SQL Server 2016.

## <a name="registry-cleanup-to-uninstall-older-components"></a>Limpeza do registro para desinstalar componentes mais antigos

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

 [SQL Server Serviços de Machine Learning (no banco de dados)](../r/sql-server-r-services.md)

 [SQL Server Machine Learning Server (autônomo)](../r/r-server-standalone.md)
