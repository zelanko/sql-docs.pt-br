---
title: Caminhos do Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.patheditor.general.f1
- sql13.dts.designer.patheditor.metadata.f1
- sql13.dts.designer.patheditor.visualizers.f1
helpviewer_keywords:
- paths [Integration Services], about paths
- data flow [Integration Services], paths
- paths [Integration Services]
- destinations [Integration Services], paths
- sources [Integration Services], paths
ms.assetid: 6c4629a9-2ede-4011-9101-3b342249640e
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 4443598b2fa59e51a9c8ec6b5161b913f2890056
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86918866"
---
# <a name="integration-services-paths"></a>Caminhos do Integration Services

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Um caminho conecta dois componentes em um fluxo de dados conectando a saída de um componente de fluxo de dados à entrada de outro componente. Um caminho tem uma origem e um destino. Por exemplo, se um caminho conectar uma origem OLE DB e uma transformação Classificação, a origem OLE DB será a origem do caminho e a transformação Classificação será o destino do caminho. A origem é o componente onde o caminho inicia, e o destino é o componente onde o caminho termina.  
  
 Se você executar um pacote no Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)] , será possível exibir os dados em um fluxo de dados anexando visualizadores de dados a um caminho. Um visualizador de dados pode ser configurado para exibir dados em uma grade. Um visualizador de dados é uma ferramenta útil de depuração. Para obter mais informações, consulte [Debugging Data Flow](../../integration-services/troubleshooting/debugging-data-flow.md).  
  
## <a name="configure-the-path"></a>Configurar o caminho  
 O Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)] fornece a caixa de diálogo **Editor de Caminho do Fluxo de Dados** para definir propriedades de caminho, exibindo os metadados das colunas de dados que passam pelo caminho e configurando visualizadores de dados.  
  
 As propriedades de caminho configurável incluem o nome, a descrição e a anotação do caminho. Você também pode configurar caminhos de forma programática. Para obter mais informações, consulte [Conectando componentes do fluxo de dados programaticamente](../../integration-services/building-packages-programmatically/connecting-data-flow-components-programmatically.md).  
  
 Uma anotação de caminho exibe o nome da origem do caminho ou o nome do caminho na superfície de design da guia **Fluxo de Dados** no Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)] . As anotações de caminho são semelhantes às anotações que você pode adicionar a fluxos de dados, fluxos de controle e manipuladores de eventos. A única diferença é que uma anotação de caminho é anexada a um caminho, ao passo que outras anotações aparecem nas guias **Fluxo de Dados**, **Fluxo de Controle**e **Controle de Eventos**do Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 Os metadados exibem nome, tipo de dados, precisão, escala, comprimento, página de código e componente de origem de cada coluna na saída do componente anterior. O componente de origem é o componente de fluxo de dados que criou a coluna. Isso pode ou não ser o primeiro componente no fluxo de dados. Por exemplo, as transformações Union All e Classificação criam as próprias colunas e são as origens de suas colunas de saída. Em contrapartida, uma transformação Copiar Coluna pode passar por colunas sem as alterá-las ou pode criar colunas novas copiando as colunas de entrada. A transformação Copiar Coluna é o componente de origem somente das novas colunas.  

## <a name="set-the-properties-of-a-path-with-the-data-flow-path-editor"></a>Definir as propriedades de um caminho por meio do Editor de Caminho do Fluxo de Dados
Os caminhos conectam dois componentes de fluxos de dados. Antes de você poder definir as propriedades do caminho, o fluxo de dados deve conter pelo menos dois componentes de fluxo de dados conectados.
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo.  
  
3.  Clique na guia **Fluxo de Dados** e clique duas vezes em um caminho.  
  
4.  No **Editor de Caminho de Fluxo de Dado**, clique em **Geral**. É possível editar o nome padrão do caminho e fornecer uma descrição do caminho. É possível também modificar a propriedade PathAnnotation.  
  
5.  Clique em **OK**.  
  
6.  Para salvar o pacote atualizado, clique em **Salvar Itens Selecionados** no menu **Arquivo** .  

## <a name="general-page---data-flow-path-editor"></a>Página Geral – Editor de Caminho do Fluxo de Dados
Use a caixa de diálogo **Editor de Caminho de Fluxo de Dados** para definir propriedades de caminho, visualizar metadados de colunas e gerenciar os visualizadores de dados que estão anexados ao caminho.  
  
 Use o nó **Geral** da caixa de diálogo **Editor de Caminho de Fluxo de Dados** para nomear e descrever o caminho e especificar as opções de anotação de caminho.  
  
