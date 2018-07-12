---
title: Caixa de diálogo de propriedades de Conexão (SSAS - Tabular) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.asvs.ssmsimbi.ConnectionProperties.F1
ms.assetid: 17bae8ae-2ba0-4978-be70-61c687f59d54
caps.latest.revision: 6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 29871222a68b9babfb2abd5b2d477316c1d6ac34
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37157237"
---
# <a name="connection-properties-dialog-box-ssas---tabular"></a>Caixa de diálogo Propriedades da Conexão (SSAS – Tabular)
  Use esta página para exibir ou modificar no SQL Server Management Studio as propriedades de conexão de uma fonte de dados usada por um banco de dados modelo de tabela.  
  
 Esta caixa de diálogo fornece carimbos de data/hora e outras informações descritivas, mais propriedades personalizáveis que determinam as características da conexão.  
  
## <a name="options"></a>Opções  
  
|Termo|Definição|  
|----------|----------------|  
|**Nome**|Especifica o nome da fonte de dados.|  
|**ID**|Exibe o identificador do objeto de fonte de dados.|  
|**Descrição**|Exibe a descrição do objeto de fonte de dados.|  
|**Criar Carimbo de Data/Hora**|Exibe a data e a hora de criação do banco de dados.|  
|**Última Atualização de Esquema**|Exibe a data e a hora da última atualização dos metadados do banco de dados.|  
|**Cadeia de Conexão**|Exibe a cadeia de conexão que é usada para conectar-se à fonte de dados que fornece dados ao modelo.|  
|**Número máximo de conexões**|Especifica o número máximo de conexões cliente com esse banco de dados.|  
|**Isolamento**|Os valores válidos são ReadCommitted ou Snapshot. Para obter mais informações, consulte [Elemento Isolation &#40;ASSL&#41;](scripting/properties/isolation-element-assl.md).|  
|**Tempo-limite da consulta**|Especifica a hora, em segundos, depois da qual a tentativa de recuperar dados se esgota.|  
|**Provedor Gerenciado**|Especifica o nome do provedor gerenciado. Se a conexão da fonte de dados usar um provedor OLE DB nativo, esse valor será vazio.|  
|**Informações sobre Representação**|Especifica a conta de representação usada para conexões de banco de dados durante o processamento ou a atualização de dados, consultas executadas em um repositório de dados relacional (via DirectQuery), associações fora de linha, partições remotas e sincronização de banco de dados do destino para a origem.<br /><br /> Os valores válidos incluem a conta de serviço do Analysis Services ou um conjunto específico de credenciais do Windows. Não especifique **Usar as credenciais do usuário atual** ou **Herdar**. Não há suporte para essas opções de credencial para um banco de dados modelo de tabela.|  
  
  
