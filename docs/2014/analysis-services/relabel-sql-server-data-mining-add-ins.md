---
title: Rotular novamente (SQL Server Data Mining Add-ins) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data preparation
- relabel
- data cleaning
ms.assetid: af041b39-fdd1-4cb5-a5ef-2f3ddab84614
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 74e2322416ec06c36a7834f35581ed611480b6e6
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52414603"
---
# <a name="relabel-sql-server-data-mining-add-ins"></a>Rotular novamente (Suplementos de Mineração de Dados do SQL Server)
  ![Ícone do Office 13 para a ferramenta rotular novamente](media/dm13-relabel.gif "ícone do Office 13 para a ferramenta rotular novamente")  
  
 O Cliente de Mineração de Dados para Excel o ajuda a criar novos rótulos para os dados para facilitar o entendimento dos resultados da análise.  
  
 Motivos para a nova rotulagem:  
  
-   Os dados incluem os resultados que foram codificados, como 1 para masculino e 2 para feminino.  
  
-   Você está particionando valores numéricos e quer atribuir aos intervalos um nome descritivo.  
  
-   Você deseja simplificar nomes longos.  
  
## <a name="using-the-relabel-wizard"></a>Usando o Assistente de Rotular Novamente  
  
1.  No **Data Mining** faixa de opções, clique em **Clean** e, em seguida, selecione **rotular novamente**.  
  
2.  Selecione a tabela ou o intervalo de dados com os dados que você deseja corrigir.  
  
3.  No **rotular novamente** página do assistente, selecione uma única coluna, escolhendo a coluna na lista suspensa ou clicando na coluna na **amostras de dados** painel.  
  
     O **exemplos de dados** painel mostra somente cerca de 50 linhas de dados, mas eles são exemplificados para garantir que você veja uma boa variedade de valores.  
  
     Clique no cabeçalho de coluna para **contagem** para classificar pela contagem de cada valor.  
  
     Você também pode classificar por **rótulos originais**, que é útil se você quiser rotular novamente todos os valores maiores ou menores pela primeira vez.  
  
4.  No **rotular novamente** página de dados do assistente, examine os valores na **rótulos originais** coluna e decidir como deseja agrupar ou editá-los.  
  
5.  Digite um novo valor na linha sob **novos rótulos**. Você também pode escolher um valor na lista de valores existentes. À medida que você digita novos valores, eles são disponibilizados para reutilização imediatamente.  
  
6.  Quando você inserir linhas suficientes, clique em **próxima**e, na **Selecionar destino** , escolha onde você salvará os dados com novos rótulos.  
  
    -   **Adicionar como uma nova coluna à planilha atual**  
  
         Clique para adicionar uma nova coluna à tabela que contém os novos valores.  
  
    -   **Copiar dados da planilha com alterações em uma nova planilha**  
  
         Clique para criar uma nova planilha que contenha os dados atualizados.  
  
    -   **Alterar dados no local**  
  
         Clique para substituir os dados originais pelos novos valores.  
  
## <a name="see-also"></a>Consulte também  
 [Explorando e limpando dados](exploring-and-cleaning-data.md)  
  
  
