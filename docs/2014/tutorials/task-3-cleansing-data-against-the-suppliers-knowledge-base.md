---
title: 'Tarefa 3: limpando dados em relação à base de conhecimento dos fornecedores | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 647c924a-9b91-4294-8d96-e81416e4e90e
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 13201a8b904a5fc5232b9fa860710e4e39cce67a
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85064754"
---
# <a name="task-3-cleansing-data-against-the-suppliers-knowledge-base"></a>Tarefa 3: Limpando dados em relação à base de dados de conhecimento de fornecedores
  Nesta tarefa, você executará o processo de limpeza auxiliado por computador. O DQS usa algoritmos avançados e níveis de confiança baseados nos valores de limite especificados para analisar os dados em relação à base de dados de conhecimento selecionada e depois limpá-los. Consulte [limpeza de dados usando o conhecimento do DQS (interno)](https://msdn.microsoft.com/library/hh213061.aspx) para obter mais detalhes.

1.  Clique em **Iniciar** para iniciar o processo de limpeza auxiliada por computador.

     ![Página Limpar do processo de limpeza](../../2014/tutorials/media/et-cleansingdataagainstthesupplierkb-01.jpg "Página Limpar do processo de limpeza")

2.  Quando o processo de limpeza for concluído, examine **estatísticas** na guia **criador de perfil** . As estatísticas de origem fornecem o número de registros processados, o número de registros que são considerados corretos, o número de registros que o DQS corrige, o número de registros que têm alterações sugeridas pelo DQS e o número de registros que são inválidos. Na caixa de listagem à direita, você pode visualizar os valores corrigidos, os valores sugeridos e a integridade (até que ponto os dados estão presentes) e a precisão (até que ponto os dados podem ser usados para os fins pretendidos) de valores para cada domínio envolvido no processo de limpeza.

     ![Resultados da limpeza](../../2014/tutorials/media/et-cleansingdataagainstthesupplierkb-02.jpg "Resultados da limpeza")

3.  Clique em **Avançar** para alternar para a página **gerenciar e exibir resultados** .

## <a name="next-step"></a>Próxima etapa
 [Tarefa 4: Gerenciando e exibindo resultados](../../2014/tutorials/task-4-manaing-and-viewing-results.md)


