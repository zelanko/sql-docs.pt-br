---
title: Editor de Gerenciador de Conexão do Excel | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dts.designer.excelconnection.f1
helpviewer_keywords:
- Excel Connection Manager Editor
ms.assetid: 7ff097e4-cafb-4885-a898-05b2a46628c1
caps.latest.revision: 27
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 9396c9fe0a04dd7cf8c3f8e408ea22e83dc1c3e5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36122885"
---
# <a name="excel-connection-manager-editor"></a>Editor de Gerenciador de Conexões Excel
  Use a caixa de diálogo **Editor de Gerenciador de Conexões Excel** para adicionar uma conexão a um arquivo da pasta de trabalho novo ou existente do [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)].  
  
 Para saber mais sobre o Gerenciador de Conexões Excel, consulte [Gerenciador de conexões do Excel](connection-manager/excel-connection-manager.md).  
  
> [!NOTE]  
>  Não é possível estabelecer conexão com um arquivo do Excel protegido por senha.  
  
## <a name="options"></a>Opções  
 **Caminho de arquivo do Excel**  
 Digite o caminho e nome de arquivo de um arquivo de pasta de trabalho do Excel (.xls) novo ou existente.  
  
> [!WARNING]  
>  O **Editor de destino do Excel** cria automaticamente o arquivo do Excel quando você seleciona um **Excel Conexão** que aponta para um novo/inexistente de arquivo e, em seguida, clique em **novo** para **Nome da planilha do Excel**.  
  
 **Procurar**  
 Use a caixa de diálogo **Abrir** para navegar até a pasta na qual o arquivo Excel existe ou onde você deseja criar o novo arquivo.  
  
 **Versão do Excel**  
 Especifique a versão do Microsoft Excel que foi usada para criar o arquivo.  
  
|Opção|Description|  
|------------|-----------------|  
|Excel 97-2003|O arquivo foi criado usando o Excel 97 ou posterior.|  
|Excel 3.0|Arquivo foi criado usando o Excel 3.0.|  
|Excel 4.0|O arquivo foi criado usando o Excel 4.0.|  
|Excel 5.0|O arquivo foi criado usando o Excel 95 (7.0).|  
  
 **Primeira linha com nomes de coluna**  
 Especifique se a primeira linha de dados na planilha selecionada contém os nomes de coluna. O valor padrão desta opção é **Verdadeiro**.  
  
## <a name="see-also"></a>Consulte também  
 [Referência de mensagens e erros do Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Loop através de arquivos e tabelas do Excel por meio de um contêiner do Loop Foreach](control-flow/foreach-loop-container.md)  
  
  