### <a name="options"></a>Opções  
 **Nome**  
 Forneça um nome exclusivo para o caminho.  
  
 **ID**  
 O identificador de linhagem exclusivo do caminho. Essa propriedade é somente leitura.  
  
 **IdentificationString**  
 A cadeia de caracteres que identifica o caminho. Gerada automaticamente a partir do nome digitado acima.  
  
 **Descrição**  
 Descreva o caminho.  
  
 **PathAnnotation**  
 Especifique o tipo de anotação a ser usada. Escolha **Never** para desabilitar anotações, **AsNeeded** para habilitar anotação sob demanda, **SourceName** para anotações automáticas usando o valor da opção **SourceName** , e **PathName** para anotações automáticas usando o valor da propriedade **Name** .  
  
 **DestinationName**  
 Exibe a entrada que é o final do caminho.  
  
 **SourceName**  
 Exibe a saída que é o início do caminho.  
 
## <a name="metadata-page---data-flow-path-editor"></a>Página de Metadados – Editor de Caminho do Fluxo de Dados
Use a página **Metadados** da caixa de diálogo **Editor do Caminho de Fluxo de Dados** para exibir o metadados das colunas de caminho.  
  
### <a name="options"></a>Opções  
 **Página de metadados**  
 Lista metadados das colunas. Clique nos títulos das colunas para classificar seus dados.  
  
 **Nome**  
 Lista o nome da coluna.  
  
 **Tipo de Dados**  
 Lista o tipo de dados da coluna.  
  
 **Precisão**  
 Lista o número de dígitos em um valor numérico.  
  
 **Escala**  
 Lista o número de dígitos à direita da casa decimal em um valor numérico.  
  
 **Comprimento**  
 Lista o comprimento atual da coluna.  
  
 **Página de Código**  
 Lista a página de código da coluna. O valor **0** indica que a coluna não usa uma página de código. Isso acontece quando os dados estão em Unicode ou têm tipo de dados numérico, de data ou de hora.  
  
 **Posição da Chave de Classificação**  
 Lista a posição da chave de classificação da coluna. O valor **0** indica que a coluna não está classificada.  
  
> [!NOTE]  
>  Um prefixo de menos (-) indica que a coluna está em ordem decrescente.  
  
 **Sinalizadores de Comparação**  
 Lista os sinalizadores de comparação aplicados à coluna.  
  
 **Componente de Origem**  
 Lista o componente do fluxo de dados que é a origem da coluna.  
  
 **Copiar para a Área de Transferência**  
 Copia os metadados da coluna para a área de transferência. Por padrão, todas as linhas de metadados são copiadas na ordem exibida atualmente.  
 
## <a name="data-viewers-page---data-flow-path-editor"></a>Página Visualizadores de Dados – Editor de Caminho do Fluxo de Dados
Use a página **Visualizadores de Dados** da caixa de diálogo **Editor de Caminho de Fluxo de Dados** para gerenciar os visualizadores de dados que estão anexados ao caminho.  
  
### <a name="options"></a>Opções  
 **Nome**  
 Lista os visualizadores de dados.  
  
 **Tipo de Visualizador de Dados**  
 Lista o tipo de visualizador de dados.  
  
 **Adicionar**  
 Clique para adicionar um visualizador de dados usando a caixa de diálogo **Configurar Visualizador de Dados** .  
  
 **Delete (excluir)**  
 Clique para excluir o visualizador de dados selecionado.  
  
 **Configurar**  
 Clique para configurar um visualizador de dados selecionado, usando a caixa de diálogo **Configurar Visualizador de Dados** .  
 
## <a name="path-properties"></a>Path Properties
Os objetos de fluxo de dados no modelo de objeto do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] têm propriedades comuns e personalizadas ao nível do componente, de entradas e saídas e de colunas de entrada e saída. Muitas propriedades têm valores somente leitura, atribuídos em tempo de execução pelo mecanismo de fluxo de dados.  
  
 Esse tópico lista e descreve as propriedades personalizadas dos caminhos que conectam objetos do fluxo de dados.  
  
### <a name="custom-properties-of-a-path"></a>Propriedades personalizadas de um caminho  
 No modelo de objeto [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], um caminho que conecta componentes no fluxo de dados implementa a interface <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSPath100>.  
  
 A tabela a seguir descreve as propriedades configuráveis dos caminhos em um fluxo de dados. O mecanismo de fluxo de dados também atribui valores a propriedades somente leitura adicionais que não são listadas aqui.  
  
|Nome da propriedade|Tipo de Dados|DESCRIÇÃO|  
|-------------------|---------------|-----------------|  
|PathAnnotation|Inteiro (enumeração)|Um valor que indica se uma anotação deve ser exibida com o caminho na superfície do designer. Os valores possíveis são **AsNeeded**, **SourceName**, **PathName**e **Never**. O valor padrão é **AsNeeded**.|  
|DestinationName|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSInput100>|A entrada associada ao caminho.|  
|SourceName|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100>|A saída associada ao caminho.|  
