---
title: Editor de destino de arquivo bruto (página colunas) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.rawfiledestinationcolumns.f1
ms.assetid: 37f61d0b-1269-42ee-94ab-011cbaac63e9
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 8a0ceb00767715c3f0b5d149ecd7c8ac3116cf78
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85423203"
---
# <a name="raw-file-destination-editor-columns-page"></a>Editor de destino Arquivo Bruto (página Colunas)
  Use o Editor de Destino Arquivo Bruto para configurar o destino Arquivo Bruto para gravar dados brutos em um arquivo.  
  
 **O que você deseja fazer?**  
  
-   [Abra o Editor de destino Arquivo Bruto](#open)  
  
-   [Definir as opções na guia de Gerenciador de Conexões](#connection)  
  
-   [Definir opções na guia Colunas](#mapping)  
  
##  <a name="open-the-raw-file-destination-editor"></a><a name="open"></a>Abrir o editor de destino arquivo bruto  
  
1.  Adicione o destino Arquivo Bruto a um pacote do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
2.  Clique com o botão direito do mouse no componente e clique em **Editar**.  
  
##  <a name="set-options-on-the-connection-manager-tab"></a><a name="connection"></a>Definir opções na guia Gerenciador de conexões  
 **Modo de acesso**  
 Selecione o modo como o nome de arquivo é especificado. Selecione **Nome de arquivo** para inserir o nome do arquivo e o caminho diretamente de **Nome de arquivo de variável** para especificar uma variável que contenha o nome de arquivo.  
  
 **Nome do arquivo** ou **Nome de variável**  
 Insira o nome e o caminho do arquivo bruto ou selecione a variável que contém o nome de arquivo.  
  
 **Opção de gravação**  
 Selecione o método usado para criar e gravar no arquivo.  
  
 **Gerar arquivo bruto inicial**  
 Clique no botão para gerar um arquivo bruto vazio que contém somente as colunas (arquivo de somente metadados) sem precisar executar o pacote. Você pode apontar a origem Arquivo Bruto para o arquivo somente de metadados.  
  
 Quando você clica no botão, uma lista das colunas é exibida. Você pode clicar em cancelar e modificar as colunas ou pode clicar em OK para continuar a criação do arquivo.  
  
##  <a name="set-options-on-the-columns-tab"></a><a name="mapping"></a>Definir opções na guia colunas  
 **Colunas de Entrada Disponíveis**  
 Selecione uma ou mais colunas de entrada para gravar no arquivo bruto.  
  
 **Coluna de Entrada**  
 Uma coluna de entrada é adicionada automaticamente a essa tabela quando você a seleciona em **Colunas de Entrada Disponíveis**; se preferir, selecione a coluna de entrada diretamente nessa tabela.  
  
 **Alias de saída**  
 Especifique um nome alternativo a ser usado para a coluna de saída.  
  
## <a name="see-also"></a>Consulte Também  
 [Destino do Arquivo Bruto](data-flow/raw-file-destination.md)  
  
  
