---
title: Visualizador de Dados | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: data-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.dts.designer.dataviewer.f1
helpviewer_keywords:
- Data Viewer dialog box
ms.assetid: 6351309a-688f-4e82-9697-1712130f10a1
caps.latest.revision: 13
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6566c459be7b1e1fb128befacc471129c2dcfcc2
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="data-viewer"></a>Visualizador de Dados
  Se um caminho for configurado para usar um visualizador de dados, o Visualizador de Dados exibirá o buffer de dados por buffer à medida que os dados se movimentarem entre dois componentes de fluxo de dados.  
  
## <a name="options"></a>Opções  
 **Seta Verde**  
 Clique para exibir os dados do próximo buffer. Se os dados puderem ser movidos em um único buffer, esta opção não estará disponível.  
  
 **Desanexar**  
 Desanexe o visualizador de dados.  
  
 **Observação** Desanexar um visualizador de dados não exclui o visualizador de dados. Se o visualizador de dados foi desanexado, os dados continuarão fluindo pelo caminho, mas os dados no visualizador não são atualizados para corresponder aos dados em cada buffer.  
  
 **Anexar**  
 Anexe um visualizador de dados.  
  
 **Observação** Quando o visualizador de dados é anexado, ele exibe informações de cada buffer no fluxo de dados e, em seguida, pausa. Você pode avançar pelos buffers usando a seta verde.  
  
 **Copiar Dados**  
 Copie os dados no buffer atual para a Área de Transferência.  
  
## <a name="see-also"></a>Consulte Também  
 [Depurar o fluxo de dados](../../integration-services/troubleshooting/debugging-data-flow.md)  
  
  
