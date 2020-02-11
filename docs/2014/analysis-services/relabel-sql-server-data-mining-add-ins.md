---
title: Rotular novamente (SQL Server suplementos de mineração de dados) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data preparation
- relabel
- data cleaning
ms.assetid: af041b39-fdd1-4cb5-a5ef-2f3ddab84614
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5471720cbd3084c661dec93d9c7f4f680e066b86
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66070398"
---
# <a name="relabel-sql-server-data-mining-add-ins"></a>Rotular novamente (Suplementos de Mineração de Dados do SQL Server)
  ![Ícone do Office 13 para a ferramenta Rotular Novamente](media/dm13-relabel.gif "Ícone do Office 13 para a ferramenta Rotular Novamente")  
  
 O Cliente de Mineração de Dados para Excel o ajuda a criar novos rótulos para os dados para facilitar o entendimento dos resultados da análise.  
  
 Motivos para a nova rotulagem:  
  
-   Os dados incluem os resultados que foram codificados, como 1 para masculino e 2 para feminino.  
  
-   Você está particionando valores numéricos e quer atribuir aos intervalos um nome descritivo.  
  
-   Você deseja simplificar nomes longos.  
  
## <a name="using-the-relabel-wizard"></a>Usando o Assistente de Rotular Novamente  
  
1.  Na faixa de opções **mineração de dados** , clique em **limpar** e, em seguida, selecione **rotular novamente**.  
  
2.  Selecione a tabela ou o intervalo de dados com os dados que você deseja corrigir.  
  
3.  Na página de **novo rótulo** do assistente, selecione uma única coluna, escolhendo a coluna na lista suspensa ou clicando na coluna no painel **amostras de dados** .  
  
     O painel **amostras de dados** mostra apenas cerca de 50 linhas de dados, mas eles são amostrados para garantir que você veja uma boa propagação de valores.  
  
     Clique no cabeçalho da coluna para **contagem** a ser classificada pela contagem de cada valor.  
  
     Você também pode classificar por **Rótulos originais**, o que é útil se você quiser rotular novamente todos os valores mais altos ou mais baixos primeiro.  
  
4.  Na página **rotular dados novamente** do assistente, examine os valores na coluna **Rótulos originais** e decida como deseja agrupá-los ou editá-los.  
  
5.  Digite um novo valor na linha em **novos rótulos**. Você também pode escolher um valor na lista de valores existentes. À medida que você digita novos valores, eles são disponibilizados para reutilização imediatamente.  
  
6.  Quando você tiver inserido linhas suficientes, clique em **Avançar**e, na página **Selecionar destino** , escolha onde você salvará os dados rerotulados.  
  
    -   **Adicionar como uma nova coluna à planilha atual**  
  
         Clique para adicionar uma nova coluna à tabela que contém os novos valores.  
  
    -   **Copiar os dados da planilha com alterações em uma nova planilha**  
  
         Clique para criar uma nova planilha que contenha os dados atualizados.  
  
    -   **Alterar dados no local**  
  
         Clique para substituir os dados originais pelos novos valores.  
  
## <a name="see-also"></a>Consulte Também  
 [Explorando e limpando dados](exploring-and-cleaning-data.md)  
  
  
