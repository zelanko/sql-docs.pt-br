---
title: Argumentos de ferramentas externas | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- arguments [SQL Server Management Studio]
- external tools [SQL Server Management Studio]
ms.assetid: 3991c13a-f23f-450b-a2ba-19391c399735
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 514b5f4e9e5df63f745e7f2e6a9465cddd6c4628
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="arguments-for-external-tools"></a>Arguments for External Tools
Argumentos são variáveis para as quais o ambiente do Studio fornece valores para quando uma ferramenta externa é iniciada no menu **Ferramentas** . Ferramentas externas, como o Bloco de Notas, podem ser adicionadas ao menu **Ferramentas** que usa a caixa de diálogo **Ferramentas Externas** .  
  
A tabela a seguir relaciona os argumentos de ferramentas externas.  
  
|Nome|Argumento|Description|  
|--------|------------|---------------|  
|**Caminho de item**|$(ItemPath)|O nome completo do arquivo da fonte atual (definido como unidade + caminho + nome de arquivo). Em branco se estiver ativa uma janela que não seja de fonte.|  
|**Diretório do item**|$(ItemDir)|O diretório da fonte atual (definido como unidade + caminho). Em branco se estiver ativa uma janela que não seja de fonte.|  
|**Nome de arquivo de item**|$(ItemFilename)|O nome do arquivo da fonte atual (definido como nome de arquivo). Em branco se estiver ativa uma janela que não seja de fonte.|  
|**Extensão de item**|$(ItemExt)|A extensão do nome de arquivo da fonte atual.|  
|**Linha atual***|$(CurLine)|A posição da linha atual do cursor no editor.|  
|**Coluna atual***|$(CurCol)|A posição da coluna atual do cursor no editor.|  
|**Texto atual***|$(CurText)|O texto atual (a palavra debaixo da posição do cursor atual ou uma seleção de linha única, se houver uma).|  
|**Caminho de destino**|$(TargetPath)|O nome de arquivo completo do destino (definido como unidade + caminho + nome de arquivo).|  
|**Diretório de destino**|$(TargetDir)|O diretório do destino.|  
|**Nome de destino**|$(TargetName)|O nome do arquivo do destino.|  
|**Extensão de destino**|$(TargetExt)|A extensão do nome do arquivo de destino.|  
|**Diretório do projeto**|$(ProjDir)|O diretório do projeto atual (definido como unidade + caminho).|  
|**Nome de arquivo do projeto**|$(ProjFileName)|O nome de arquivo do projeto atual (definido como unidade + caminho + nome de arquivo).|  
|**Diretório da solução**|$(SolutionDir)|O diretório da solução atual (definido como unidade + caminho).|  
|**Nome de arquivo da solução**|$(SolutionFileName)|O nome de arquivo da solução atual (definido como unidade + caminho + nome de arquivo).|  
  
*A linha atual, a coluna atual ou o texto atual se baseia na posição do cursor no editor de texto conforme mostrado na barra de status.  
  
## <a name="see-also"></a>Consulte também  
[Caixa de diálogo Ferramentas Externas](../ssms/external-tools-dialog-box.md)  
[Elementos gerais da interface de usuário](../ssms/general-user-interface-elements.md)  
  

