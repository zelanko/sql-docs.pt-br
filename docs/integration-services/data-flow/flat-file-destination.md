---
title: Destino de arquivo simples | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.flatfiledest.f1
- sql13.dts.designer.flatfiledestadapter.connection.f1
- sql13.dts.designer.flatfiledestadapter.mappings.f1
helpviewer_keywords:
- flat files
- Flat File destination
- text file writing [Integration Services]
- destinations [Integration Services], Flat File
ms.assetid: e0d6e356-8db4-48aa-ba66-029397f98f61
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 96badece6d707558fa9fcda87bdf9f71af64255e
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/20/2019
ms.locfileid: "58290432"
---
# <a name="flat-file-destination"></a>Destino de arquivo simples
  O destino de Arquivo Simples grava dados em um arquivo de texto. O arquivo de texto pode ser em formato delimitado, de largura fixa, largura fixa com delimitador de linha ou com imperfeição à direita.  
  
 Você pode configurar o destino de arquivo simples das seguintes formas:  
  
-   Forneça um bloco de texto que é inserido no arquivo antes de qualquer dado ser escrito. O texto pode fornecer informações como cabeçalhos de coluna.  
  
-   Especifique se os dados devem ser substituídos em um arquivo de destino que tenha o mesmo nome.  
  
 Esse destino utiliza um gerente de conexões de arquivo simples para acessar o arquivo de texto. Ao definir propriedades no gerenciador de conexões de arquivo simples que o arquivo simples usa, você pode especificar como o destino do arquivo simples formata e escreve o arquivo de texto. Quando você configura o gerenciador de conexões de arquivo simples, você especifica informações sobre o arquivo e sobre cada coluna do arquivo. Por exemplo, pode-se especificar os caracteres que delimitam colunas e linhas no arquivo e especificar o tipo de dados e o comprimento de cada coluna. Para obter mais informações, consulte [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md).  
  
 O destino de arquivo simples inclui a propriedade personalizada Header. Essa propriedade pode ser atualizada por uma expressão de propriedade quando o pacote é carregado. Para obter mais informações, consulte [Expressões do Integration Services &#40;SSIS&#41;](../../integration-services/expressions/integration-services-ssis-expressions.md), [Usar expressões de propriedade em pacotes](../../integration-services/expressions/use-property-expressions-in-packages.md) e [Propriedades personalizadas de arquivo simples](../../integration-services/data-flow/flat-file-custom-properties.md).  
  
 Esse destino tem uma saída. Não dá suporte a uma saída de erro.  
  
## <a name="configuration-of-the-flat-file-destination"></a>Configuração do destino de Arquivo Simples  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 A caixa de diálogo **Editor Avançado** reflete as propriedades que podem ser definidas programaticamente. Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor Avançado** ou programaticamente, clique em um dos seguintes tópicos:  
  
-   [Propriedades comuns](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Propriedades personalizadas de arquivo simples](../../integration-services/data-flow/flat-file-custom-properties.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 Para obter informações sobre como definir as propriedades do componente de fluxo de dados, consulte [Definir as propriedades de um componente de fluxo de dados](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="flat-file-destination-editor-connection-manager-page"></a>Editor de Destino de Arquivo Simples (página Gerenciador de Conexões)
  Use a página do **Gerenciador de Conexões** da caixa de diálogo do **Editor de Destino de Arquivo Simples** para selecionar a conexão de arquivo simples do destino e especificar se irá substituir ou anexar ao arquivo de destino existente. O destino de arquivo simples grava dados em um arquivo de texto. Esse arquivo de texto pode ser em formato delimitado, de largura fixa, de largura fixa com delimitador de linha ou em formato irregular à direita.  
  
### <a name="options"></a>Opções  
 **Gerenciador de conexões de arquivo simples**  
 Selecione um gerenciador de conexões existente usando a caixa de listagem ou crie uma nova conexão clicando em **Novo**.  
  
 **Nova**  
 Crie uma nova conexão utilizando as caixas de diálogo **Formato de Arquivo Simples** e **Editor do Gerenciador de Conexões de Arquivos Simples** .  
  
 Além dos formatos padrão de arquivo simples: delimitado, de largura fixa e irregular à direita, a caixa de diálogo **Formato de Arquivo Simples** tem uma quarta opção, **Largura fixa com delimitadores de linha**. Esta opção representa um caso especial do formato irregular à direita no qual o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] adiciona uma coluna fictícia como a coluna final de dados. Essa coluna fictícia assegura que a coluna final tenha uma largura fixa.  
  
 A opção **Largura fixa com delimitadores de linha** não está disponível no **Editor do Gerenciador de Conexões de Arquivos Simples**. Se necessário, você pode emular esta opção no editor. Para emular esta opção, na página **Geral** do **Editor do Gerenciador de Conexões de Arquivos Simples**, em **Formato**, selecione **Irregular à direita**. Na página **Avançado** do editor, adicione uma nova coluna fictícia como a coluna final de dados.  
  
 **Substituir dados no arquivo**  
 Indique se irá substituir um arquivo existente ou acrescentar dados a ele.  
  
 **Cabeçalho**  
 Digite um bloco de texto a ser inserido no arquivo antes que qualquer dado seja gravado. Use esta opção para incluir informações adicionais, como cabeçalhos de coluna.  
  
 **Visualização**  
 Visualize os resultados usando a caixa de diálogo **Exibição de Dados** . A visualização pode exibir até 200 linhas.  
  
## <a name="flat-file-destination-editor-mappings-page"></a>Editor de Destino de Arquivo Simples (Página Mapeamentos)
  Use a página **Mapeamentos** da caixa de diálogo **Editor de Destino de Arquivo Simples** para mapear colunas de entrada para colunas de destino.  
  
### <a name="options"></a>Opções  
 **Colunas de Entrada Disponíveis**  
 Exiba a lista das colunas de entrada disponíveis. Use uma operação de arrastar e soltar para mapear as colunas de entrada disponíveis para colunas de destino.  
  
 **Colunas de Destino Disponíveis**  
 Exiba a lista de colunas de destino disponíveis. Use uma operação de arrastar e soltar para mapear as colunas de destino disponíveis para colunas de entrada.  
  
 **Coluna de Entrada**  
 Exiba as colunas de entrada selecionadas anteriormente neste tópico. É possível alterar os mapeamentos usando a lista **Colunas de Entrada Disponíveis**. Selecione **\<ignorar>** para excluir a coluna da saída.  
  
 **Coluna de Destino**  
 Exiba cada coluna de destino disponível, seja ela mapeada ou não.  
  
## <a name="see-also"></a>Consulte Também  
 [Fonte de Arquivo Simples](../../integration-services/data-flow/flat-file-source.md)   
 [Fluxo de Dados](../../integration-services/data-flow/data-flow.md)  
  
  
