---
title: Tabela de modelagem (SSAS Tabular) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 80027288-c203-4667-a3e1-40fa572b4975
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: df693d141f3a91c1c0b9b023a89d39c5f2c171ce
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36021014"
---
# <a name="tabular-modeling-ssas-tabular"></a>Modelagem tabular (SSAS tabular)
  Modelos tabulares são bancos de dados de memória no Analysis Services. Usando algoritmos de compactação de última geração e processador de consulta multi-threaded, o mecanismo analítico na memória xVelocity (VertiPaq) entrega acesso rápido a objetos e dados modelo tabular relatando aplicativos clientes como o Microsoft Excel e o Microsoft [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)].  
  
 Modelos tabulares dão suporte a acesso a dados por meio de dois modos: modo armazenado em cache e modo DirectQuery. No modo armazenado em cache, você pode integrar dados de várias origens inclusive bancos de dados relacionais, feeds de dados e arquivos de texto planos. No modo DirectQuery, você pode ignorar o modelo de memória, permitindo que aplicativos cliente consultem dados diretamente na origem (SQL Server relacional).  
  
 Os modelos tabulares são criados no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] usando novos modelos de projeto de modelo tabular. Você pode importar dados de várias origens e enriquecer o modelo adicionando relações, colunas calculadas, medidas, KPIs e hierarquias. Modelos podem ser implantados a uma instância do Analysis Services onde os aplicativos de relatório de cliente podem conectar-se a eles. Os modelos implantados podem ser gerenciados n SQL Server Management Studio da mesma forma que modelos multidimensionais. Eles também podem ser particionados para processamento otimizado e protegido no nível de linha usando segurança baseada em função.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Soluções de modelo tabular &#40;Tabular do SSAS&#41;](../tabular-model-solutions-ssas-tabular.md)  
  
 [Bancos de dados de modelo de tabela &#40;Tabular do SSAS&#41;](tabular-model-databases-ssas-tabular.md)  
  
 [Acesso a dados de modelo de tabela](tabular-model-data-access.md)  
  
  