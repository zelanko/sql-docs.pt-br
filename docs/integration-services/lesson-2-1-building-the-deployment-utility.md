---
title: "Etapa 1: Compilando o utilitário de implantação | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: 1ff4dcff-89b3-4b99-a725-5f7963e98abf
caps.latest.revision: 21
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 227ebbba4190ff05ebdc04f988beafec4edc8a37
ms.contentlocale: pt-br
ms.lasthandoff: 09/26/2017

---
# <a name="lesson-2-1---building-the-deployment-utility"></a>Lição 2-1-criar o utilitário de implantação
Nesta tarefa, você configurará e compilará um utilitário de implantação para o projeto do Tutorial de Implantação.  
  
Antes de compilar o utilitário de implantação, você deve modificar as propriedades do projeto do Tutorial de Implantação. Você usará a caixa de diálogo **Páginas de Propriedades do Tutorial de Implantação** para configurar essas propriedades. Nesta caixa de diálogo, você deve habilitar o recurso para atualizar configurações durante a implantação e especificar que o processo de compilação gera um utilitário de implantação. Depois que você definir as propriedades, o projeto será compilado.  
  
[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] fornece um conjunto de janelas que você pode usar para depurar pacotes. Você pode visualizar mensagens de erro, de avisos e de informações, pode rastrear o status de pacotes em tempo de execução, ou pode visualizar o progresso e os resultados dos processos de compilação. Nesta lição, você usará a janela Saída para visualizar o progresso e os resultados da compilação do utilitário de implantação.  
  
### <a name="to-set-the-deployment-utility-properties"></a>Para definir as propriedades do utilitário de implantação  
  
1.  Se o [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] ainda não estiver aberto, clique em **Iniciar**, aponte para **Todos os Programas**, **Microsoft SQL Server**e clique em **Business Intelligence Development Studio**.  
  
2.  No menu **Arquivo** , clique em **Abrir**, em **Projeto/Solução**, clique na pasta **Tutorial de Implantação** , clique em **Abrir**e clique duas vezes em **Deployment Tutorial.sln**.  
  
3.  No Gerenciador de Soluções, clique com o botão direito do mouse em Tutorial de Implantação e clique em **Propriedades**.  
  
4.  Na caixa de diálogo **Páginas de Propriedades do Tutorial de Implantação** , expanda Propriedades de Configurações e clique em Utilitário de Implantação.  
  
5.  No painel direito da caixa de diálogo **Páginas de Propriedades do Tutorial de Implantação** , verifique se a opção **AllowConfigurationChanges** está definida como **true**, defina **CreateDeploymentUtility** como **true**e, opcionalmente, atualize o valor padrão de **DeploymentOutputPath**.  
  
6.  Clique em **OK**.  
  
### <a name="to-build-the-deployment-utility"></a>Para compilar o utilitário de implantação  
  
1.  No Gerenciador de Soluções, clique em **Tutorial de Implantação**.  
  
2.  No menu **Exibir** , clique em **Saída**. Por padrão, a janela Saída está localizada no canto esquerdo inferior do [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
3.  No menu **Criar** , clique em **Criar Tutorial de Implantação**.  
  
4.  Na janela Saída, verifique as seguintes informações:  
  
    Compilação iniciada: Projeto do SQL Integration Services: Incremental ...  
  
    Criando utilitário de implantação...  
  
    Utilitário de implantação criado.  
  
    Compilação concluída – 0 erros, 0 avisos  
  
    ========== Compilação: 0 bem-sucedido, 0 com falha, 1 atualizado, 0 ignorado ==========  
  
5.  No menu **Arquivo** , clique em **Sair**. Se for solicitado que você salve as alterações dos itens do Tutorial de Implantação, clique em **Sim**.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
[Etapa 2: Verificando o pacote de implantação](../integration-services/lesson-2-2-verifying-the-deployment-bundle.md)  
  
## <a name="see-also"></a>Consulte também  
[Criar um utilitário de implantação](../integration-services/packages/create-a-deployment-utility.md)  
  
  
  

