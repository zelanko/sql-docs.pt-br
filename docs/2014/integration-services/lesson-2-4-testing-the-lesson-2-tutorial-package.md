---
title: 'Etapa 4: testar o pacote de tutoriais da Lição 2 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 0e8c0a25-8f79-41df-8ed2-f82a74b129cd
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 0e62ad84a6199568de63676c1b450dc3963c5166
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85440563"
---
# <a name="step-4-testing-the-lesson-2-tutorial-package"></a>Etapa 4: Testar o pacote de tutorial da Lição 2
  Com o contêiner Loop Foreach e o gerenciador de conexões de Arquivo Simples agora configurado, o pacote da Lição 2 pode iterar através da coleção de 14 arquivos simples na pasta Dados de Exemplo. Cada vez que um nome de arquivo é encontrado e corresponde aos critérios de nome de arquivo especificado, o contêiner Loop Foreach popula a variável definida pelo usuário com o nome do arquivo. Essa variável, por sua vez, atualiza a propriedade ConnectionString do gerenciador de conexões de Arquivo Simples, e uma conexão é criada para o novo arquivo simples. O contêiner Loop Foreach, então, executa a tarefa de fluxo de dados não modificados em relação aos dados no novo arquivo simples, antes de se conectar ao próximo arquivo na pasta.  
  
 Use o procedimento a seguir para testar a nova funcionalidade de loop que você adicionou ao seu pacote.  
  
> [!NOTE]  
>  Se você tiver executado o pacote da lição 1, precisará excluir os registros de dbo.FactCurrency no AdventureWorksDW2012 antes de executar o pacote dessa lição, ou o pacote falhará com erros que indicam uma violação de restrição de chave primária. Você receberá os mesmos erros se executar o pacote selecionando Depurar/Iniciar Depuração (ou pressione F5) porque as lições 1 e 2 serão executadas. A lição 2 tentará inserir os registros já inseridos na lição 1.  
  
## <a name="checking-the-package-layout"></a>Verificando o layout do pacote  
 Antes de testar o pacote, deve-se verificar se os fluxos de controle e de dados do pacote da Lição 2 contêm os objetos mostrados nos diagramas a seguir. O fluxo de dados deve ser idêntico ao fluxo de dados na Lição 1.  
  
 **Fluxo de controle**  
  
 ![Fluxo de controle no pacote](../../2014/tutorials/media/task4lesson2control.gif "Fluxo de controle no pacote")  
  
 **Fluxo de Dados**  
  
 ![Fluxo de dados no pacote](../../2014/tutorials/media/task9lesson1data.gif "Fluxo de dados no pacote")  
  
### <a name="to-test-the-lesson-2-tutorial-package"></a>Para testar o pacote de tutorial da Lição 2  
  
1.  No **Gerenciador de Soluções**, clique com o botão direito do mouse em **Lesson 2.dtsx** e clique em **Executar Pacote**.  
  
     O pacote será executado. Você pode verificar o status de cada loop na janela de saída ou clicando na guia **progresso** . Por exemplo, você pode ver que 1097 linhas foram adicionadas à tabela de destino do arquivo Currency_VEB.txt.  
  
2.  Terminada a execução do pacote, no menu **Depurar** , clique em **Parar Depuração**.  
  
## <a name="next-lesson"></a>Próxima lição  
 [Lição 5: Como adicionar configurações de pacote para o modelo de implantação de pacote](../integration-services/lesson-5-add-ssis-package-configurations-for-the-package-deployment-model.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Execução de projetos e pacotes](packages/run-integration-services-ssis-packages.md)  
  
  
