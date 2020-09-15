---
description: Caixa de diálogo Ordenação (Ferramentas de Banco de Dados Visual)
title: Caixa de diálogo Ordenação
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.dlgbox.definecolumncollation
- vdtsql.chm:65561
ms.assetid: e4020f79-7abf-4839-b9b2-984ef7049817
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: c1e4c82b90c9b3c569f9f179ed16242c4ca76f40
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88314652"
---
# <a name="collation-dialog-box-visual-database-tools"></a>Caixa de diálogo Ordenação (Ferramentas de Banco de Dados Visual)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
Essa caixa de diálogo lhe permite especificar uma sequência de ordenação para a coluna. A sequência de ordenação de uma coluna é usada em qualquer operação que compare os valores da coluna com os de outra coluna ou com valores constantes. Isso também afeta o comportamento de algumas funções de cadeia de caracteres, como SUBSTRING e CHARINDEX. Para uma lista completa dos efeitos da configuração de ordenação de uma coluna, consulte a documentação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
Essa caixa de diálogo aparece:  
  
-   Se você digitar um nome de ordenação inválido no campo **Ordenação** na guia **Propriedades de Coluna**.  
  
-   Quando você clica no campo **Ordenação** na guia **Propriedades de Coluna** e, em seguida, clica no botão de reticências ( **…** ) à direita do campo.  
  
## <a name="options"></a>Opções  
**Ordenação SQL**  
Escolha na lista suspensa as sequências de ordenação definidas pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
**Ordenação do Windows**  
Escolha na lista suspensa as sequências de ordenação definidas pelo Windows.  
  
**Classificação binária**  
Use os códigos binários de valores de caractere para comparações. Se você selecionar essa opção, certas opções de comparação alfabéticas não estarão mais disponíveis. Por exemplo, comparações que não diferenciam maiúsculas de minúsculas ficam indisponíveis porque letras maiúsculas e letras minúsculas têm codificações binárias diferentes. Aplicável apenas se você selecionar **Ordenação do Windows**.  
  
**Classificação do Dicionário**  
Use opções de comparação alfabéticas. Aplicável apenas se você selecionar **Ordenação do Windows**. As opções de comparação alfabéticas são:  
  
-   Selecione**Diferenciar Maiúsculas de Minúsculas** se quiser que as comparações considerem letras maiúsculas e letras minúsculas de forma diferente.  
  
-   Selecione**Diferenciar Acento** se quiser que as comparações considerem letras com e sem acento de forma diferente. Ao selecione essa opção, as comparações também irão considerar de forma diferente letras com acento diferente.  
  
-   Selecione**Diferenciar Katakana** se quiser que as comparações considerem de forma diferente sílabas japonesas katakana e hiragana.  
  
-   Selecione**Diferenciar Largura** se quiser que as comparações considerem de forma diferente caracteres de meia largura e de largura inteira.  
  
**Botão Restaurar padrão**  
Aplica à coluna a ordenação padrão para o banco de dados.  
  
## <a name="see-also"></a>Consulte Também  
[Trabalhar com colunas em consultas de agregação &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/work-with-columns-in-aggregate-queries-visual-database-tools.md)  
  
