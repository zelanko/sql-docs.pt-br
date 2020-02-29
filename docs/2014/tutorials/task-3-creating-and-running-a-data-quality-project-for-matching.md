---
title: 'Tarefa 3: Criando e executando um projeto de qualidade de dados para correspondência | Microsoft Docs'
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 6260e911-ea8b-4c69-a39d-d1bccd565a32
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: c6953214bd5e5353643cb16b75ed51ac18783256
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/28/2020
ms.locfileid: "78171765"
---
# <a name="task-3-creating-and-running-a-data-quality-project-for-matching"></a>Tarefa 3: Criando e executando um projeto de qualidade de dados para correspondência
  Nesta tarefa, você criará um Projeto do Data Quality para a atividade de correspondência e executará o processo de correspondência nos dados de fornecedor limpos para remover as duplicatas nos dados.

1.  Na página principal do **cliente do DQS**, clique em **novo projeto de qualidade de dados**.

2.  Digite **remover duplicatas do fornecedor** do **nome do projeto**.

3.  Selecione **fornecedores** na lista de KBS para o campo **usar base de dados de conhecimento** . Você criou uma política de correspondência nessa base de dados de conhecimento na lição anterior.

4.  Selecione **correspondência** na **lista de atividades** no painel inferior direito.

     ![Projeto de Qualidade de Novos Dados - Correspondência selecionada](../../2014/tutorials/media/et-creatingandrunningadqpformatching.jpg "Projeto de Qualidade de Novos Dados - Correspondência selecionada")

5.  Clique em **Próximo**.

6.  Na página **Mapear** , selecione **Arquivo do Excel** em **Fonte de Dados**.

7.  Clique em **procurar** e selecione **lista de fornecedores limpos. xls**, que é o arquivo de saída da atividade de limpeza.

8.  Mapeie a coluna de origem **CódigoDoFornecedor** para o domínio da **ID** do fornecedor, a coluna **nome do fornecedor** para **nome do fornecedor** domínio e a coluna **ContactEmailAddress** para contatar o domínio de **email** .

9. Clique em **Avançar** para alternar para a página **correspondente** .

10. Clique em **Iniciar** para iniciar o processo de correspondência. Você deverá visualizar resultados semelhantes aos da tarefa anterior, pois usou o mesmo arquivo de entrada para definir a política de correspondência.

11. Revise todos os registros correspondentes e sua pontuação na caixa de listagem. Os resultados deverão ser iguais aos exibidos na tarefa anterior. Consulte as etapas na tarefa anterior para analisar os resultados dessa atividade de correspondência.

12. Clique em **Avançar** para alternar para a página **Exportar** .

## <a name="next-step"></a>Próxima etapa
 [Tarefa 4: Exportando os resultados da atividade de correspondência para um arquivo do Excel](../../2014/tutorials/task-4-exporting-the-results-from-matching-activity-to-an-excel-file.md)


