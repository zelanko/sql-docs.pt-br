---
title: "'Página Geral' da caixa de diálogo 'Criar Condição' ou 'Abrir Condição'"
description: Descreve a 'Página Geral' da caixa de diálogo 'Criar Condição' ou 'Abrir Condição' para o gerenciamento baseado em políticas do SSMS (SQL Server Management Studio).
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql13.swb.dmf.condition.f1
ms.assetid: 106954bf-e4ba-412b-9c1a-907d06153dcd
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: c16d813af595e3698379026e219440ba0007db12
ms.sourcegitcommit: 035ad9197cb9799852ed705432740ad52e0a256d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/31/2019
ms.locfileid: "75558131"
---
# <a name="create-new-condition-or-open-condition-dialog-box-general-page"></a>Caixa de diálogo Criar Nova Condição ou Abrir Condição, Página Geral
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Use esta caixa de diálogo para criar ou alterar uma condição de Gerenciamento Baseado em Políticas. A condição é uma expressão Booleana que especifica um conjunto de estados permitidos de um destino gerenciado pelo Gerenciamento Baseado em Políticas em relação às facetas. As propriedades que podem ser selecionadas na caixa **Expressão/Campo** dependem da faceta usada. Para obter mais informações sobre como condições se relacionam às facetas e às políticas, veja [Administrar servidores usando o Gerenciamento Baseado em Políticas](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md).  
  
## <a name="options"></a>Opções  
 **Nome**  
 Para uma condição nova, digite o nome da nova condição. Para uma condição existente, o nome será exibido.  
  
 **Faceta**  
 A faceta usada por essa condição.  
  
 **AndOr**  
 Quando você adiciona várias expressões, indica se elas devem ser unidas com **E** ou **Ou**. Permanece em branco quando há somente uma expressão.  
  
 **Campo**  
 Cada faceta expõe uma ou mais propriedades que podem ser definidas. Na caixa campo, selecione uma propriedade na lista de propriedades disponíveis, para criar uma expressão para essa condição.  
  
 **Operador**  
 Selecione um operador de comparação para esta expressão. Os operadores são os seguintes: =, !=, >, >=, <, <=, [NOT]LIKE, [NOT]IN. Nem todos os operadores estão disponíveis para algumas propriedades.  
  
 **Valor**  
 A configuração de valor dessa expressão. Os valores permitidos dependem da faceta. Os valores podem ser TRUE/FALSE, cadeia de caracteres ou numéricos. Os valores da cadeia de caracteres devem ser colocados entre aspas simples, por exemplo: **'AdventureWorks'** . Nem todos os operadores estão disponíveis para algumas propriedades.  
  
## <a name="group-clauses"></a>Agrupar Cláusulas  
 As cláusulas podem ser agrupadas para operar como uma única unidade separada do restante da consulta, assim como se coloca uma expressão entre parênteses em uma equação matemática ou uma instrução lógica. O agrupamento de cláusulas é útil quando você está criando consultas complexas.  
  
 **Para agrupar cláusulas**  
  
-   Pressione a tecla SHIFT ou CTRL e clique em duas ou mais cláusulas para selecionar um intervalo. Clique com o botão direito do mouse na área selecionada e clique em **Agrupar Cláusulas**.  
  
## <a name="see-also"></a>Consulte Também  
 [Administrar servidores com Gerenciamento Baseado em Políticas](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)  
  
  
