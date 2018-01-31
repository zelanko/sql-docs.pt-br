---
title: "Etapa 1: criando pastas de trabalho e variáveis de ambiente | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: tutorial
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: 45091ba2-ea3d-4399-9814-489d812b42cc
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 06b762b3411f13eff291746467d9217487e94655
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="lesson-1-1---creating-working-folders-and-environment-variables"></a>Lição 1-1 – criar pastas de trabalho e variáveis de ambiente
Nesta tarefa, você criará a pasta de trabalho (C:\DeploymentTutorial) e as novas variáveis de ambiente do sistema (`DataTransfer` e `LoadXMLData`), que serão usadas em tarefas posteriores do tutorial.  
  
A pasta de trabalho está na raiz da unidade C. Se você precisar usar uma unidade ou um local diferente, poderá fazer isso. Porém, será necessário anotar esse local e usá-lo sempre que o tutorial se referir ao local da pasta de trabalho DeploymentTutorial.  
  
Em uma lição posterior, você implantará os pacotes salvos no sistema de arquivos na tabela sysssispackages no banco de dados msdb do[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . O ideal seria implantar os pacotes [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] em um computador diferente. Se isso não for possível, você ainda poderá aprender muito fazendo esse tutorial para implantar os pacotes em uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que estiver no computador local. As variáveis de ambiente usadas nos computadores local e de destino têm os mesmos nomes de variável, mas são armazenados valores diferentes nas variáveis. Por exemplo, no computador local, o valor da variável do ambiente `DataTransfer` se refere à pasta C:\DeploymentTutorial, enquanto que no computador de destino a variável do ambiente `DataTransfer` se refere à pasta C:\DeploymentTutorialInstall.  
  
Se você planejar fazer a implantação no computador local, precisará criar apenas um conjunto de variáveis de ambiente; porém, precisará atualizar o valor das variáveis de ambiente para um valor apropriado antes de fazer a implantação local.  
  
Se você planeja implantar os pacotes em um computador diferente, deverá criar dois conjuntos de variáveis de ambiente: um conjunto para o computador local e outro para o computador de destino. Você pode criar agora apenas as variáveis para o computador original, e criar as variáveis para o computador de destino mais tarde, mas deve ter tanto a pasta, quanto as variáveis de ambiente disponíveis no computador de destino antes de instalar os pacotes nesse computador.  
  
### <a name="to-create-the-local-working-folder"></a>Para criar a pasta de trabalho local  
  
1.  Clique com o botão direito do mouse no menu Iniciar e clique em Explorar.  
  
2.  Clique em **Disco Local (C:)**.  
  
3.  No menu **Arquivo** , aponte para **Novo**e clique em **Pasta**.  
  
4.  Renomeie a Nova Pasta como **DeploymentTutorial**.  
  
### <a name="to-create-local-environment-variables"></a>Para criar variáveis locais do ambiente  
  
1.  No menu **Iniciar** , clique em **Painel de Controle**.  
  
2.  No Painel de Controle, clique duas vezes em **Sistema**.  
  
3.  Na caixa de diálogo **Propriedades do Sistema** , clique na guia **Avançado** e clique em **Variáveis de Ambiente**.  
  
4.  Na caixa de diálogo **Variáveis de Ambiente** , no quadro **Variáveis do sistema** , clique em **Novo**.  
  
5.  Na caixa de diálogo **Nova Variável do Sistema** , digite **DataTransfer** na caixa **Nome da variável** e **C:\DeploymentTutorial\datatransferconfig.dtsconfig** na caixa **Valor da variável** .  
  
6.  Clique em **OK**.  
  
7.  Clique novamente em **Novo** e digite **LoadXMLData** na caixa **Nome da variável** e **C:\DeploymentTutorial\loadxmldataconfig.dtsconfig** na caixa **Valor da variável** .  
  
8.  Clique em **OK** para sair da caixa de diálogo **Variáveis de Ambiente** .  
  
9. Clique em **OK** para sair da caixa de diálogo **Propriedades do Sistema** .  
  
10. Opcionalmente, reinicie o seu computador. Se você não reiniciar o seu computador, o nome da nova variável não será exibido no Assistente de Configuração de Pacotes, mas você ainda poderá usá-lo.  
  
### <a name="to-create-destination-environment-variables"></a>Para criar variáveis de ambiente de destino  
  
1.  No menu **Iniciar** , clique em **Painel de Controle**.  
  
2.  No Painel de Controle, clique duas vezes em **Sistema**.  
  
3.  Na caixa de diálogo **Propriedades do Sistema** , clique na guia **Avançado** e clique em **Variáveis de Ambiente**.  
  
4.  Na caixa de diálogo **Variáveis de Ambiente** , no quadro **Variáveis do sistema** , clique em **Novo**.  
  
5.  Na caixa de diálogo **Novas Variáveis do Sistema** , digite **DataTransfer** na caixa **Nome da variável** e **C:\DeploymentTutorialInstall\datatransferconfig.dtsconfig** na caixa **Valor da variável** .  
  
6.  Clique em **OK**.  
  
7.  Clique novamente em **Novo** e digite **LoadXMLData** na caixa **Nome da variável** e **C:\DeploymentTutorialInstall\loadxmldataconfig.dtsconfig** na caixa **Valor da variável** .  
  
8.  Clique em **OK** para sair da caixa de diálogo **Variáveis de Ambiente** .  
  
9. Clique em **OK** para sair da caixa de diálogo **Propriedades do Sistema** .  
  
10. Opcionalmente, reinicie o seu computador.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
[Etapa 2: Criando o projeto de implantação](../integration-services/lesson-1-2-creating-the-deployment-project.md)  
  
  
  
