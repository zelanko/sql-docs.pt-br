---
title: Propriedades personalizadas do Excel | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: bdcc72b8-8950-47bd-88bf-5db6d48cc6bf
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: e7d5c7df84ed001aa969f3fb164fa9691670fc3e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36009601"
---
# <a name="excel-custom-properties"></a>Propriedades personalizadas do Excel
  **Propriedades personalizadas de fontes**  
  
 A origem do Excel tem as propriedades personalizadas e as propriedades comuns a todos os componentes de fluxo de dados.  
  
 A tabela a seguir descreve as propriedades personalizadas da origem do Excel. Todas as propriedades são de leitura/gravação.  
  
|Nome da propriedade|Tipo de Dados|Description|  
|-------------------|---------------|-----------------|  
|AccessMode|Integer|O modo usado para acessar o banco de dados. Os valores possíveis são **Open Rowset**, **abrir conjunto de linhas de variável**, `SQL Command`, e **comando SQL da variável**. O valor padrão é **Abrir Conjunto de Linhas**.|  
|CommandTimeOut|Integer|O número de segundos antes de um comando expirar.  Um valor de 0 indica que nunca expirará.<br /><br /> **Observação** : esta propriedade não está disponível no **Editor de Origem do Excel**, mas pode ser definida usando o **Editor Avançado**.|  
|OpenRowset|Cadeia de caracteres|O nome do objeto de banco de dados usado para abrir um conjunto de linhas.|  
|OpenRowsetVariable|Cadeia de caracteres|A variável que contém o nome do objeto de banco de dados usado para abrir um conjunto de linhas.|  
|ParameterMapping|Cadeia de caracteres|O mapeamento de parâmetros no comando SQL para variáveis.|  
|SqlCommand|Cadeia de caracteres|O comando SQL a ser executado.|  
|SqlCommandVariable|Cadeia de caracteres|A variável que contém o comando do SQL a ser executado.|  
  
 A saída e as colunas de saída da origem do Excel não têm nenhuma propriedade personalizada.  
  
 Para obter mais informações, consulte [Origem do Excel](excel-source.md).  
  
 **Propriedades personalizadas de destino**  
  
 O destino Excel tem propriedades personalizadas e propriedades comuns a todos os componentes de fluxo de dados.  
  
 A tabela a seguir descreve as propriedades personalizadas do destino Excel. Todas as propriedades são de leitura/gravação.  
  
|Nome da propriedade|Tipo de Dados|Description|  
|-------------------|---------------|-----------------|  
|AccessMode|Inteiro (enumeração)|Um valor que especifica como o destino acessa o seu banco de dados de destino.<br /><br /> Essa propriedade pode ter um dos seguintes valores:<br /><br /> `OpenRowset` (0) — você fornecer o nome de uma tabela ou exibição.<br /><br /> `OpenRowset from Variable` (1) — você fornecer o nome de uma variável que contém o nome de uma tabela ou exibição.<br /><br /> `OpenRowset Using Fastload` (3) — Você fornece o nome de uma tabela ou exibição.<br /><br /> `OpenRowset Using Fastload from Variable` (4) — você fornecer o nome de uma variável que contém o nome de uma tabela ou exibição.<br /><br /> `SQL Command` (2) — Você fornece uma instrução SQL.|  
|CommandTimeOut|Integer|O número máximo de segundos em que o comando SQL pode ser executado antes que o tempo limite seja excedido. O valor **0** indica que não há limite de tempo. O valor padrão dessa propriedade é **0**.<br /><br /> Observação: essa propriedade não está disponível no **Editor de Destinos Excel**, mas pode ser definida usando o **Editor Avançado**.|  
|FastLoadKeepIdentity|Booliano|Um valor que especifica se os valores de identidade devem ser copiados quando os dados são carregados. Essa propriedade só está disponível quando uma das opções de carregamento rápido é usada. O valor padrão dessa propriedade é **False**.|  
|FastLoadKeepNulls|Booliano|Um valor que especifica se os valores Nulos devem ser copiados quando os dados são carregados. Essa propriedade só está disponível com uma das opções de carregamento rápido. O valor padrão dessa propriedade é **False**.|  
|FastLoadMaxInsertCommitSize|Integer|Um valor que especifica o tamanho do lote que o destino Excel tenta confirmar durante as operações de carregamento rápido. O valor padrão é **2147483647**. Um valor de **0** indica uma única operação de confirmação após o processamento de todas as linhas.|  
|FastLoadOptions|Cadeia de caracteres|Uma coleção de opções de carregamento rápido. As opções de carregamento rápido incluem o bloqueio de tabelas e a verificação de restrições. É possível especificar uma, ambas ou nenhuma.<br /><br /> Observação: algumas opções dessa propriedade não estão disponíveis no **Editor de Destinos do Excel**, mas podem ser definidas no **Editor Avançado**.|  
|OpenRowset|Cadeia de caracteres|Quando AccessMode é `OpenRowset`, o nome da tabela ou exibição acessada pelo destino Excel.|  
|OpenRowsetVariable|Cadeia de caracteres|Quando AccessMode é `OpenRowset from Variable`, o nome da variável que contém o nome da tabela ou exibição acessada pelo destino Excel.|  
|SqlCommand|Cadeia de caracteres|Quando AccessMode é `SQL Command`, a instrução Transact-SQL que usa o destino do Excel para especificar as colunas de destino para os dados.|  
  
 A entrada e as colunas de entrada do destino Excel não têm nenhuma propriedade personalizada.  
  
 Para obter mais informações, consulte [Destino do Excel](excel-destination.md).  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades comuns](../common-properties.md)  
  
  