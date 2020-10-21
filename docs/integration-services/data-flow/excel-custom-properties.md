---
description: Propriedades personalizadas do Excel
title: Propriedades personalizadas do Excel | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: bdcc72b8-8950-47bd-88bf-5db6d48cc6bf
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 0ad1aa213b09afc77d507b874094122611f96dbf
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92194820"
---
# <a name="excel-custom-properties"></a>Propriedades personalizadas do Excel

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  **Propriedades personalizadas de fontes**  
  
 A origem do Excel tem as propriedades personalizadas e as propriedades comuns a todos os componentes de fluxo de dados.  
  
 A tabela a seguir descreve as propriedades personalizadas da origem do Excel. Todas as propriedades são de leitura/gravação.  
  
|Nome da propriedade|Tipo de Dados|Descrição|  
|-------------------|---------------|-----------------|  
|AccessMode|Integer|O modo usado para acessar o banco de dados. Os valores possíveis são **Abrir Conjunto de Linhas**, **Abrir Conjunto de Linhas da Variável**, **Comando do SQL**e **Comando SQL da Variável**. O valor padrão é **Abrir Conjunto de Linhas**.|  
|CommandTimeOut|Integer|O número de segundos antes de um comando expirar.  Um valor de 0 indica que nunca expirará.<br /><br /> **Observação** : esta propriedade não está disponível no **Editor de Origem do Excel**, mas pode ser definida usando o **Editor Avançado**.|  
|OpenRowset|String|O nome do objeto de banco de dados usado para abrir um conjunto de linhas.|  
|OpenRowsetVariable|String|A variável que contém o nome do objeto de banco de dados usado para abrir um conjunto de linhas.|  
|ParameterMapping|String|O mapeamento de parâmetros no comando SQL para variáveis.|  
|SqlCommand|String|O comando SQL a ser executado.|  
|SqlCommandVariable|String|A variável que contém o comando do SQL a ser executado.|  
  
 A saída e as colunas de saída da origem do Excel não têm nenhuma propriedade personalizada.  
  
 Para obter mais informações, consulte [Origem do Excel](../../integration-services/data-flow/excel-source.md).  
  
 **Propriedades personalizadas de destino**  
  
 O destino Excel tem propriedades personalizadas e propriedades comuns a todos os componentes de fluxo de dados.  
  
 A tabela a seguir descreve as propriedades personalizadas do destino Excel. Todas as propriedades são de leitura/gravação.  
  
|Nome da propriedade|Tipo de Dados|Descrição|  
|-------------------|---------------|-----------------|  
|AccessMode|Inteiro (enumeração)|Um valor que especifica como o destino acessa o seu banco de dados de destino.<br /><br /> Essa propriedade pode ter um dos seguintes valores:<br /><br /> **OpenRowset** (0) – Forneça o nome de uma tabela ou exibição.<br /><br /> **OpenRowset from Variable** (1) – Forneça o nome de uma variável que contém o nome de uma tabela ou exibição.<br /><br /> **OpenRowset Using Fastload** (3) – Forneça o nome de uma tabela ou exibição.<br /><br /> **OpenRowset Using Fastload from Variable** (4) – Forneça o nome de uma variável que contém o nome de uma tabela ou exibição.<br /><br /> **Comando SQL** (2) – Forneça uma instrução SQL.|  
|CommandTimeOut|Integer|O número máximo de segundos em que o comando SQL pode ser executado antes que o tempo limite seja excedido. O valor **0** indica que não há limite de tempo. O valor padrão dessa propriedade é **0**.<br /><br /> Observação: essa propriedade não está disponível no **Editor de Destinos Excel**, mas pode ser definida usando o **Editor Avançado**.|  
|FastLoadKeepIdentity|Booliano|Um valor que especifica se os valores de identidade devem ser copiados quando os dados são carregados. Essa propriedade só está disponível quando uma das opções de carregamento rápido é usada. O valor padrão dessa propriedade é **False**.|  
|FastLoadKeepNulls|Booliano|Um valor que especifica se os valores Nulos devem ser copiados quando os dados são carregados. Essa propriedade só está disponível com uma das opções de carregamento rápido. O valor padrão dessa propriedade é **False**.|  
|FastLoadMaxInsertCommitSize|Integer|Um valor que especifica o tamanho do lote que o destino Excel tenta confirmar durante as operações de carregamento rápido. O valor padrão é **2147483647**. Um valor de **0** indica uma única operação de confirmação após o processamento de todas as linhas.|  
|FastLoadOptions|String|Uma coleção de opções de carregamento rápido. As opções de carregamento rápido incluem o bloqueio de tabelas e a verificação de restrições. É possível especificar uma, ambas ou nenhuma.<br /><br /> Observação: algumas opções dessa propriedade não estão disponíveis no **Editor de Destinos do Excel**, mas podem ser definidas no **Editor Avançado**.|  
|OpenRowset|String|Quando AccessMode é **OpenRowset**, o nome da tabela ou exibição acessada pelo destino Excel.|  
|OpenRowsetVariable|String|Quando AccessMode é **OpenRowset from Variable**, o nome da variável que contém o nome da tabela ou exibição acessada pelo destino Excel.|  
|SqlCommand|String|Quando AccessMode é **Comando SQL**, a instrução Transact-SQL usada pelo destino Excel para especificar as colunas de destino dos dados.|  
  
 A entrada e as colunas de entrada do destino Excel não têm nenhuma propriedade personalizada.  
  
 Para obter mais informações, consulte [Destino do Excel](../../integration-services/data-flow/excel-destination.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Propriedades comuns](./set-the-properties-of-a-data-flow-component.md)  
 [Carregar dados do ou para o Excel com o SSIS (SQL Server Integration Services)](../load-data-to-from-excel-with-ssis.md)
  
