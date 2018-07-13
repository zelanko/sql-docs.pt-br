---
title: Exemplo do arquivo de entrada XML com carga de trabalho embutida (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- sample applications [DTA]
ms.assetid: 7c04fe1d-6669-44a1-8b73-36d469e9b002
caps.latest.revision: 13
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6e6bdb810dab08a3b46d164389857c1d394b4a20
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37189603"
---
# <a name="xml-input-file-sample-with-inline-workload-dta"></a>Amostra do arquivo de entrada XML com carga de trabalho embutida (DTA)
  Copie e cole esta amostra em um arquivo de entrada XML que especifica uma carga de trabalho com o elemento **EventString** em seu editor de XML ou editor de texto favorito. Você pode usar o elemento **EventString** para especificar uma carga de trabalho de script [!INCLUDE[tsql](../../includes/tsql-md.md)] no arquivo de entrada XML em vez de usar um arquivo de carga de trabalho separado. Depois de copiar esta amostra na ferramenta de edição, substitua os valores especificados dos elementos **Server**, **Database**, **Schema**, **Table**, **Workload**, **EventString**e **TuningOptions** pelos valores de sua sessão de ajuste específica. Para obter mais informações sobre todos os atributos e elementos filho que podem ser usados com esses elementos, veja a [XML Input File Reference &#40;Database Engine Tuning Advisor&#41;](xml-input-file-reference-database-engine-tuning-advisor.md). O exemplo a segui usa um subconjunto de atributo único disponível e opções de elemento filho.  
  
## <a name="code"></a>Código  
 [!code-xml[InputFileSamples#InlineWorkloadInputFile](../../snippets/xml/SQL14/dta_xml/inputfilesamples/xml/dta_xml_input_file_samples.xml#inlineworkloadinputfile)]  
  
## <a name="comments"></a>Comentários  
 `USE database_name` As instruções podem ser especificadas na carga de trabalho embutida, contida no elemento **EventString** .  
  
## <a name="see-also"></a>Consulte também  
 [Iniciar e usar o Orientador de Otimização do Mecanismo de Banco de Dados](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)   
 [Exibir e trabalhar com a saída do Orientador de Otimização do Mecanismo de Banco de Dados](../../relational-databases/performance/view-and-work-with-the-output-from-the-database-engine-tuning-advisor.md)   
 [Referência do arquivo de entrada XML &#40;Orientador de Otimização do Mecanismo de Banco de Dados&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
