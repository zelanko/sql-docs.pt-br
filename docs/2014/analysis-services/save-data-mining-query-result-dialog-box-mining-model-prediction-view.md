---
title: Caixa de diálogo Salvar resultado da consulta de mineração de dados (exibição de previsão do modelo de mineração) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dm.savedataminingqueryresult.f1
helpviewer_keywords:
- Save Data Mining Query Result dialog box
ms.assetid: 112fb527-7466-4fd4-9cf1-75596135648f
author: minewiskan
ms.author: owend
ms.openlocfilehash: 0838c90f0797a0db9c8a66cd8c5f877aaecdad0a
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84538928"
---
# <a name="save-data-mining-query-result-dialog-box-mining-model-prediction-view"></a>Caixa de diálogo Salvar Resultado da Consulta de Mineração de Dados (Exibição de Previsão do Modelo de Mineração)
  Use a caixa de diálogo **Salvar Resultado da Consulta da Mineração de Dados** para salvar os resultados de uma consulta de mineração de dados em uma nova tabela.  
  
 A nova tabela será criada no banco de dados definido pela fonte de dados.  
  
## <a name="options"></a>Opções  
 **Fonte de Dados**  
 Selecione uma fonte de dados do projeto atual. Se a fonte de dados correta não existir, clique em **Novo** para criar uma nova fonte de dados.  
  
 **Novo**  
 Abre o **Assistente de Fonte de Dados**.  
  
 **Nome da Tabela**  
 Digite um nome para a nova tabela.  
  
 **Substitua se existir**  
 Selecione esta opção se você quiser substituir uma tabela existente com o mesmo nome.  
  
 Substituir a tabela existente será necessário se qualquer um dos seguintes for verdadeiro:  
  
-   Você adicionou colunas à consulta de previsão.  
  
-   Você alterou os nomes ou tipos de dados de todas as colunas na consulta de previsão.  
  
-   Você executou uma instrução ALTER na tabela de destino.  
  
 Se várias colunas tiverem o mesmo nome (por exemplo, várias colunas derivadas podem ter o nome da coluna padrão **Expression**), você deverá criar um alias para cada coluna com um nome duplicado. Se as colunas não tiverem nomes exclusivos, um erro será gerado quando o designer tentar salvar os resultados no SQL Server, porque as colunas em uma tabela devem ter nomes exclusivos.  
  
 **Adicione à DSV**  
 (Opcional) Selecione uma exibição de fonte de dados contida no projeto se quiser adicionar a tabela a uma fonte de dados existente.  
  
 Essa opção será útil se você quiser manter todas as tabelas relacionadas para um modelo, como dados de treinamento, dados de origem de previsão e resultados da consulta, na mesma fonte de dados.  
  
## <a name="see-also"></a>Consulte Também  
 [Construtor de Consultas de &#40;de mineração de dados de previsão&#41;](prediction-query-builder-data-mining.md)   
 [Interfaces de consulta de mineração de dados](data-mining/data-mining-query-tools.md)   
 [Referência de instruções de DMX &#40extensões de Mineração de Dados&#41;](/sql/dmx/data-mining-extensions-dmx-statements)  
  
  
