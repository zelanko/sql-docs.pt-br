---
title: Gerenciando um domínio de composição | Microsoft Docs
ms.custom: ''
ms.date: 07/31/2012
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology:
- data-quality-services
ms.topic: conceptual
ms.assetid: 47821eff-800b-4053-8d36-e42bbc267f54
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 959b778d613376197774a01de8efb6fa031cee14
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47621854"
---
# <a name="managing-a-composite-domain"></a>Gerenciando um domínio composto

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Este tópico descreve o uso dos domínios compostos no [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). Às vezes, um domínio único não representa os dados de um campo satisfatoriamente, e você pode representar os dados apenas agrupando domínios únicos. Para fazer isso, crie um domínio composto. Um domínio composto consiste em dois ou mais domínios únicos, e é mapeado para um campo de dados que consiste em vários termos relacionados que não são analisados, mas são incluídos em um valor composto único. Cada termo no valor será representado por um único domínio diferente. Quando você incluir domínios únicos em domínios compostos e mapear o domínio composto para o campo de dados, poderá compilar o conhecimento sobre os dados nesse campo da base de dados de conhecimento, compilando o conhecimento nos domínios únicos. Um domínio composto, assim como um domínio único, é uma representação semântica dos dados em um único campo de dados.  
  
 Os domínios únicos em um domínio composto devem ter uma área comum de conhecimento. Um exemplo é o campo de endereço que tem rua, cidade, estado, país e dados de código postal. Os termos diferentes neste campo podem ter tipos de dados diferentes. Para lidar com isso, você mapeia esses termos para domínios únicos diferentes. Outro exemplo é um campo de nome completo que tem nome, segundo nome e sobrenome. Para usar um domínio composto, você precisa analisar os dados no campo em domínios únicos diferentes, criando um domínio composto para o campo e um domínio único para parte do campo.  
  
 Os domínios compostos têm recursos diferentes dos recursos dos domínios únicos. Você não pode alterar os valores no domínio composto; você deve fazer isso em um domínio único. Com os domínios compostos, você pode usar regras de domínio cruzado para testar os valores nos domínios únicos do domínio composto. Você também pode exibir as combinações de valor encontradas nos domínios compostos.  
  
## <a name="in-this-section"></a>Nesta seção  
 Com um domínio composto, você pode fazer o seguinte:  
  
|||  
|-|-|  
|Crie uma representação semântica para um campo de dados que consiste em vários termos relacionados que não são analisados|[Criar um domínio de composição](../data-quality-services/create-a-composite-domain.md)|  
|Quando você estiver mapeando dados complexos para um domínio composto, poderá analisar os dados com base no conhecimento, além de analisar um delimitador. O DQS tentará primeiro usar seu conhecimento sobre domínios únicos para determinar como as partes da cadeia de caracteres complexa pertencerão aos domínios únicos.|[Criar um domínio de composição](../data-quality-services/create-a-composite-domain.md)|  
|Anexe um serviço de dados de referência, como o que lida com os dados de endereço, a um domínio composto.|[Anexar domínio ou domínio de composição para dados de referência](../data-quality-services/attach-domain-or-composite-domain-to-reference-data.md)|  
|Crie uma regra de domínio cruzado quando o valor de um domínio em um domínio composto afetar o valor de outro.|[Criar uma regra de domínio cruzado](../data-quality-services/create-a-cross-domain-rule.md)|  
|Identifique as combinações de valor para que o DQS possa relatar sua frequência.|[Usar relações de valor em um domínio de composição](../data-quality-services/use-value-relations-in-a-composite-domain.md)|  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Descrição da tarefa|Tópico|  
|----------------------|-----------|  
|Criar uma base de dados de conhecimento executando a descoberta da base de dados de conhecimento e gerenciando o conhecimento de modo interativo|[Criar uma base de dados de conhecimento](../data-quality-services/building-a-knowledge-base.md)|  
|Importar ou exportar conhecimento para/de uma base de dados de conhecimento.|[Importar e exportar conhecimento](../data-quality-services/importing-and-exporting-knowledge.md)|  
|Criar um domínio único e adicionar conhecimento ao domínio.|[Gerenciar um domínio](../data-quality-services/managing-a-domain.md)|  
  
  
