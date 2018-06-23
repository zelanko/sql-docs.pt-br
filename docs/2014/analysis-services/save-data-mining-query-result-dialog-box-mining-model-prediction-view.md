---
title: Salvar a caixa de diálogo de resultados de consulta (exibição de previsão do modelo de mineração) de mineração de dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.asvs.dm.savedataminingqueryresult.f1
helpviewer_keywords:
- Save Data Mining Query Result dialog box
ms.assetid: 112fb527-7466-4fd4-9cf1-75596135648f
caps.latest.revision: 16
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 709c3364ac5b4d6bc159af4ec6db40663d21fcbf
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36008754"
---
# <a name="save-data-mining-query-result-dialog-box-mining-model-prediction-view"></a>Caixa de diálogo Salvar Resultado da Consulta de Mineração de Dados (Exibição de Previsão do Modelo de Mineração)
  Use a caixa de diálogo **Salvar Resultado da Consulta da Mineração de Dados** para salvar os resultados de uma consulta de mineração de dados em uma nova tabela.  
  
 A nova tabela será criada no banco de dados definido pela fonte de dados.  
  
## <a name="options"></a>Opções  
 **Fonte de dados**  
 Selecione uma fonte de dados do projeto atual. Se a fonte de dados correta não existir, clique em **Novo** para criar uma nova fonte de dados.  
  
 **Nova**  
 Abre o **Assistente de Fonte de Dados**.  
  
 **Nome da tabela**  
 Digite um nome para a nova tabela.  
  
 **Substituir se existir**  
 Selecione esta opção se você quiser substituir uma tabela existente com o mesmo nome.  
  
 Substituir a tabela existente será necessário se qualquer um dos seguintes for verdadeiro:  
  
-   Você adicionou colunas à consulta de previsão.  
  
-   Você alterou os nomes ou tipos de dados de todas as colunas na consulta de previsão.  
  
-   Você executou uma instrução ALTER na tabela de destino.  
  
 Se várias colunas tiverem o mesmo nome (por exemplo, várias colunas derivadas podem ter o nome da coluna padrão **Expression**), você deverá criar um alias para cada coluna com um nome duplicado. Se as colunas não tiverem nomes exclusivos, um erro será gerado quando o designer tentar salvar os resultados no SQL Server, porque as colunas em uma tabela devem ter nomes exclusivos.  
  
 **Adicione à DSV**  
 (Opcional) Selecione uma exibição de fonte de dados contida no projeto se quiser adicionar a tabela a uma fonte de dados existente.  
  
 Esta opção será útil se você quiser manter todas as tabelas relacionadas para um modelo, por exemplo, dados de treinamento, dados de origem de previsão e resultados de consulta, na mesma fonte de dados.  
  
## <a name="see-also"></a>Consulte também  
 [Construtor de consultas de previsão &#40;mineração de dados&#41;](prediction-query-builder-data-mining.md)   
 [Interfaces de consulta de mineração de dados](data-mining/data-mining-query-tools.md)   
 [Referência de instruções de DMX &#40extensões de Mineração de Dados&#41;](/sql/dmx/data-mining-extensions-dmx-statements)  
  
  
