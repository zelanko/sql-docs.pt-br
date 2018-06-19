---
title: 'Etapa 3: modificar o gerenciador de conexões de arquivo simples | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: tutorial
applies_to:
- SQL Server 2016
ms.assetid: 459e3995-2116-4f15-aaa2-32f26113869c
caps.latest.revision: 20
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 49aab641ac10aa3f92b59284058b363f3ceba856
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/12/2018
ms.locfileid: "35402918"
---
# <a name="lesson-2-3---modifying-the-flat-file-connection-manager"></a>Lição 2-3 – modificar o gerenciador de conexões de arquivo simples
Nesta tarefa, você modificará o gerenciador de conexões de arquivo simples que você criou e configurou na Lição 1. Quando foi criado originalmente, o gerenciador de conexões de arquivo simples foi configurado para carregar estatisticamente um único arquivo. Para habilitar o gerenciador de conexões de Arquivo Simples a carregar arquivos de forma iterativa, você deve modificar a propriedade ConnectionString do gerenciador de conexões para aceitar a variável definida pelo usuário `User:varFileName`, que contém o caminho do arquivo a ser carregado em tempo de execução.  
  
Ao modificar o gerenciador de conexões para usar o valor da variável definida pelo usuário, `User::varFileName`, para popular a propriedade ConnectionString do gerenciador de conexões, o gerenciador de conexões poderá se conectar a diferentes arquivos simples. No tempo de execução, cada iteração do contêiner Loop Foreach atualizará dinamicamente a variável `User::varFileName` . Atualizar a variável, por sua vez, faz com que o gerenciador de conexões se conecte a um arquivo simples diferente e a tarefa de fluxo de dados processe um conjunto diferente de dados.  
  
### <a name="to-configure-the-flat-file-connection-manager-to-use-a-variable-for-the-connection-string"></a>Para configurar o gerenciador de conexões de arquivo simples para usar uma variável para a cadeia de conexão  
  
1.  No painel **Gerenciadores de Conexões** , clique com o botão direito do mouse em **Dados de Origem de Arquivo Simples de Exemplo**e selecione **Propriedades**.  
  
2.  Na janela Propriedades, em **Expressões**, clique na célula vazia e clique no botão de reticências **(…)**.  
  
3.  Na caixa de diálogo **Editor de Expressões de Propriedades** , na coluna **Propriedade** , digite ou selecione **ConnectionString**.  
  
4.  Na coluna **Expressão** , clique no botão de reticências **(…)** para abrir a caixa de diálogo **Construtor de Expressões** .  
  
5.  Na caixa de diálogo **Construtor de Expressão** , expanda o nó **Variáveis** .  
  
6.  Arraste a variável, **User::varFileName**, para a caixa **Expressão** .  
  
7.  Clique em **OK** para fechar a caixa de diálogo **Construtor de Expressão** .  
  
8.  Clique em **OK** novamente para fechar a caixa de diálogo **Editor de Expressões de Propriedades** .  
  
## <a name="next-lesson-task"></a>Próxima tarefa da lição  
[Etapa 4: Testando o pacote de tutorial da Lição 2](../integration-services/lesson-2-4-testing-the-lesson-2-tutorial-package.md)  
  
  
  
