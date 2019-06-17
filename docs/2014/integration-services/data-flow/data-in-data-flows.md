---
title: Dados em fluxos de dados | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- converting data types [Integration Services]
- comparing data
- data types [Integration Services], data flow
- parsing [Integration Services]
- string comparisons
- data flow [Integration Services], data options
ms.assetid: 8a9d6186-eb52-48e3-997e-021f24d458a3
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 225b6010e5d5a6c45a84d7e22272c4e5242906fd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62827896"
---
# <a name="data-in-data-flows"></a>Dados em fluxos de dados
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] fornece um conjunto de tipos de dados que são usados em fluxos de dados.  
  
## <a name="data-type-conversion"></a>Conversão de tipo de dados  
 A fonte que você adiciona a um fluxo de dados converte os dados de origem para tipos de dados [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . As transformações subsequentes podem converter os dados para um tipo de dados [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] diferente e, dependendo do repositório do tipo de dados no qual eles são carregados, os destinos podem converter o tipo de dados [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] finais no tipo de dados exigido pelo armazenamento de dados de destino. Para obter mais informações, consulte [Integration Services Data Types](integration-services-data-types.md).  
  
 Para converter os dados em um tipo de dados [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , um componente do fluxo de dados analisa os dados. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] fornece dois tipos de análise de dados: análise rápida e análise padrão. A maior parte dos componentes de fluxo de dados só pode usar a análise padrão, entretanto, a fonte de Arquivo Simples e a transformação Conversão de Dados podem usar tanto a análise rápida quanto a análise padrão. Para obter mais informações, consulte [Análise de dados](parsing-data.md).  
  
## <a name="data-type-comparison"></a>Comparação de tipos de dados  
 Muitas transformações comparam valores de dados Por exemplo, a transformação Agregação compara os valores com o propósito de agregar valores em um conjunto de linhas de dados, a transformação Classificação compara os valores para poder classificá-los, e a transformação Pesquisa compara os valores em relação aos valores de uma tabela de referência separada. Para especificar como as sequências de caracteres devem ser comparadas, a transformação inclui um conjunto de opções de comparação, como ignorar ou não a diferenciação de maiúsculas e minúsculas, como manusear os tipos de kana em textos em japonês, e ignorar ou não caracteres de espaço em branco na cadeia de caracteres. Para obter mais informações, consulte [Comparing String Data](comparing-string-data.md).  
  
 O avaliador da expressão também compara os valores dos dados quando avalia as expressões que as variáveis, restrições de precedência e transformações usam.  
  
## <a name="data-flow-troubleshooting"></a>Solução de problemas de fluxo de dados  
 Quando você tiver implantado um pacote no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , poderá analisar o fluxo de dados no pacote durante a execução para verificar o desempenho ou procurar outros problemas. Os relatórios padrão estão disponíveis para permitir exibir status de pacote e histórico, e você pode consultar as exibições de banco de dados que fornecem informações detalhadas sobre execução de pacote. Você também pode adicionar e remover toques de dados dinamicamente durante a execução para atingir componentes específicos de seu pacote. Para obter mais informações, consulte [Análise do Fluxo de Dados](data-flow.md).  
  
  
