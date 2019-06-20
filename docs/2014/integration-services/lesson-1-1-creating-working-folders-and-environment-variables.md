---
title: 'Etapa 1: Criando pastas de trabalho e variáveis de ambiente | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 45091ba2-ea3d-4399-9814-489d812b42cc
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b58da11d973d169a0372e59c7e8d7e174e3cf789
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62767648"
---
# <a name="step-1-creating-working-folders-and-environment-variables"></a>Etapa 1: Criar pastas de trabalho e variáveis de ambiente
  Nesta tarefa, você criará a pasta de trabalho (C:\DeploymentTutorial) e as novas variáveis de ambiente do sistema (`DataTransfer` e `LoadXMLData`), que serão usadas em tarefas posteriores do tutorial.  
  
 A pasta de trabalho está na raiz da unidade C. Se você precisar usar uma unidade ou um local diferente, poderá fazer isso. Porém, será necessário anotar esse local e usá-lo sempre que o tutorial se referir ao local da pasta de trabalho DeploymentTutorial.  
  
 Em uma lição posterior, você implantará os pacotes salvos no sistema de arquivos na tabela sysssispackages no banco de dados msdb do[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . O ideal seria implantar os pacotes [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] em um computador diferente. Se isso não for possível, você ainda poderá aprender muito fazendo esse tutorial para implantar os pacotes em uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que estiver no computador local. As variáveis de ambiente usadas nos computadores local e de destino têm os mesmos nomes de variável, mas são armazenados valores diferentes nas variáveis. Por exemplo, no computador local, o valor da variável do ambiente `DataTransfer` se refere à pasta C:\DeploymentTutorial, enquanto que no computador de destino a variável do ambiente `DataTransfer` se refere à pasta C:\DeploymentTutorialInstall.  
  
 Se você planejar fazer a implantação no computador local, precisará criar apenas um conjunto de variáveis de ambiente; porém, precisará atualizar o valor das variáveis de ambiente para um valor apropriado antes de fazer a implantação local.  
  
 Se você planeja implantar os pacotes em um computador diferente, deverá criar dois conjuntos de variáveis de ambiente: um conjunto para o computador local e outro para o computador de destino. Você pode criar agora apenas as variáveis para o computador original, e criar as variáveis para o computador de destino mais tarde, mas deve ter tanto a pasta, quanto as variáveis de ambiente disponíveis no computador de destino antes de instalar os pacotes nesse computador.  
  
### <a name="to-create-the-local-working-folder"></a>Para criar a pasta de trabalho local  
  
1.  Clique com o botão direito do mouse no menu Iniciar e clique em Explorar.  
  
2.  Clique em **Disco Local (C:)**.  
  
3.  No menu **Arquivo** , aponte para **Novo**e clique em **Pasta**.  
  
4.  Renomeie a nova pasta como `DeploymentTutorial`.  
  
### <a name="to-create-local-environment-variables"></a>Para criar variáveis locais do ambiente  
  
1.  No menu **Iniciar** , clique em **Painel de Controle**.  
  
2.  No Painel de Controle, clique duas vezes em **Sistema**.  
  
3.  Na caixa de diálogo **Propriedades do Sistema** , clique na guia **Avançado** e clique em **Variáveis de Ambiente**.  
  
4.  Na caixa de diálogo **Variáveis de Ambiente** , no quadro **Variáveis do sistema** , clique em **Novo**.  
  
5.  No **nova variável do sistema** caixa de diálogo, digite `DataTransfer` no **nome da variável** caixa, e `C:\DeploymentTutorial\datatransferconfig.dtsconfig` no **valor da variável** caixa.  
  
6.  Clique em **OK**.  
  
7.  Clique em **New** novamente e o tipo `LoadXMLData` no **nome da variável** caixa, e `C:\DeploymentTutorial\loadxmldataconfig.dtsconfig` no **valor da variável** caixa.  
  
8.  Clique em **OK** para sair da caixa de diálogo **Variáveis de Ambiente** .  
  
9. Clique em **OK** para sair da caixa de diálogo **Propriedades do Sistema** .  
  
10. Opcionalmente, reinicie o seu computador. Se você não reiniciar o seu computador, o nome da nova variável não será exibido no Assistente de Configuração de Pacotes, mas você ainda poderá usá-lo.  
  
### <a name="to-create-destination-environment-variables"></a>Para criar variáveis de ambiente de destino  
  
1.  No menu **Iniciar** , clique em **Painel de Controle**.  
  
2.  No Painel de Controle, clique duas vezes em **Sistema**.  
  
3.  Na caixa de diálogo **Propriedades do Sistema** , clique na guia **Avançado** e clique em **Variáveis de Ambiente**.  
  
4.  Na caixa de diálogo **Variáveis de Ambiente** , no quadro **Variáveis do sistema** , clique em **Novo**.  
  
5.  No **novas variáveis de sistema** caixa de diálogo, digite `DataTransfer` no **nome da variável** caixa, e `C:\DeploymentTutorialInstall\datatransferconfig.dtsconfig` no **valor da variável** caixa.  
  
6.  Clique em **OK**.  
  
7.  Clique em **New** novamente e o tipo `LoadXMLData` no **nome da variável** caixa, e `C:\DeploymentTutorialInstall\loadxmldataconfig.dtsconfig` no **valor da variável** caixa.  
  
8.  Clique em **OK** para sair da caixa de diálogo **Variáveis de Ambiente** .  
  
9. Clique em **OK** para sair da caixa de diálogo **Propriedades do Sistema** .  
  
10. Opcionalmente, reinicie o seu computador.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Etapa 2: Criando o projeto de implantação](../integration-services/lesson-1-2-creating-the-deployment-project.md)  
  
![Ícone do Integration Services (pequeno)](media/dts-16.gif "ícone do Integration Services (pequeno)")**mantenha-se para cima até o momento com o Integration Services**<br /> Para obter os downloads, artigos, exemplos e vídeos mais recentes da Microsoft, assim como soluções selecionadas pela comunidade, visite a página do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] no MSDN:<br /><br /> [Visite a página do Integration Services no MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para receber uma notificação automática dessas atualizações, assine os RSS feeds disponíveis na página.  
  
  
