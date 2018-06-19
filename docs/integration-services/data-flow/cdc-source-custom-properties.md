---
title: Propriedades personalizadas da origem CDC | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 744e9357-94a9-4202-abe8-1d3d202697e9
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d32994082244c755937c5c076d8a4a4ed25aba92
ms.sourcegitcommit: de5e726db2f287bb32b7910831a0c4649ccf3c4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/12/2018
ms.locfileid: "35332400"
---
# <a name="cdc-source-custom-properties"></a>Propriedades personalizadas da origem CDC
  A tabela a seguir descreve as propriedades personalizadas da origem CDC. Todas as propriedades são de leitura/gravação.  
  
|Nome da propriedade|Tipo de Dados|Descrição|  
|-------------------|---------------|-----------------|  
|Conexão|Conexão ADO.Net|Uma conexão ADO.NET com o banco de dados do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] CDC para acesso às tabelas de alterações.|  
|StateVariable|Cadeia de caracteres|Uma variável de pacote de cadeia de caracteres SSIS que mantém o estado CDC da execução CDC atual.|  
|CdcProcessingMode|Inteiro (enumeração)|Esse modo determina como o processamento é tratado. As possíveis opções são **Tudo**, **Tudo com valores antigos**, **Rede**, **Rede com máscara de atualização**e **Rede com mesclagem**.<br /><br /> Modos que iniciam com Tudo retornam todas as alterações e modos que começam com Rede retornam apenas as alterações de rede.<br /><br /> Tabelas sem uma chave primária só podem ter os valores Tudo.<br /><br /> **Rede com Máscara de Atualização** adiciona colunas boolianas com o nome padrão **__$\<nome-da-coluna>\__Changed**, que indica as colunas alteradas na linha de alteração atual.<br /><br /> Para obter informações adicionais sobre os valores dessa propriedade, consulte [Editor de Origem CDC &#40;página Gerenciador de Conexões&#41;](../../integration-services/data-flow/cdc-source-editor-connection-manager-page.md).|  
|CaptureInstance|Cadeia de caracteres|O nome da instância de captura CDC com a tabela CDC a ser lida. Uma tabela de origem capturada pode ter uma ou duas instâncias capturadas para tratar diretamente a transição da definição de tabela por meio de alterações de esquema. Se mais de uma instância de captura for definida para a tabela de origem que está sendo capturada, selecione a instância de captura que você deseja usar aqui. O nome padrão da instância de captura para uma tabela [esquema].[tabela] é \<esquema>_\<tabela>, mas os nomes reais da instância de captura em uso podem ser diferentes. A tabela da qual a leitura é realmente realizada é a tabela CDC **cdc.\<instância-de-captura>_CT**.|  
|ReprocessingIndicator|Booliano|Um valor que especifica se a coluna **__$reprocessing** deve ser adicionada. Essa coluna de saída especial permite ao desenvolvedor SSIS tratar erros de consistência diferentemente ao trabalhar no Intervalo de Processamento Inicial.<br /><br /> Se **true**, a coluna  **__$reprocessing** será adicionada.<br /><br /> Esta coluna será **true** quando o intervalo de processamento CDC sobrepõe o intervalo de processamento inicial (o intervalo de LSNs que corresponde ao período de carga inicial) ou quando um intervalo de processamento CDC é reprocessado após um erro em uma execução anterior. Esta coluna de indicador permite que o desenvolvedor do SSIS trate erros diferentemente ao reprocessar alterações (por exemplo, ações como excluir de uma linha não existente e uma inserção com falha em uma chave duplicada podem ser ignoradas).<br /><br /> O valor padrão é **false**.|  
|CommandTimeOut|Integer|Esse valor indica o tempo limite (em segundos) a ser usado ao se comunicar com o banco de dados do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . Esse valor é usado quando o tempo de resposta do banco de dados é muito lento e o valor padrão (30 segundos) não é o bastante.|  
  
 Para obter mais informações sobre a origem CDC, consulte [Origem CDC](../../integration-services/data-flow/cdc-source.md).  
  
  
