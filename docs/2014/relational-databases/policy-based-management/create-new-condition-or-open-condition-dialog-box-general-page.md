---
title: Caixa de diálogo Criar Nova Condição ou Abrir Condição, Página Geral | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql12.swb.dmf.condition.f1
ms.assetid: 106954bf-e4ba-412b-9c1a-907d06153dcd
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 296cdebc8a7a290cf8cdd848359ad776fa290c30
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52798288"
---
# <a name="create-new-condition-or-open-condition-dialog-box-general-page"></a>Caixa de diálogo Criar Nova Condição ou Abrir Condição, Página Geral
  Use esta caixa de diálogo para criar ou alterar uma condição de Gerenciamento Baseado em Políticas. A condição é uma expressão Booleana que especifica um conjunto de estados permitidos de um destino gerenciado pelo Gerenciamento Baseado em Políticas em relação às facetas. As propriedades que podem ser selecionadas na caixa **Expressão/Campo** dependem da faceta usada. Para obter mais informações sobre como condições se relacionam às facetas e às políticas, veja [Administrar servidores usando o Gerenciamento Baseado em Políticas](administer-servers-by-using-policy-based-management.md).  
  
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
  
 **Value**  
 A configuração de valor dessa expressão. Os valores permitidos dependem da faceta. Os valores podem ser TRUE/FALSE, cadeia de caracteres ou numéricos. Valores de cadeia de caracteres devem ser colocados entre aspas simples, por exemplo: **'AdventureWorks'**. Nem todos os operadores estão disponíveis para algumas propriedades.  
  
## <a name="group-clauses"></a>Agrupar Cláusulas  
 As cláusulas podem ser agrupadas para operar como uma única unidade separada do restante da consulta, assim como se coloca uma expressão entre parênteses em uma equação matemática ou uma instrução lógica. O agrupamento de cláusulas é útil quando você está criando consultas complexas.  
  
 **Para agrupar cláusulas**  
  
-   Pressione a tecla SHIFT ou CTRL e clique em duas ou mais cláusulas para selecionar um intervalo. Clique com o botão direito do mouse na área selecionada e clique em **Agrupar Cláusulas**.  
  
## <a name="see-also"></a>Consulte também  
 [Administrar servidores com Gerenciamento Baseado em Políticas](administer-servers-by-using-policy-based-management.md)  
  
  
