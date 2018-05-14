---
title: Linguagem de script (TMSL) de comandos na tabela modelo | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tmsl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9c36ba09aa19aa8abc1c21ea8c870dbfe2d24c9e
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="tmsl-reference---commands"></a>Referência TMSL - comandos
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Você pode executar comandos em um ponto de extremidade do XMLA, formular definições de objeto em JSON usando o modelo de script TMSL (linguagem tabela), nos bancos de dados de modelo de tabela.   Consulte [definições de objeto na linguagem de script de modelo de tabela &#40;TMSL&#41; ](../../analysis-services/tabular-models-scripting-language-objects/tmsl-reference-tabular-objects.md) para obter uma lista de objetos usados com os comandos a seguir.  
  
## <a name="object-operations"></a>Operações de objeto  
  
|||  
|-|-|  
|[Comando ALTER &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/alter-command-tmsl.md)|Faça as modificações de embutido para um objeto sem a necessidade de especificar a definição completa.|  
|[Criar um comando &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/create-command-tmsl.md)|Cria um novo objeto, incluindo seus descendentes.|  
|[Comando CreateOrReplace &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl.md)|Criar ou substituir partes de uma definição de objeto. A definição completa deve ser fornecida.|  
|[Comando Delete &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/delete-command-tmsl.md)|Exclua um objeto, incluindo seus descendentes.|  
  
## <a name="data-refresh-operations"></a>Operações de atualização de dados  
  
|||  
|-|-|  
|[Comando MergePartitions &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/mergepartitions-command-tmsl.md)|Mesclar uma partição de destino em uma fonte e, em seguida, exclua o destino.|  
|[Comando Refresh &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/refresh-command-tmsl.md)|Processe um banco de dados, tabela ou partição.|  
  
## <a name="scripting"></a>Script  
  
|||  
|-|-|  
|[Sequência de comando &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/sequence-command-tmsl.md)|Operações em lotes em sequência ou em paralelo|  
  
## <a name="database-management-operations"></a>Operações de gerenciamento de banco de dados  
  
|||  
|-|-|  
|[O comando attach &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/attach-command-tmsl.md)|Adiciona um arquivo para o servidor.|  
|[Comando Detach &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/detach-command-tmsl.md)|Remove um arquivo de servidores.|  
|[Comando de backup &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/backup-command-tmsl.md)|Cria um arquivo de backup de um banco de dados.|  
|[Comando Restore &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/restore-command-tmsl.md)|Restaura o banco de dados para o servidor.|  
|[Comando Synchronize &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/synchronize-command-tmsl.md)|Sincroniza um banco de dados do Analysis Services com outro banco de dados existente.|  
  
## <a name="see-also"></a>Consulte também  
 [Referência de TMSL &#40;Linguagem de Scripts de Modelo de Tabela&#41;](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)   
 [Instalar provedores de dados do Analysis Services &#40;AMO, ADOMD.NET, MSOLAP&#41;](../../analysis-services/instances/install-windows/install-analysis-services-data-providers-amo-adomd-net-msolap.md)   
 [Nível de compatibilidade para modelos de tabela no Analysis Services](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)  
  
  
