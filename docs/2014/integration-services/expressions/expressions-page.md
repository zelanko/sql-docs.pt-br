---
title: Página expressões | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.expressionspage.f1
helpviewer_keywords:
- Expressions Page dialog box
ms.assetid: c9016ec6-11c1-4ebd-b2a7-0fa6631fd9e4
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ba4e73ea495456e8f9e452108ab09106a65543ae
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85428713"
---
# <a name="expressions-page"></a>Página Expressões
  Use a página **Expressões** para editar as expressões de propriedade e para acessar as caixas de diálogo **Editor de Expressões de Propriedades** e **Construtor de Expressões de Propriedade** .  
  
 Quando o pacote é executado, as expressões de propriedades atualizam os valores das propriedades. As expressões de propriedades são usadas com as propriedades dos pacotes, tarefas, contêiners, gerenciadores de conexões, bem como com alguns componentes do fluxo de dados. As expressões são avaliadas e seus resultados são usados em vez dos valores que você definiu para as propriedades ao configurar o pacote e os objetos do pacote. As expressões podem incluir variáveis e funções bem como operadores que o idioma da expressão fornece. Por exemplo, você pode gerar a linha do assunto para a tarefa Enviar Mensagem concatenando o valor de uma variável que contém a cadeia de caracteres "Previsão do tempo para" e os resultados retornados da função GETDATE() para desenvolver a cadeia de caracteres "Previsão do tempo para 4/5/2006.  
  
 Para saber mais sobre expressões de gravação e como usar expressões de propriedade, consulte [Expressões do Integration Services &#40;SSIS&#41;](integration-services-ssis-expressions.md) e [Usar expressões de propriedade em pacotes](use-property-expressions-in-packages.md).  
  
## <a name="options"></a>Opções  
 **Expressões (...)**  
 Clique nas reticências para abrir a caixa de diálogo **Editor de Expressões de Propriedade** . Para obter mais informações, consulte [Editor de expressões de propriedade](property-expressions-editor.md).  
  
 **\<property name>**  
 Clique nas reticências para abrir a caixa de diálogo **Construtor de Expressões** . Para obter mais informações, consulte [Expression Builder](expression-builder.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Integration Services &#40;as variáveis&#41; SSIS](../integration-services-ssis-variables.md)   
 [Variáveis do sistema](../system-variables.md)   
 [Expressões do SSIS &#40;Integration Services&#41;](integration-services-ssis-expressions.md)  
  
  
