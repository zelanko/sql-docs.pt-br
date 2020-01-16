---
title: OData Source | Microsoft Docs
ms.date: 09/17/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.custom: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.DTS.DESIGNER.ODATASOURCE.F1
- sql13.dts.designer.odatasource.connection.f1
- sql13.dts.designer.odatasource.columns.f1
- sql13.dts.designer.odatasource.erroroutput.f1
ms.assetid: cc9003c9-638e-432b-867e-e949d50cec90
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 2177b4d1c4454aca803f11980340407362236c8c
ms.sourcegitcommit: 94f6a4b506dfda242fc3efb2403847e22a36d340
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/30/2019
ms.locfileid: "75546531"
---
# <a name="odata-source"></a>Origem do OData

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


Use o componente OData Source em um pacote do SSIS para consumir os dados do serviço do OData (Protocolo Open Data).

## <a name="supported-protocols-and-data-formats"></a>Formatos de dados e protocolos com suporte

O componente oferece suporte para os protocolos OData v3 e v4.  
  
-   Para o protocolo V3 do OData, o componente dá suporte aos formatos de dados ATOM e JSON.  
  
-   Para o protocolo V4 do OData, o componente dá suporte ao formato de dados JSON.  

## <a name="supported-data-sources"></a>Fontes de dados com suporte

