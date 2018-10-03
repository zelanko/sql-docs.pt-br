---
title: 'Etapa 3: modificar o gerenciador de conexões de arquivo simples | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
ms.assetid: 459e3995-2116-4f15-aaa2-32f26113869c
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2e5f2aecb84754ee470a9cbafabdf06e38d38ae1
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48102027"
---
# <a name="step-3-modifying-the-flat-file-connection-manager"></a>Etapa 3: Modificando o Gerenciador de Conexões de Arquivo Simples
  Nesta tarefa, você modificará o gerenciador de conexões de arquivo simples que você criou e configurou na Lição 1. Quando foi criado originalmente, o gerenciador de conexões de arquivo simples foi configurado para carregar estatisticamente um único arquivo. Para habilitar o gerenciador de conexões de Arquivo Simples a carregar arquivos de forma iterativa, você deve modificar a propriedade ConnectionString do gerenciador de conexões para aceitar a variável definida pelo usuário `User:varFileName`, que contém o caminho do arquivo a ser carregado em tempo de execução.  
  
 Ao modificar o gerenciador de conexões para usar o valor da variável definida pelo usuário, `User::varFileName`, para popular a propriedade ConnectionString do gerenciador de conexões, o gerenciador de conexões poderá se conectar a diferentes arquivos simples. No tempo de execução, cada iteração do contêiner Loop Foreach atualizará dinamicamente a variável `User::varFileName` . Atualizar a variável, por sua vez, faz com que o gerenciador de conexões se conecte a um arquivo simples diferente e a tarefa de fluxo de dados processe um conjunto diferente de dados.  
  
### <a name="to-configure-the-flat-file-connection-manager-to-use-a-variable-for-the-connection-string"></a>Para configurar o gerenciador de conexões de arquivo simples para usar uma variável para a cadeia de conexão  
  
1.  No painel **Gerenciadores de Conexões** , clique com o botão direito do mouse em **Dados de Origem de Arquivo Simples de Exemplo**e selecione **Propriedades**.  
  
2.  Na janela Propriedades, em **Expressões**, clique na célula vazia e clique no botão de reticências **(…)**.  
  
3.  No **Editor de expressões de propriedade** na caixa de **propriedade** coluna, digite ou selecione `ConnectionString`.  
  
4.  Na coluna **Expressão** , clique no botão de reticências **(…)** para abrir a caixa de diálogo **Construtor de Expressões** .  
  
5.  Na caixa de diálogo **Construtor de Expressão** , expanda o nó **Variáveis** .  
  
6.  Arraste a variável, **User::varFileName**, para a caixa **Expressão** .  
  
7.  Clique em **OK** para fechar a caixa de diálogo **Construtor de Expressão** .  
  
8.  Clique em **OK** novamente para fechar a caixa de diálogo **Editor de Expressões de Propriedades** .  
  
## <a name="next-lesson-task"></a>Próxima tarefa da lição  
 [Etapa 4: Testando o pacote de tutorial da Lição 2](../integration-services/lesson-2-4-testing-the-lesson-2-tutorial-package.md)  
  
  
