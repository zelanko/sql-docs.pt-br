---
title: 'Tarefa 2: testando e publicando a política de correspondência | Microsoft Docs'
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "65484735"
---
# <a name="task-2-testing-and-publishing-the-matching-policy"></a>Tarefa 2: Testando e publicando a política de correspondência
  Nesta tarefa, você testará e publicará a política de correspondência **remover fornecedores duplicados** .  
  
1.  Na página **resultados da correspondência** , clique em **Iniciar** para testar a política inteira. No seu caso, você tem uma única regra na política; portanto, os resultados do teste da regra e da política devem ser os mesmos.  
  
2.  Revise todos os registros correspondentes e sua pontuação na caixa de listagem. Um registro que tem um ícone **verde** associado a ele é uma duplicata do registro dinâmico que o precede. Aqui estão os pares de exemplos:  
  
    1.  O registro com **ID de registro: 1000005** é uma correspondência do registro com a **ID de registro: 1000004** com **Pontuação: 100%** porque ambos os registros têm os mesmos valores para **CódigoDoFornecedor (pré-requisito)**, **nome do fornecedor**e **colunas ContactEmailAddress**. O DQS escolherá aleatoriamente um registro como registro dinâmico de um cluster.  
  
    2.  O registro **1000023** é uma correspondência do registro **1000022** com a pontuação de correspondência: 93% porque os dois registros têm os mesmos valores para as colunas **CódigoDoFornecedor (pré-requisito)** e **nome do fornecedor** , mas valores diferentes para a coluna **ContactEmailAddress** .  
  
    3.  Role até a parte inferior da lista para ver dois registros com IDs de registros: **1000051** e **1000052**. O registro **1000052** é considerado uma correspondência com a pontuação de correspondência **91%** porque os dois registros têm os mesmos valores para as colunas **CódigoDoFornecedor** e **ContactEmailAddress** , mas valores diferentes para a coluna **nome do fornecedor** .  
  
     ![Definição de Políticas - Resultados de Políticas](../../2014/tutorials/media/et-testingandpublishingthematchingpolicy-01.jpg "Definição de Políticas - Resultados de Políticas")  
  
3.  Clique com o botão direito do mouse em qualquer registro correspondente (com o ícone verde) e clique em **Exibir detalhes** para ver mais detalhes sobre a correspondência, como contribuição de cada Pontuação de campo, para a pontuação de correspondência geral.  
  
     ![Caixa de diálogo Detalhes de Pontuação Correspondente](../../2014/tutorials/media/et-testingandpublishingthematchingpolicy-02.jpg "Caixa de diálogo Detalhes de Pontuação Correspondente")  
  
4.  Clique em **fechar** para fechar a caixa de diálogo **detalhes da Pontuação de correspondência** .  
  
5.  Clique na guia **resultados de correspondência** na parte inferior da página. Essa guia fornece detalhes como o número de registros correspondentes, o número de registros não correspondentes, o número de clusters com registros correspondentes, o tamanho médio do cluster, o tamanho mínimo do cluster e o tamanho máximo do cluster. Consulte [criar uma política de correspondência](https://msdn.microsoft.com/library/hh270290.aspx) para obter mais detalhes. Não é possível exportar resultados dessa atividade. Você está apenas definindo uma política de correspondência usando os dados de exemplo para testar as regras e a política com base nesses dados.  
  
     ![Guia Resultados Correspondentes](../../2014/tutorials/media/et-testingandpublishingthematchingpolicy-03.jpg "Guia Resultados Correspondentes")  
  
6.  Clique em **concluir** para concluir a criação da política de correspondência.  
  
    > [!NOTE]  
    >  Você definiu a política de correspondência aqui; portanto, não é possível exportar resultados para um arquivo de saída. Você usou basicamente um arquivo de entrada de exemplo, criou regras e testou as regras e a política com base nos dados de exemplo com o objetivo de definir a política.  
  
7.  Na caixa de diálogo SQL Server Data Quality Services, clique em **publicar** e clique em **OK** na caixa de mensagem. Agora, a política de correspondência que você definiu é publicada na base de dados de conhecimento dos **fornecedores** . Você pode usar a base de dados de conhecimento para executar o processo de correspondência com base em um arquivo de entrada, a fim de identificar e remover duplicatas.  
  
## <a name="next-step"></a>Próxima etapa  
 [Tarefa 3: Criando e executando um projeto de qualidade de dados para correspondência](../../2014/tutorials/task-3-creating-and-running-a-data-quality-project-for-matching.md)  
  
  