O OData Source inclui suporte para as seguintes fontes de dados:
-   Microsoft Dynamics AX Online e Microsoft Dynamics CRM Online
-   Listas do SharePoint. Para ver todas as listas em um servidor do SharePoint, use a seguinte URL: `https://<server>/_vti_bin/ListData.svc`. Para obter mais informações sobre as convenções de URL do SharePoint, consulte [Interface REST do SharePoint Foundation](https://msdn.microsoft.com/library/ff521587.aspx).

## <a name="supported-data-types"></a>Tipos de dados com suporte

A fonte OData dá suporte aos seguintes tipos de dados simples: int, byte[], bool, byte, DateTime, DateTimeOffset, decimal, double, Guid, Int16, Int32, Int64, sbyte, float, string e TimeSpan.

Para descobrir os tipos de dados das colunas em sua fonte de dados, verifique a página `https://<OData feed endpoint>/$metadata`.

Para o tipo de dados **Decimal**, a precisão e a escala são determinadas pelos metadados de origem. Se os metadados de origem não especificarem as propriedades de **Precisão** e **Escala**, os dados poderão ser truncados.

> [!IMPORTANT]
> O componente OData Source não é compatível com tipos complexos, como itens de múltipla escolha, nas listas do SharePoint.

## <a name="odata-format-and-performance"></a>Desempenho e Formato OData
 A maioria dos serviços do OData podem retornar resultados em vários formatos. Você pode especificar o formato do conjunto de resultados usando a opção de consulta `$format`. Os formatos como JSON e JSON Light são mais eficientes do que o ATOM ou XML, e podem oferecer um melhor desempenho ao transferir grandes quantidades de dados. A tabela a seguir fornece os resultados dos testes de exemplo. Como você pode ver, houve um ganho de desempenho de 30% a 53% ao trocar do ATOM para o JSON e um ganho de desempenho de 67% ao trocar do ATOM para o novo formato JSON Light (disponível nos Serviços de Dados do WCF 5.1).  
  
|Linhas|ATOM|JSON|JSON (Light)|  
|-|-|-|-|  
|10000|113 segundos|74 segundos|68 segundos|  
|1\.000.000|1\.110 segundos|853 segundos|665 segundos|  
  
## <a name="related-topics-in-this-section"></a>Tópicos relacionados nesta seção  
  
-   [Tutorial: Uso do OData Source](../../integration-services/data-flow/tutorial-using-the-odata-source.md)  
  
-   [Modifique a consulta de origem do OData em runtime](../../integration-services/data-flow/modify-odata-source-query-at-runtime.md)  
  
-   [Propriedades da origem do OData](../../integration-services/data-flow/odata-source-properties.md)  
  
## <a name="odata-source-editor-connection-page"></a>Editor de Origem do OData (página Conexão)
  Use a página **Conexão** da caixa de diálogo **Editor de Origem do OData** para selecionar o gerenciador de conexões do OData para a origem do OData. Essa página também permite que você especifique uma coleção ou um caminho de recurso e qualquer opção de consulta para indicar quais dados precisam ser recuperados da origem do OData. 
  
### <a name="static-options"></a>Opções estáticas  
 **Gerenciador de conexões do OData**  
 Selecione um gerenciador de conexões existente na lista ou crie uma nova conexão clicando em **Nova**.  
  
 Depois que você selecionar ou criar um gerente de conexões, a caixa de diálogo exibe a versão do protocolo OData que o gerenciador de conexão está usando.  
  
 **Novo**  
 Crie um novo gerenciador de conexões usando a caixa de diálogo **Editor do Gerenciador de Conexões do OData** .  
  
 **Use o caminho de coleção ou de recurso**  
 Especifique o método para selecionar os dados da origem.  
  
|Opção|DESCRIÇÃO|  
|------------|-----------------|  
|Coleção|Recupere os dados da origem do OData usando um nome de coleção.|  
|Caminho do recurso|Recupere os dados da origem do OData usando um caminho de recurso.|  
  
 **Opções de consulta**  
 Especifique as opções para a consulta. Por exemplo: `$top=5` 
  
 **Url do feed**  
 Exibe o URL do feed somente leitura com base nas opções que você selecionou nesta caixa de diálogo.  
  
 **Visualização**  
 Visualize os resultados usando a caixa de diálogo **Visualização** . A**Visualização** pode exibir até 20 linhas.  
  
### <a name="dynamic-options"></a>Opções dinâmicas  
  
#### <a name="use-collection-or-resource-path--collection"></a>Use o caminho de coleção ou de recurso = Coleção  
 **Coleção**  
 Selecione uma coleção na lista suspensa.  
  
#### <a name="use-collection-or-resource-path--resource-path"></a>Use o caminho da coleção ou do recurso = Caminho do recurso  
 **Resource path**  
 Digite um caminho de recurso. Por exemplo:  funcionários  
  
## <a name="odata-source-editor-columns-page"></a>Editor de Origem do OData (página Colunas)
  Use a página **Colunas** da caixa de diálogo **Editor de Origem OData** para selecionar as colunas externas (origem) a serem incluídas na saída e para mapeá-las para as colunas de saída.  
  
### <a name="options"></a>Opções  
 **Colunas Externas Disponíveis**  
 Exiba a lista de colunas de origem disponíveis na fonte de dados. Use as caixas de seleção na lista para adicionar ou remover colunas à tabela na parte inferior da página. As colunas selecionadas são adicionadas à saída.  
  
 **Coluna Externa**  
 Exiba as colunas de origem que você escolheu para serem incluídas na saída.  
  
 **Coluna de Saída**  
 Forneça um nome exclusivo para cada coluna de saída. O padrão é o nome da coluna externa (origem) selecionada; porém, é possível escolher qualquer nome descritivo exclusivo.  
  
## <a name="odata-source-editor-error-output-page"></a>Editor de Origem do OData (página Saída de Erro)
  Use a página **Saída de Erro** da caixa de diálogo **Editor de Origem OData** para selecionar opções de tratamento de erros e definir propriedades em colunas de saída de erros.  
  
### <a name="options"></a>Opções  
 **Entrada/Saída**  
 Exibe o nome da fonte de dados.  
  
 **Coluna**  
 Exiba as colunas externas (origem) que você selecionou na página **Gerenciador de Conexões** da caixa de diálogo do **Editor de Origem do OData** .  
  
 **Erro**  
 Especifique o que deve acontecer quando ocorre um erro: ignorar a falha, redirecionar a linha ou causar falha no componente.  
  
 **Tópicos relacionados:** [Tratamento de erro em dados](../../integration-services/data-flow/error-handling-in-data.md)  
  
 **Truncation**  
 Especifique o que deve acontecer quando ocorre um truncamento: ignorar a falha, redirecionar a linha ou causar falha do componente.  
  
 **Descrição**  
 Exiba a descrição do erro.  
  
 **Definir este valor para células selecionadas**  
 Especifique o que deve acontecer a todas as células selecionadas quando ocorre um erro ou um truncamento: ignorar a falha, redirecionar a linha ou causar a falha no componente.  
  
 **Aplicar**  
 Aplique a opção de tratamento de erros às células selecionadas.  
  
## <a name="see-also"></a>Consulte Também  
 [Gerenciador de Conexões OData](../../integration-services/connection-manager/odata-connection-manager.md)  
  
  
