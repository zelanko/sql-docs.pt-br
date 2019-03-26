---
title: Visualizador de Dados | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.dataviewer.f1
helpviewer_keywords:
- Data Viewer dialog box
ms.assetid: 6351309a-688f-4e82-9697-1712130f10a1
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8d2232235b1d89384f269edb3a1632f8ff9db067
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/20/2019
ms.locfileid: "58290822"
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
  
  
