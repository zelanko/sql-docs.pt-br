---
title: 'Etapa 3: modificar o gerenciador de conexões de arquivo simples | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 459e3995-2116-4f15-aaa2-32f26113869c
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 5a237fac7322ed1529a8962b096c6b918ffee33b
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84968206"
---
# <a name="step-3-modifying-the-flat-file-connection-manager"></a>Etapa 3: Modificar o gerenciador de conexões de arquivo simples
  Nesta tarefa, você modificará o gerenciador de conexões de arquivo simples que você criou e configurou na Lição 1. Quando foi criado originalmente, o gerenciador de conexões de arquivo simples foi configurado para carregar estatisticamente um único arquivo. Para habilitar o gerenciador de conexões de Arquivo Simples a carregar arquivos de forma iterativa, você deve modificar a propriedade ConnectionString do gerenciador de conexões para aceitar a variável definida pelo usuário `User:varFileName`, que contém o caminho do arquivo a ser carregado em tempo de execução.  
  
 Ao modificar o gerenciador de conexões para usar o valor da variável definida pelo usuário, `User::varFileName`, para popular a propriedade ConnectionString do gerenciador de conexões, o gerenciador de conexões poderá se conectar a diferentes arquivos simples. No tempo de execução, cada iteração do contêiner Loop Foreach atualizará dinamicamente a variável `User::varFileName` . Atualizar a variável, por sua vez, faz com que o gerenciador de conexões se conecte a um arquivo simples diferente e a tarefa de fluxo de dados processe um conjunto diferente de dados.  
  
### <a name="to-configure-the-flat-file-connection-manager-to-use-a-variable-for-the-connection-string"></a>Para configurar o gerenciador de conexões de arquivo simples para usar uma variável para a cadeia de conexão  
  
1.  No painel **Gerenciadores de Conexões** , clique com o botão direito do mouse em **Dados de Origem de Arquivo Simples de Exemplo**e selecione **Propriedades**.  
  
2.  No janela Propriedades, para **expressões**, clique na célula vazia e, em seguida, clique no botão de reticências **(...)**.  
  
3.  Na caixa de diálogo **Editor de expressões de propriedade** , na coluna **Propriedade** , digite ou selecione `ConnectionString` .  
  
4.  Na coluna **expressão** , clique no botão de reticências **(...)** para abrir a caixa de diálogo **Construtor de expressões** .  
  
5.  Na caixa de diálogo **Construtor de Expressão** , expanda o nó **Variáveis** .  
  
6.  Arraste a variável, **User:: varFileName**, para a caixa **expressão** .  
  
7.  Clique em **OK** para fechar a caixa de diálogo **Construtor de Expressão** .  
  
8.  Clique em **OK** novamente para fechar a caixa de diálogo **Editor de Expressões de Propriedades** .  
  
## <a name="next-lesson-task"></a>Próxima tarefa da lição  
 [Etapa 4: Testar o pacote de tutorial da Lição 2](../integration-services/lesson-2-4-testing-the-lesson-2-tutorial-package.md)  
  
  
