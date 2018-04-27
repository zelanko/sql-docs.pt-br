---
title: Caixa de diálogo Agrupamento (Ferramentas de Banco de Dados Visual) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-visual-db
ms.reviewer: ''
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vdt.dlgbox.definecolumncollation
- vdtsql.chm:65561
ms.assetid: e4020f79-7abf-4839-b9b2-984ef7049817
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3f5efc3b29f6ecf3f66b170524eeba41d235f39e
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="collation-dialog-box-visual-database-tools"></a>Caixa de diálogo Agrupamento (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Essa caixa de diálogo lhe permite especificar uma sequência de agrupamento para a coluna. A sequência de agrupamento de uma coluna é usada em qualquer operação que compare os valores da coluna com os de outra coluna ou com valores constantes. Isso também afeta o comportamento de algumas funções de cadeia de caracteres, como SUBSTRING e CHARINDEX. Para uma lista completa dos efeitos da configuração de agrupamento de uma coluna, consulte a documentação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] .  
  
Essa caixa de diálogo aparece:  
  
-   Se você digitar um nome de agrupamento inválido no campo **Agrupamento** na guia **Propriedades de Coluna** .  
  
-   Se você clicar no campo **Agrupamento** na guia **Propriedades de Coluna** e clicar no botão de reticências (**…**) à direita do campo.  
  
## <a name="options"></a>Opções  
**Agrupamento SQL**  
Escolha na lista suspensa as sequências de agrupamento definidas pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] .  
  
**Agrupamento do Windows**  
Escolha na lista suspensa as sequências de agrupamento definidas pelo Windows.  
  
**Classificação binária**  
Use os códigos binários de valores de caractere para comparações. Se você selecionar essa opção, certas opções de comparação alfabéticas não estarão mais disponíveis. Por exemplo, comparações que não diferenciam maiúsculas de minúsculas ficam indisponíveis porque letras maiúsculas e letras minúsculas têm codificações binárias diferentes. Aplicável apenas se você selecionar **Agrupamento do Windows**.  
  
**Classificação do Dicionário**  
Use opções de comparação alfabéticas. Aplicável apenas se você selecionar **Agrupamento do Windows**. As opções de comparação alfabéticas são:  
  
-   Selecione**Diferenciar Maiúsculas de Minúsculas** se quiser que as comparações considerem letras maiúsculas e letras minúsculas de forma diferente.  
  
-   Selecione**Diferenciar Acento** se quiser que as comparações considerem letras com e sem acento de forma diferente. Ao selecione essa opção, as comparações também irão considerar de forma diferente letras com acento diferente.  
  
-   Selecione**Diferenciar Katakana** se quiser que as comparações considerem de forma diferente sílabas japonesas katakana e hiragana.  
  
-   Selecione**Diferenciar Largura** se quiser que as comparações considerem de forma diferente caracteres de meia largura e de largura inteira.  
  
**Botão Restaurar padrão**  
Aplica à coluna o agrupamento padrão para o banco de dados.  
  
## <a name="see-also"></a>Consulte Também  
[Trabalhar com colunas em consultas de agregação &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/work-with-columns-in-aggregate-queries-visual-database-tools.md)  
  
