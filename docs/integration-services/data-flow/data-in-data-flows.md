---
title: Dados em fluxos de dados | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
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
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: dcc79e1bcb8e871b5424e9e4995db58e1f97a513
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47692865"
---
# <a name="data-in-data-flows"></a>Dados em fluxos de dados
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] fornece um conjunto de tipos de dados que são usados em fluxos de dados.  
  
## <a name="data-type-conversion"></a>Conversão de tipo de dados  
 A fonte que você adiciona a um fluxo de dados converte os dados de origem para tipos de dados [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . As transformações subsequentes podem converter os dados para um tipo de dados [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] diferente e, dependendo do repositório do tipo de dados no qual eles são carregados, os destinos podem converter o tipo de dados [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] finais no tipo de dados exigido pelo armazenamento de dados de destino. Para obter mais informações, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
 Para converter os dados em um tipo de dados [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , um componente do fluxo de dados analisa os dados. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] fornece dois tipos de análise de dados: análise rápida e análise padrão. A maior parte dos componentes de fluxo de dados só pode usar a análise padrão, entretanto, a fonte de Arquivo Simples e a transformação Conversão de Dados podem usar tanto a análise rápida quanto a análise padrão. Para obter mais informações, consulte [Análise de dados](../../integration-services/data-flow/parsing-data.md).  
  
## <a name="data-type-comparison"></a>Comparação de tipos de dados  
 Muitas transformações comparam valores de dados Por exemplo, a transformação Agregação compara os valores com o propósito de agregar valores em um conjunto de linhas de dados, a transformação Classificação compara os valores para poder classificá-los, e a transformação Pesquisa compara os valores em relação aos valores de uma tabela de referência separada. Para especificar como as sequências de caracteres devem ser comparadas, a transformação inclui um conjunto de opções de comparação, como ignorar ou não a diferenciação de maiúsculas e minúsculas, como manusear os tipos de kana em textos em japonês, e ignorar ou não caracteres de espaço em branco na cadeia de caracteres. Para obter mais informações, consulte [Comparing String Data](../../integration-services/data-flow/comparing-string-data.md).  
  
 O avaliador da expressão também compara os valores dos dados quando avalia as expressões que as variáveis, restrições de precedência e transformações usam.  
  
## <a name="data-flow-troubleshooting"></a>Solução de problemas de fluxo de dados  
 Quando você tiver implantado um pacote no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , poderá analisar o fluxo de dados no pacote durante a execução para verificar o desempenho ou procurar outros problemas. Os relatórios padrão estão disponíveis para permitir exibir status de pacote e histórico, e você pode consultar as exibições de banco de dados que fornecem informações detalhadas sobre execução de pacote. Você também pode adicionar e remover toques de dados dinamicamente durante a execução para atingir componentes específicos de seu pacote. Para obter mais informações, consulte [Debugging Data Flow](../../integration-services/troubleshooting/debugging-data-flow.md).  
  
  
