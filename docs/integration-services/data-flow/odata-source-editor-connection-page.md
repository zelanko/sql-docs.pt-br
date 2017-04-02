---
title: "Editor de Origem do OData (p&#225;gina Conex&#227;o) | Microsoft Docs"
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.odatasource.connection.f1"
ms.assetid: 20bcd347-4547-4fad-b182-9571030101df
caps.latest.revision: 8
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 8
---
# Editor de Origem do OData (p&#225;gina Conex&#227;o)
  Use a página **Conexão** da caixa de diálogo **Editor de Origem do OData** para selecionar o gerenciador de conexões do OData para a origem do OData. Essa página também permite que você especifique uma coleção ou um caminho de recurso e qualquer opção de consulta para indicar quais dados precisam ser recuperados da origem do OData. Para obter mais informações sobre origem do OData, consulte [OData Source](../../integration-services/data-flow/odata-source.md).  
  
## Opções estáticas  
 **Gerenciador de conexões do OData**  
 Selecione um gerenciador de conexões existente na lista ou crie uma nova conexão clicando em **Nova**.  
  
 Depois que você selecionar ou criar um gerente de conexões, a caixa de diálogo exibe a versão do protocolo OData que o gerenciador de conexão está usando.  
  
 **Nova**  
 Crie um novo gerenciador de conexões usando a caixa de diálogo **Editor do Gerenciador de Conexões do OData**.  
  
 **Use o caminho de coleção ou de recurso**  
 Especifique o método para selecionar os dados da origem.  
  
|Opção|Description|  
|------------|-----------------|  
|Coleção|Recupere os dados da origem do OData usando um nome de coleção.|  
|Caminho do recurso|Recupere os dados da origem do OData usando um caminho de recurso.|  
  
 **Opções de consulta**  
 Especifique as opções para a consulta.  Por exemplo: $top=5  
  
 **Url do feed**  
 Exibe o URL do feed somente leitura com base nas opções que você selecionou nesta caixa de diálogo.  
  
 **Visualização**  
 Visualize os resultados usando a caixa de diálogo **Visualização**. A**Visualização** pode exibir até 20 linhas.  
  
## Opções dinâmicas  
  
### Use o caminho de coleção ou de recurso = Coleção  
 **Coleção**  
 Selecione uma coleção na lista suspensa.  
  
### Use o caminho da coleção ou do recurso = Caminho do recurso  
 **Caminho do recurso**  
 Digite um caminho de recurso. Por exemplo: Funcionários  
  
## Consulte também  
 [Editor de Fonte OData &#40;Página Colunas&#41;](../../integration-services/data-flow/odata-source-editor-columns-page.md)   
 [Editor de Fonte OData &#40;Página Saída de Erro&#41;](../../integration-services/data-flow/odata-source-editor-error-output-page.md)   
 [Gerenciador de Conexões OData](../../integration-services/connection-manager/odata-connection-manager.md)  
  
  