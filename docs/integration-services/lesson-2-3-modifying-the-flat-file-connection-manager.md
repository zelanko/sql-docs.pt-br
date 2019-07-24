---
title: 'Etapa 3: Modificar o gerenciador de conexões de Arquivo Simples | Microsoft Docs'
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 459e3995-2116-4f15-aaa2-32f26113869c
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 1cb492b9b162c9494c4cd009fd3ad5b68427a030
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68086578"
---
# <a name="lesson-2-3-modify-the-flat-file-connection-manager"></a>Lição 2-3: Modificar o gerenciador de conexões de Arquivo Simples

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



Nesta tarefa, você modificará o Gerenciador de conexão de arquivo simples da Lição 1. Esse gerenciador de conexões de Arquivo Simples está configurado para carregar estatisticamente um único arquivo. Para habilitar o gerenciador de conexões de Arquivo Simples a carregar arquivos de forma iterativa, você modifica a propriedade ConnectionString do gerenciador de conexões para usar a variável definida pelo usuário `User::varFileName`, que contém o caminho do arquivo a ser carregado em tempo de execução.  
  
Ao modificar o gerenciador de conexão para usar o valor da variável definida pelo usuário para alterar a propriedade ConnectionString, o gerenciador de conexão conecta-se a diferentes arquivos simples. No tempo de execução, cada iteração do contêiner de Foreach Loop atualiza a variável `User::varFileName`. Atualizar a variável, por sua vez, faz com que o gerenciador de conexões se conecte a um arquivo simples diferente e a tarefa de fluxo de dados processe um conjunto diferente de dados.  
  
## <a name="configure-the-flat-file-connection-manager-to-use-a-variable"></a>Configurar o gerenciador de conexões do Arquivo Simples para usar uma variável  
  
1.  No painel **Gerenciadores de Conexões** , clique com o botão direito do mouse em **Dados de Origem de Arquivo Simples de Exemplo**e selecione **Propriedades**.  

2.  Na janela **Propriedades**, verifique se **PackagePath** começa com **\Package.Connections**. Se não, no painel **Gerenciadores de Conexões**, clique com o botão direito do mouse em **Dados de Origem de Arquivo Simples de Exemplo**e selecione **Converter em Conexão do Pacote**.
  
3.  Na janela **Propriedades**, para **Expressões**, selecione a célula vazia e selecione o botão de reticências **(…)** .  
  
4.  Na caixa de diálogo **Editor de Expressões de Propriedades**, na coluna **Propriedade**, selecione ou selecione **ConnectionString**.  
  
5.  Na coluna **Expressão**, selecione o botão de reticências **(…)** para abrir a caixa de diálogo **Construtor de Expressões**.  
  
6.  Na caixa de diálogo **Construtor de Expressões**, expanda o nó **Variáveis**.  
  
7.  Arraste a variável, **User::varFileName** para a caixa **Expressão**.  
  
8.  Selecione **OK** para fechar a caixa de diálogo **Construtor de Expressões**.  
  
9.  Selecione **OK** novamente para fechar a caixa de diálogo **Editor de Expressões de Propriedades**.  
  
## <a name="go-to-next-task"></a>Ir para a próxima tarefa  
[Etapa 4: Testar o pacote de tutorial da Lição 2](../integration-services/lesson-2-4-testing-the-lesson-2-tutorial-package.md)  
  
  
  
