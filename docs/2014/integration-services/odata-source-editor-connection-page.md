---
title: Editor de origem OData (página conexão) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- Sql12.dts.designer.odatasource.connection.f1
ms.assetid: 20bcd347-4547-4fad-b182-9571030101df
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 0e36c0a3449566db9a2acee360243c77ee548f92
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66057322"
---
# <a name="odata-source-editor-connection-page"></a>Editor de Origem do OData (página Conexão)
  Use a página **Conexão** da caixa de diálogo **Editor de Origem do OData** para selecionar o gerenciador de conexões do OData para a origem do OData. Essa página também permite que você especifique uma coleção ou um caminho de recurso e qualquer opção de consulta para indicar quais dados precisam ser recuperados da origem do OData. Para obter mais informações sobre origem do OData, consulte [OData Source](data-flow/odata-source.md).  
  
## <a name="static-options"></a>Opções estáticas  
 **Gerenciador de conexões do OData**  
 Selecione um gerenciador de conexões existente na lista ou crie uma nova conexão clicando em **Nova**.  
  
 **Novo**  
 Crie um novo gerenciador de conexões usando a caixa de diálogo **Editor do Gerenciador de Conexões do OData** .  
  
 **Use o caminho de coleção ou de recurso**  
 Especifique o método para selecionar os dados da origem.  
  
|Opção|DESCRIÇÃO|  
|------------|-----------------|  
|Coleção|Recupere os dados da origem do OData usando um nome de coleção.|  
|Caminho do recurso|Recupere os dados da origem do OData usando um caminho de recurso.|  
  
 **Opções de consulta**  
 Especifique as opções para a consulta.  Por exemplo: $top=5  
  
 **Url do feed**  
 Exibe o URL do feed somente leitura com base nas opções que você selecionou nesta caixa de diálogo.  
  
 **Visualização**  
 Visualize os resultados usando a caixa de diálogo **Visualização** . A**Visualização** pode exibir até 20 linhas.  
  
## <a name="dynamic-options"></a>Opções dinâmicas  
  
### <a name="use-collection-or-resource-path--collection"></a>Use o caminho de coleção ou de recurso = Coleção  
 **Coleção**  
 Selecione uma coleção na lista suspensa.  
  
### <a name="use-collection-or-resource-path--resource-path"></a>Use o caminho da coleção ou do recurso = Caminho do recurso  
 **Resource path**  
 Digite um caminho de recurso. Por exemplo:  funcionários  
  
## <a name="see-also"></a>Consulte Também  
 [Editor de origem OData &#40;página colunas&#41;](../../2014/integration-services/odata-source-editor-columns-page.md)   
 [Editor de origem OData &#40;página saída de erro&#41;](../../2014/integration-services/odata-source-editor-error-output-page.md)   
 [Gerenciador de Conexões OData](connection-manager/odata-connection-manager.md)  
  
  
