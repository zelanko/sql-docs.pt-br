---
title: Comparar soluções de script e objetos personalizados | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- managed tasks [Integration Services]
- Script task [Integration Services], vs. custom managed tasks
- SSIS Script task, vs. custom managed tasks
- custom tasks [Integration Services], scripts
ms.assetid: c0aea822-a21e-44e1-a3d3-8777bd0a1c34
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ba27959fa5c98b26bd6dc4fdf60d695829c7382d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47653416"
---
# <a name="comparing-scripting-solutions-and-custom-objects"></a>Comparando soluções de script e objetos personalizados
  Uma tarefa Script ou componente Script do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] pode implementar muitas das funcionalidades possíveis em uma tarefa gerenciada personalizada ou em um componente de fluxo de dados. Eis algumas considerações para ajudar você a escolher o tipo apropriado de tarefa para suas necessidades:  
  
-   Se a configuração ou funcionalidade for específica de um pacote individual, use a tarefa Script ou o componente Script em vez de desenvolver um objeto personalizado.  
  
-   Se a funcionalidade for genérica e puder ser usada no futuro por outros pacotes e outros desenvolvedores, você deve criar um objeto personalizado em vez de usar uma solução de script. É possível usar um objeto personalizado em qualquer pacote, enquanto que um script só pode ser usado no pacote para o qual foi criado.  
  
-   Se o código for reutilizado dentro do mesmo pacote, você deve pensar em criar um objeto personalizado. Copiar um código de uma tarefa ou componente Script para outro prejudica a manutenção, pois fica mais difícil manter e atualizar múltiplas cópias do código.  
  
-   Se a implementação tiver que ser alterada com o passar do tempo, pense em usar um objeto personalizado. Objetos personalizados podem ser desenvolvidos e implantados separadamente do pacote pai, enquanto uma atualização feita em uma solução de script requer a reimplantação de todo o pacote.  
  
## <a name="see-also"></a>Consulte Também  
 [Estendendo pacotes com objetos personalizados](../../integration-services/extending-packages-custom-objects/extending-packages-with-custom-objects.md)  
  
  
