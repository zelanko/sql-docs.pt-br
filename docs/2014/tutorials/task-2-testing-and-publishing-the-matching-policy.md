---
title: 'Tarefa 2: Testando e publicando a política de correspondência | Microsoft Docs'
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: e1ffb6d7-fbc5-4695-b538-cc2302d1a17d
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: a9957625e09bde8bb733eca6e564dfdcfbb0bd98
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65484735"
---
# <a name="task-2-testing-and-publishing-the-matching-policy"></a>Tarefa 2: Testar e publicar a política de correspondência
  Nesta tarefa, você pode testar e publicar os **remover fornecedores duplicados** política de correspondência.  
  
1.  No **resultados correspondentes** , clique em **iniciar** para testar a política inteira. No seu caso, você tem uma única regra na política; portanto, os resultados do teste da regra e da política devem ser os mesmos.  
  
2.  Revise todos os registros correspondentes e sua pontuação na caixa de listagem. Um registro que tenha um **verde** ícone associado a ele é uma duplicata de registro dinâmico que o precede. Aqui estão os pares de exemplos:  
  
    1.  O registro com **ID de registro: 1000005** é uma correspondência do registro com **Id de registro: 1000004** com **pontuação: 100%** porque ambos os registros têm os mesmos valores para **SupplierID (pré-requisito)**, **Supplier Name**, e **ContactEmailAddress colunas**. O DQS escolherá aleatoriamente um registro como registro dinâmico de um cluster.  
  
    2.  O registro **1000023** é uma correspondência do registro **1000022** com a pontuação de correspondência: 93% porque os dois registros têm os mesmos valores para **SupplierID (pré-requisito)** e **Supplier Name** colunas, mas valores diferentes para o **ContactEmailAddress** coluna.  
  
    3.  Role até a parte inferior da lista para ver dois registros com as IDs: **1000051** e **1000052**. Registro **1000052** é considerada uma correspondência com a pontuação de correspondência **91%** porque os dois registros têm os mesmos valores para o **SupplierID** e  **ContactEmailAddress** colunas, mas valores diferentes para o **Supplier Name** coluna.  
  
     ![Definição de política – resultados da política](../../2014/tutorials/media/et-testingandpublishingthematchingpolicy-01.jpg "definição de política – resultados da política")  
  
3.  Clique com botão direito em qualquer registro correspondente (com ícone verde) e clique em **exibir detalhes** para ver mais detalhes sobre a correspondência, como a contribuição de cada pontuação de campo para a pontuação de correspondência geral.  
  
     ![Pontuação de correspondência fornece detalhes sobre a caixa de diálogo](../../2014/tutorials/media/et-testingandpublishingthematchingpolicy-02.jpg "pontuação de correspondência fornece detalhes sobre a caixa de diálogo")  
  
4.  Clique em **feche** para fechar o **detalhes da pontuação de correspondência** caixa de diálogo.  
  
5.  Clique em **resultados de correspondência** guia na parte inferior da página. Essa guia fornece detalhes como o número de registros correspondentes, o número de registros não correspondentes, o número de clusters com registros correspondentes, o tamanho médio do cluster, o tamanho mínimo do cluster e o tamanho máximo do cluster. Ver [criar uma política de conciliação](https://msdn.microsoft.com/library/hh270290.aspx) para obter mais detalhes. Não é possível exportar resultados dessa atividade. Você está apenas definindo uma política de correspondência usando os dados de exemplo para testar as regras e a política com base nesses dados.  
  
     ![Guia de resultados de correspondência](../../2014/tutorials/media/et-testingandpublishingthematchingpolicy-03.jpg "guia resultados de correspondência")  
  
6.  Clique em **concluir** para terminar de criar a política de correspondência.  
  
    > [!NOTE]  
    >  Você definiu a política de correspondência aqui; portanto, não é possível exportar resultados para um arquivo de saída. Você usou basicamente um arquivo de entrada de exemplo, criou regras e testou as regras e a política com base nos dados de exemplo com o objetivo de definir a política.  
  
7.  Na caixa de diálogo Serviços de qualidade de dados do SQL Server, clique em **Publish** e clique em **Okey** na caixa de mensagem. Agora, a política de correspondência que você definiu é publicada para o **fornecedores** da Base de dados de Conhecimento. Você pode usar a base de dados de conhecimento para executar o processo de correspondência com base em um arquivo de entrada, a fim de identificar e remover duplicatas.  
  
## <a name="next-step"></a>Próxima etapa  
 [Tarefa 3: Criando e executando um projeto de qualidade de dados para correspondência](../../2014/tutorials/task-3-creating-and-running-a-data-quality-project-for-matching.md)  
  
  
