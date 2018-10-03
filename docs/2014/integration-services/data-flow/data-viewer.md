---
title: Visualizador de Dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.dataviewer.f1
helpviewer_keywords:
- Data Viewer dialog box
ms.assetid: 6351309a-688f-4e82-9697-1712130f10a1
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: e4744860e9a220771374863be2bfd4138b2f553f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48156846"
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
  
## <a name="see-also"></a>Consulte também  
 [Depurar o fluxo de dados](../troubleshooting/debugging-data-flow.md)  
  
  
