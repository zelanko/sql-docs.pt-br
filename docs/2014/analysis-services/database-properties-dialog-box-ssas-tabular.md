---
title: Caixa de diálogo de propriedades (SSAS - tabela) de banco de dados | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.asvs.ssmsimbi.DatabaseProperties.f1
ms.assetid: 0f0ec02f-7b55-40ea-8a04-ed0deb1efd7a
caps.latest.revision: 9
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 142a3eeb8ae135fa27316f4b227f13fc33c77814
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36115129"
---
# <a name="database-properties-dialog-box-ssas---tabular"></a>Caixa de diálogo Propriedades de Banco de Dados (SSAS - Tabela)
  Esta caixa de diálogo fornece carimbos de data/hora e outras informações descritivas, mais propriedades personalizáveis que determinam se o banco de dados usa dados armazenados em cache. Outras propriedades personalizáveis incluem a alteração do nome do banco de dados e a especificação das opções de representação.  
  
## <a name="options"></a>Opções  
  
|Termo|Definição|  
|----------|----------------|  
|**Nome**|**Nome** é o nome do banco de dados que identifica exclusivamente o banco de dados no servidor. Ao alterar o nome de banco de dados, considere o impacto em relatórios e aplicativos cliente que usam o nome atual em cadeias de conexão existentes. Você precisará atualizar as cadeias de conexão nos relatórios existentes para evitar erros de acesso negado. Além disso, o modelo de tabela que é a origem desse banco de dados muito provavelmente usa o nome original. Considere atualizar as propriedades de implantação de banco de dados no modelo para assegurar que as futuras atualizações a esse modelo sejam publicadas no banco de dados pretendido.|  
|**ID**|Exibe o identificador do banco de dados.|  
|**Descrição**|Digite para alterar a descrição do banco de dados.|  
|**Criar Carimbo de Data/Hora**|Exibe a data e a hora de criação do banco de dados.|  
|**Última Atualização de Esquema**|Exibe a data e a hora da última atualização dos metadados do banco de dados.|  
|**Última atualização**|Exibe a data e a hora da última atualização dos dados do banco de dados.|  
|**Modo de leitura / gravação**|Esta é uma propriedade somente leitura, mas você pode alterá-la usando uma sequência de comandos **Detach** e **Attach** , em que a propriedade é um parâmetro do comando **Attach** . Para obter mais informações, consulte [Banco de dados ReadWriteModes](multidimensional-models/database-readwritemodes.md).|  
|**DirectQueryMode**|Especifica se o banco de dados usa apenas o armazenamento na memória (sem armazenamento em disco), apenas o armazenamento em disco ou uma combinação dos dois. Os valores válidos são: InMemory, DirectQuery, InMemoryWithDirectQuery (principalmente baseado na memória com alguma paginação em disco) ou DirectQueryWithInMemory (principalmente baseado em disco com algum armazenamento na memória). Para obter mais informações, consulte [cenários de implantação do DirectQuery &#40;SSAS de tabela&#41;](directquery-deployment-scenarios-ssas-tabular.md).|  
|**Informações de representação de fonte de dados**|Especifica a conta de representação usada para conexões de banco de dados durante o processamento ou a atualização de dados nas partições locais ou remotas consultas executadas em um repositório de dados relacional (via DirectQuery), associações fora de linha e sincronização de banco de dados do destino para a origem.<br /><br /> Os valores válidos incluem a conta de serviço do Analysis Services ou um conjunto específico de credenciais do Windows. Não especifique **Usar as credenciais do usuário atual**. Não há suporte para essa opção de credencial para um banco de dados modelo de tabela.|  
|**Último processamento**|Exibe a data e a hora do último processamento do banco de dados.|  
|**Tamanho estimado**|Exibe o tamanho estimado do banco de dados.|  
|**Local de armazenamento**|Especifica o local do banco de dados. Se o banco de dados for localizado no diretório de Dados padrão, esse valor será vazio.|  
  
  