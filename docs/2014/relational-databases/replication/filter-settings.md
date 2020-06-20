---
title: Configurações de filtro | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.monitor.filtersettings.f1
ms.assetid: 1b401d7d-db8a-4ba1-acb1-b8dec14e3311
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: d82d5f38eb460f392f1eb2ed3387ce3d97757db5
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85010577"
---
# <a name="filter-settings"></a>Configurações de Filtro
  A caixa de diálogo **Configurações de Filtro** permite que você defina filtros para grades no Replication Monitor. Por exemplo, para mostrar somente as assinaturas ativas na guia **Todas as Assinaturas** , selecione **Status** na coluna **Nome da Coluna** , **Igual** na coluna **Operador** e **Ativo** na coluna **Value1** . Depois de definir um filtro com base em uma ou mais colunas, o filtro é aplicado para que a grade exiba somente o subconjunto de linhas que corresponda aos critérios do filtro.  
  
## <a name="options"></a>Opções  
 **Nome da Coluna**  
 Selecione o nome da coluna na qual você pretende aplicar o filtro. Você pode basear um filtro em uma ou mais colunas.  
  
 **Operador**  
 Selecione um operador para o filtro, como **Menor que ou Igual a**.  
  
 **Value1** e **Value2**  
 Insira ou selecione um valor para o filtro. A maioria dos operadores só exige um valor na coluna **Value1** , mas os operadores **Entre** e **Não Entre** também requerem um valor na coluna **Value2** .  
  
 **Limpar Filtro**  
 Clique neste botão para limpar todos os filtros definidos. Para remover um único filtro, selecione a linha do filtro e pressione a tela Delete.  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorando a Replicação](monitoring-replication.md)  
  
  
