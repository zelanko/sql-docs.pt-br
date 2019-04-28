---
title: Caixa de diálogo de propriedades de Conexão (SSAS - Tabular) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.ssmsimbi.ConnectionProperties.F1
ms.assetid: 17bae8ae-2ba0-4978-be70-61c687f59d54
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3322b71162b93204591dbb1c0bffb6bac4856454
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62679943"
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
|**Isolamento**|Os valores válidos são ReadCommitted ou Snapshot. Para obter mais informações, consulte [Elemento Isolation &#40;ASSL&#41;](https://docs.microsoft.com/bi-reference/assl/properties/isolation-element-assl).|  
|**Tempo-limite da consulta**|Especifica a hora, em segundos, depois da qual a tentativa de recuperar dados se esgota.|  
|**Provedor Gerenciado**|Especifica o nome do provedor gerenciado. Se a conexão da fonte de dados usar um provedor OLE DB nativo, esse valor será vazio.|  
|**Informações sobre Representação**|Especifica a conta de representação usada para conexões de banco de dados durante o processamento ou a atualização de dados, consultas executadas em um repositório de dados relacional (via DirectQuery), associações fora de linha, partições remotas e sincronização de banco de dados do destino para a origem.<br /><br /> Os valores válidos incluem a conta de serviço do Analysis Services ou um conjunto específico de credenciais do Windows. Não especifique **Usar as credenciais do usuário atual** ou **Herdar**. Não há suporte para essas opções de credencial para um banco de dados modelo de tabela.|  
  
  
