---
title: Editor do Gerenciador de conexões do Excel | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.excelconnection.f1
helpviewer_keywords:
- Excel Connection Manager Editor
ms.assetid: 7ff097e4-cafb-4885-a898-05b2a46628c1
author: chugugrace
ms.author: chugu
ms.openlocfilehash: d9951d9bfe7e95499c2b967e6329d206cdc4aa44
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85437403"
---
# <a name="excel-connection-manager-editor"></a>Editor de Gerenciador de Conexões Excel
  Use a caixa de diálogo **Editor de Gerenciador de Conexões Excel** para adicionar uma conexão a um arquivo da pasta de trabalho novo ou existente do [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)] .  
  
 Para saber mais sobre o Gerenciador de Conexões Excel, consulte [Gerenciador de conexões do Excel](connection-manager/excel-connection-manager.md).  
  
> [!NOTE]  
>  Não é possível estabelecer conexão com um arquivo do Excel protegido por senha.  
  
## <a name="options"></a>Opções  
 **Caminho de arquivo do Excel**  
 Digite o caminho e nome de arquivo de um arquivo de pasta de trabalho do Excel (.xls) novo ou existente.  
  
> [!WARNING]  
>  O **Editor de destino do Excel** cria automaticamente o arquivo do Excel quando você seleciona uma **conexão do Excel** que aponta para um arquivo novo/não existente e, em seguida, clica em **novo** para **o nome da planilha do Excel**.  
  
 **Procurar**  
 Use a caixa de diálogo **abrir** para navegar até a pasta na qual o arquivo do Excel existe ou onde você deseja criar o novo arquivo.  
  
 **Versão do Excel**  
 Especifique a versão do Microsoft Excel que foi usada para criar o arquivo.  
  
|Opção|Descrição|  
|------------|-----------------|  
|Excel 97-2003|O arquivo foi criado usando o Excel 97 ou posterior.|  
|Excel 3,0|O arquivo foi criado usando o Excel 3,0.|  
|Excel 4,0|O arquivo foi criado usando o Excel 4.0.|  
|Excel 5,0|O arquivo foi criado usando o Excel 95 (7.0).|  
  
 **Primeira linha com nomes de coluna**  
 Especifique se a primeira linha de dados na planilha selecionada contém os nomes de coluna. O valor padrão desta opção é **Verdadeiro**.  
  
## <a name="see-also"></a>Consulte Também  
 [Integration Services referência de erro e mensagem](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Loop por meio de arquivos do Excel e tabelas usando um contêiner de Loop Foreach](control-flow/foreach-loop-container.md)  
  
  
