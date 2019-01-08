---
title: Exemplo de arquivo de entrada XML com DTA (configuração especificada pelo usuário) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- sample applications [DTA]
ms.assetid: b29c9716-e5c3-4003-9efb-3ade2197b630
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4fefcec96100a9848810bc37a7b02760a3005cc3
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52781839"
---
# <a name="xml-input-file-sample-with-user-specified-configuration-dta"></a>Exemplo de arquivo de entrada XML com configuração especificada pelo usuário (DTA)
  Copie e cole este exemplo de um arquivo de entrada XML que especifica uma configuração especificada pelo usuário com o elemento **Configuration** em seu editor XML ou editor de texto favorito. Isso permite realizar uma análise hipotética. A análise hipotética envolve o uso do elemento **Configuration** para especificar um conjunto de estruturas de design físico hipotéticas para o banco de dados que você deseja ajustar. Então você usa o Orientador de Otimização do Mecanismo de Banco de Dados para analisar os efeitos de executar uma carga de trabalho em relação a essa configuração hipotética para descobrir se ela melhorará o desempenho de processamento de consulta. Esse tipo de análise oferece a vantagem de poder avaliar a nova configuração sem incorrer na sobrecarga da implementação de fato. Se sua configuração hipotética não oferecer a melhora de desempenho desejada, é fácil alterá-la e fazer novas análises até que você alcance a configuração que produza os resultados necessários.  
  
 Depois de copiar esse exemplo em sua ferramenta de edição, substitua os valores especificados para os elementos **Servidor**, **Banco de Dados**, **Esquema**, **Tabela**, **Carga de trabalho**, **Opções de Ajuste**e **Configuração** com aqueles para sua sessão de ajuste específica. Para obter mais informações sobre todos os atributos e elementos filho que podem ser usados com esses elementos, veja a [Referência do arquivo de entrada XML &#40;Orientador de Otimização do Mecanismo de Banco de Dados&#41;](xml-input-file-reference-database-engine-tuning-advisor.md). O exemplo a segui usa um subconjunto de atributo único disponível e opções de elemento filho.  
  
## <a name="code"></a>Código  
 [!code-xml[InputFileSamples#UserSpecifiedConfigInputFile](../../snippets/xml/SQL14/dta_xml/inputfilesamples/xml/dta_xml_input_file_samples.xml#userspecifiedconfiginputfile)]  
  
## <a name="comments"></a>Comentários  
  
-   A remoção das estruturas de design físico não terá suporte caso você especifique o modo **Absoluto** para o elemento **Configuration** (`Configuration SpecificationMode="Absolute"`).  
  
-   Não é possível criar e remover a mesma estrutura de design físico em qualquer um dos modos (**Relative** ou **Absolute**) do elemento **Configuration** .  
  
## <a name="see-also"></a>Consulte também  
 [Iniciar e usar o Orientador de Otimização do Mecanismo de Banco de Dados](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)   
 [Exibir e trabalhar com a saída do Orientador de Otimização do Mecanismo de Banco de Dados](../../relational-databases/performance/view-and-work-with-the-output-from-the-database-engine-tuning-advisor.md)   
 [Referência do arquivo de entrada XML &#40;Orientador de Otimização do Mecanismo de Banco de Dados&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
