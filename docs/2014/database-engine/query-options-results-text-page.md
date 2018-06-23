---
title: Opções de consulta (página de texto) de resultados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.swb.query.text.f1
ms.assetid: fd2fb409-58f9-4ede-8349-ce007126b68d
caps.latest.revision: 15
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 51e1a98f00bc4d33e0609f1b03ceca928bded049
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36120638"
---
# <a name="query-options-results-text-page"></a>Resultados das opções de consulta (página de texto)
  Use esta página para especificar as opções de exibição de um conjunto de resultados da consulta em formato de texto. As configurações desta página também se aplicam quando **Resultados em Arquivo** é selecionado.  
  
 **Formato de saída**  
 Por padrão, a saída é exibida em colunas criadas preenchendo os resultados com espaços. Outras opções são o uso de vírgulas, tabulações ou espaços para separar as colunas. Marque a caixa de seleção **Delimitador personalizado** para especificar um caractere delimitador diferente na caixa **Delimitador personalizado** .  
  
 **Delimitador personalizado**  
 Especifique o caractere de sua escolha para separar colunas. Esta opção só está disponível se a caixa de seleção **Delimitador personalizado** for marcada na caixa **Formato de saída** .  
  
 **Incluir cabeçalhos de coluna no conjunto de resultados**  
 Desmarque esta caixa de seleção se não quiser cada coluna rotulada com um título de coluna.  
  
 **Rolar à medida que resultados forem recebidos**  
 Marque esta caixa de seleção para manter o foco de exibição nos registros retornados mais recentemente na parte inferior. Desmarque esta caixa de seleção para manter o foco de exibição nas primeiras linhas recebidas.  
  
 **Alinhar valores numéricos à direita**  
 Marque esta caixa de seleção para alinhar valores numéricos à direita da coluna. Isso pode tornar mais fácil a revisão de números com um número fixo de casas decimais.  
  
 **Descartar resultado após a execução da consulta**  
 Libera memória descartando os resultados da consulta depois de serem recebidos pelo monitor.  
  
 **Exibir resultados em uma guia separada**  
 Marque essa caixa de seleção para exibir o conjunto de resultados em uma nova janela de documento, em vez de na parte inferior da janela de documentos de consulta.  
  
 **Alternar para a guia resultados após a execução da consulta**  
 Clique para definir automaticamente o foco da tela no conjunto de resultados.  
  
 **Número máximo de caracteres exibidos em cada coluna**  
 Esse valor padrão é 256. Aumente o valor para exibir conjuntos de resultados maiores sem truncar.  
  
 **Redefinir para padrão**  
 Redefine todos os valores dessa página com os valores padrão originais.  
  
## <a name="saving-a-text-result-set-with-headers"></a>Salvar um conjunto de resultados de texto com cabeçalhos  
 Para salvar resultados de consulta como um arquivo de texto com cabeçalhos, marque a caixa de seleção **Incluir cabeçalhos de colunas no conjunto de resultados** e um formato de saída delimitado. Agora, o arquivo do relatório conterá cabeçalhos quando você clicar em **Resultados em Arquivo** na barra de ferramenta ou quando você clicar com o botão direito do mouse em qualquer um dos resultados da consulta, clicar em **Salvar Resultados Como**, digitar um nome de arquivo e clicar em **Salvar**.  
  
  