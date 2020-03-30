---
title: 'Etapa 4: Testar o pacote de tutoriais da Lição 2 | Microsoft Docs'
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 0e8c0a25-8f79-41df-8ed2-f82a74b129cd
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 1b17fc99cc7746739f381ba22f55a973d55497a1
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "71283561"
---
# <a name="lesson-2-4-test-the-lesson-2-tutorial-package"></a>Lição 2-4: Testar o pacote de tutorial da Lição 2

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



Com o contêiner Loop Foreach e o gerenciador de conexões de Arquivo Simples agora configurado, o pacote da Lição 2 pode iterar pelos 14 arquivos simples na pasta Dados de Exemplo. Cada vez que um nome de arquivo corresponde aos critérios especificados, o contêiner Loop Foreach preenche a variável definida pelo usuário com o nome do arquivo. Essa variável, por sua vez, atualiza a propriedade ConnectionString do gerenciador de conexões de Arquivo Simples, que se conecta àquele arquivo simples. O contêiner Foreach Loop então executa a tarefa de fluxo de dados não modificada com relação aos dados nesse arquivo simples.  
  
> [!NOTE]  
> Se você tiver executado o pacote da Lição 1, precisará excluir os registros da tabela dbo.NewFactCurrencyRate no banco de dados AdventureWorksDW2012 antes de executar o pacote desta lição. A Lição 2 tenta inserir registros já inseridos na Lição 1, o que causa um erro.  
  
## <a name="check-the-package-layout"></a>Verificar o layout do pacote  
Antes de testar o pacote, verifique se os fluxos de controle e de dados do pacote da Lição 2 contêm os objetos mostrados nos diagramas a seguir. O fluxo de dados da Lição do 2 é igual ao da Lição 1.  
  
**Fluxo de Controle**  
  
![Fluxo de controle no pacote](../integration-services/media/task4lesson2control.gif "Fluxo de controle no pacote")  
  
**Fluxo de Dados**  
  
![Fluxo de dados no pacote](../integration-services/media/task9lesson1data.gif "Fluxo de dados no pacote")  
  
## <a name="test-the-lesson-2-tutorial-package"></a>Testar o pacote de tutorial da Lição 2  
  
1.  No **Gerenciador de Soluções**, clique com o botão direito do mouse em **Lesson 2.dtsx** e selecione **Executar Pacote**.  
  
    O pacote é executado. Você pode verificar o status de cada loop na janela de **Saída** ou selecionando a guia **Progresso**. Por exemplo, você pode ver que foram adicionadas 1.097 linhas à tabela de destino do arquivo Currency_VEB.txt.  
  
2.  Terminada a execução do pacote, no menu **Depurar**, selecione **Parar Depuração**.  
  
## <a name="go-to-next-lesson"></a>Vá para a próxima lição  
[Lição 3: Adicionar o log com o SSIS](../integration-services/lesson-3-add-logging-with-ssis.md)  
  
## <a name="see-also"></a>Confira também  
[Execução de projetos e pacotes](../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md)  
  
  
  

