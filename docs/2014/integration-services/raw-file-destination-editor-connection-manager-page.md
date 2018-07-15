---
title: Editor de destino arquivo bruto (página Gerenciador de Conexão) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.rawfiledestinationconnectionmanager.f1
ms.assetid: a0ec9643-3b44-4467-b855-f45ae4794f7f
caps.latest.revision: 7
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: cade93703374705e88abf136233a966e20aadfe8
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37271192"
---
# <a name="raw-file-destination-editor-connection-manager-page"></a>Editor de destino Arquivo Bruto (página Gerenciador de Conexões)
  Use o Editor de Destino Arquivo Bruto para configurar o destino Arquivo Bruto para gravar dados brutos em um arquivo.  
  
 **O que você deseja fazer?**  
  
-   [Abra o Editor de destino Arquivo Bruto](#open)  
  
-   [Definir as opções na guia de Gerenciador de Conexões](#connection)  
  
-   [Definir opções na guia Colunas](#mapping)  
  
##  <a name="open"></a> Abra o Editor de destino Arquivo Bruto  
  
1.  Adicione o destino Arquivo Bruto a um pacote do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
2.  Clique com o botão direito do mouse no componente e clique em **Editar**.  
  
##  <a name="connection"></a> Definir as opções na guia de Gerenciador de Conexões  
 **Modo de acesso**  
 Selecione o modo como o nome de arquivo é especificado. Selecione **Nome de arquivo** para inserir o nome do arquivo e o caminho diretamente de **Nome de arquivo de variável** para especificar uma variável que contenha o nome de arquivo.  
  
 **Nome do arquivo** ou **Nome de variável**  
 Insira o nome e o caminho do arquivo bruto ou selecione a variável que contém o nome de arquivo.  
  
 **Opção de gravação**  
 Selecione o método usado para criar e gravar no arquivo.  
  
 **Gerar arquivo bruto inicial**  
 Clique no botão para gerar um arquivo bruto vazio que contém somente as colunas (arquivo de somente metadados) sem precisar executar o pacote. O arquivo contém as colunas que você selecionou na página **Colunas** do **Editor de destino Arquivo Bruto**. Você pode apontar a fonte Arquivo Bruto para esse arquivo somente de metadados.  
  
 Quando você clica em **Gerar arquivo bruto inicial**, uma caixa de mensagem aparece. Clique em **OK** para continuar a criar o arquivo. Clique em **Cancelamento** para selecionar uma lista diferente de colunas na página de **Colunas** .  
  
##  <a name="mapping"></a> Definir opções na guia Colunas  
 **Colunas de Entrada Disponíveis**  
 Selecione uma ou mais colunas de entrada para gravar no arquivo bruto.  
  
 **Coluna de Entrada**  
 Uma coluna de entrada é adicionada automaticamente a essa tabela quando você a seleciona em **Colunas de Entrada Disponíveis**; se preferir, selecione a coluna de entrada diretamente nessa tabela.  
  
 **Alias de Saída**  
 Especifique um nome alternativo a ser usado para a coluna de saída.  
  
## <a name="see-also"></a>Consulte também  
 [Destino do Arquivo Bruto](data-flow/raw-file-destination.md)  
  
  
