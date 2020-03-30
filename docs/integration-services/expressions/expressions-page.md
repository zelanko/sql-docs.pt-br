---
title: Página expressões | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.expressionspage.f1
helpviewer_keywords:
- Expressions Page dialog box
ms.assetid: c9016ec6-11c1-4ebd-b2a7-0fa6631fd9e4
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 9e3bbe6e788512144211ed35d1cfa8326d8f3ef7
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "71290013"
---
# <a name="expressions-page"></a>Página Expressões

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Use a página **Expressões** para editar as expressões de propriedade e para acessar as caixas de diálogo **Editor de Expressões de Propriedades** e **Construtor de Expressões de Propriedade** .  
  
 Quando o pacote é executado, as expressões de propriedades atualizam os valores das propriedades. As expressões de propriedades são usadas com as propriedades dos pacotes, tarefas, contêiners, gerenciadores de conexões, bem como com alguns componentes do fluxo de dados. As expressões são avaliadas e seus resultados são usados em vez dos valores que você definiu para as propriedades ao configurar o pacote e os objetos do pacote. As expressões podem incluir variáveis e funções bem como operadores que o idioma da expressão fornece. Por exemplo, você pode gerar a linha do assunto para a tarefa Enviar Mensagem concatenando o valor de uma variável que contém a cadeia de caracteres "Previsão do tempo para" e os resultados retornados da função GETDATE() para desenvolver a cadeia de caracteres "Previsão do tempo para 4/5/2006.  
  
 Para saber mais sobre expressões de gravação e como usar expressões de propriedade, consulte [Expressões do Integration Services &#40;SSIS&#41;](../../integration-services/expressions/integration-services-ssis-expressions.md) e [Usar expressões de propriedade em pacotes](../../integration-services/expressions/use-property-expressions-in-packages.md).  
  
## <a name="options"></a>Opções  
 **Expressões (...)**  
 Clique nas reticências para abrir a caixa de diálogo **Editor de Expressões de Propriedade** . Para obter mais informações, consulte [Editor de expressões de propriedade](../../integration-services/expressions/property-expressions-editor.md).  
  
 **\<nome da propriedade>**  
 Clique nas reticências para abrir a caixa de diálogo **Construtor de Expressões** . Para obter mais informações, consulte [Expression Builder](../../integration-services/expressions/expression-builder.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Variáveis do SSIS &#40;Integration Services&#41;](../../integration-services/integration-services-ssis-variables.md)   
 [Variáveis do Sistema](../../integration-services/system-variables.md)   
 [Expressões do SSIS &#40;Integration Services&#41;](../../integration-services/expressions/integration-services-ssis-expressions.md)  
  
  
