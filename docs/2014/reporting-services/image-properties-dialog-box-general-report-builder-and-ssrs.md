---
title: Imagem da caixa de diálogo de propriedades geral (construtor de relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- "10051"
- sql12.rtp.rptdesigner.pictureproperties.general.f1
ms.assetid: c2218b93-f7fe-46ef-995f-d7dadf9752ec
caps.latest.revision: 12
author: maggiesmsft
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 7137b65223a092cc136db7fda21cd2cd0e5c2ce2
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37292206"
---
# <a name="image-properties-dialog-box-general-report-builder-and-ssrs"></a>Caixa de diálogo Propriedades da Imagem, Geral (Construtor de Relatórios e SSRS)
  Selecione **Geral** na caixa de diálogo **Propriedades da Imagem** para adicionar uma imagem, alterar o nome padrão da imagem e adicionar texto à Dica de Ferramenta.  
  
## <a name="options"></a>Opções  
 **Nome**  
 Digite um nome para o item. O nome deve ser exclusivo no relatório. Por padrão, é atribuído um nome geral, como Image1 ou Image2.  
  
 **Dica de ferramenta**  
 Digite um texto ou uma expressão que seja avaliada como uma Dica de Ferramenta. Clique no botão Expressão (*fx*) para editar a expressão. A **Dica de Ferramenta** é exibida quando o usuário coloca o ponteiro sobre o item em um relatório de HTML.  
  
 **Selecione a origem da imagem**  
 Indique onde a imagem está armazenada para que quando o relatório for renderizado, o processador de relatórios saiba onde poderá obter a imagem.  
  
-   **Externa** Escolha essa opção quando quiser que a imagem continue existindo como um arquivo em um servidor Web ou um servidor de relatórios.  
  
-   **Inserido** Escolha essa opção quando quiser inserir a imagem no relatório.  
  
-   **Banco de Dados** Escolha essa opção quando quiser incluir um nome de campo do banco de dados que representa as imagens que deseja incluir em seu relatório.  
  
 **Usar esta imagem**  
 Essa opção aparece quando você seleciona a opção **Inserido** ou **Externo** .  
  
 Se você estiver inserindo a imagem, escolha a imagem que deseja adicionar ao relatório na lista suspensa. Clique no botão **Importar** para adicionar a imagem à lista suspensa.  
  
 Se você selecionar a opção **Externo** , digite a URL da imagem. Para um relatório publicado em um servidor de relatórios configurado para o modo nativo, use um caminho completo ou relativo. Por exemplo, http://\<servername > / images/image1.jpg. Para um relatório publicado em um servidor de relatórios configurado para o modo integrado do SharePoint, use uma URL completamente qualificada. Por exemplo, http://\<*SharePointservername*>/\<*site*> / Documents/images/image1.jpg.  
  
 **Importar**  
 Clique para adicionar uma imagem à lista suspensa **Usar esta imagem** .  
  
 **Use este campo**  
 Esta opção será exibida se você selecionar a opção **Banco de Dados** . Selecione o nome do campo.  
  
 **Use esse tipo MIME**  
 Escolha o formato apropriado das imagens contidas no banco de dados, por exemplo, .bmp, .jpeg, .gif, .png e .x-png.  
  
## <a name="see-also"></a>Consulte também  
 [Exemplos de expressões &#40;Construtor de Relatórios e SSRS&#41;](report-design/expression-examples-report-builder-and-ssrs.md)   
 [Imagens &#40;relatórios e SSRS&#41;](report-design/images-report-builder-and-ssrs.md)   
 [Ajuda do Construtor de Relatórios para caixas de diálogo, painéis e assistentes](../../2014/reporting-services/report-builder-help-for-dialog-boxes-panes-and-wizards.md)  
  
  
