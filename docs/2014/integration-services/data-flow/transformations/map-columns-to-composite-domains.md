---
title: Mapear colunas para domínios de composição | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: d9422412-8a3d-45ae-af7f-072c902a09ba
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 5b826b771944bb70a97ad116b4c55258a106ec52
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85430303"
---
# <a name="map-columns-to-composite-domains"></a>Mapear colunas para domínios compostos
  Um domínio composto consiste em dois ou mais domínios únicos. Você pode mapear várias colunas para o domínio, ou pode mapear uma única coluna com valores limitados para o domínio.  
  
 Quando você tiver várias colunas, deverá mapear uma coluna para cada domínio único no domínio composto para aplicar as regras do domínio composto para a limpeza de dados. Selecione os domínios únicos contidos no domínio composto, no Cliente Data Quality. Para obter mais informações, consulte [Criar um domínio composto](../../../data-quality-services/create-a-composite-domain.md).  
  
 Quando você tiver uma única coluna com valores limitados, deverá mapear a única coluna para o domínio composto. Os valores devem aparecer na mesma ordem que os domínios únicos aparecem no domínio composto. O delimitador na fonte de dados deve corresponder ao delimitador usado para analisar os valores do domínio composto. Você seleciona o delimitador para o domínio composto, bem como define outras propriedades, no Cliente Data Quality. Para obter mais informações, consulte [Criar um domínio composto](../../../data-quality-services/create-a-composite-domain.md).  
  
### <a name="to-map-multiple-columns-to-a-composite-domain"></a>Para mapear várias colunas para um domínio composto  
  
1.  Clique com o botão direito do mouse na transformação Limpeza DQS e clique em **Editar**.  
  
2.  Na guia **Gerenciador de Conexões** , confirme se o domínio composto é exibido na lista de domínios disponíveis.  
  
3.  Na guia **Mapeamento** , selecione as colunas na área **Colunas de Entrada Disponíveis** .  
  
4.  Para cada coluna listada no campo **Coluna de Entrada** , selecione um domínio único no campo **Domínio** . Selecione somente domínios únicos que estão no domínio composto.  
  
5.  Quando necessário, modifique os nomes que aparecem nos campos **Alias de Origem**, **Alias de Saída**e **Alias de Status** .  
  
6.  Conforme o necessário, defina as propriedades na guia **Avançado** . Para obter mais informações sobre as propriedades, consulte [DQS Cleansing Transformation Editor Dialog Box](../../dqs-cleansing-transformation-editor-dialog-box.md).  
  
### <a name="to-map-a-column-with-delimited-values-to-a-composite-domain"></a>Para mapear uma coluna com valores delimitados para um domínio composto  
  
1.  Clique com o botão direito do mouse na transformação Limpeza DQS e clique em **Editar**.  
  
2.  Na guia **Gerenciador de Conexões** , confirme se o domínio composto é exibido na lista de domínios disponíveis.  
  
3.  Na guia **Mapeamento** , selecione a coluna na área **Colunas de Entrada Disponíveis** .  
  
4.  Para a coluna listada no campo **Coluna de Entrada** , selecione o domínio composto no campo **Domínio** .  
  
5.  Quando necessário, modifique os nomes que aparecem nos campos **Alias de Origem**, **Alias de Saída**e **Alias de Status** .  
  
6.  Conforme o necessário, defina as propriedades na guia **Avançado** . Para obter mais informações sobre as propriedades, consulte [DQS Cleansing Transformation Editor Dialog Box](../../dqs-cleansing-transformation-editor-dialog-box.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Transformação Limpeza DQS](dqs-cleansing-transformation.md)  
  
  
