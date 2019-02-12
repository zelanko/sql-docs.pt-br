---
title: Preencha a caixa de diálogo (construtor de relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.reportbody.fill.f1
- "10065"
- "10501"
- sql12.rtp.rptdesigner.shared.filldv.f1
- sql12.rtp.rptdesigner.rectangleproperties.fill.f1
- "10064"
- sql12.rtp.rptdesigner.textboxproperties.fill.f1
- "10124"
ms.assetid: 93a91d02-d558-4a0e-8d17-3fdf21e208d3
author: maggiesmsft
ms.author: maghan
manager: kfile
ms.openlocfilehash: 08451c74c9227fa76eb78c695908d96066015361
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56018218"
---
# <a name="fill-dialog-box-report-builder-and-ssrs"></a>Caixa de diálogo Preenchimento (Construtor de Relatórios e SSRS)
  Na guia **Preenchimento**, você pode especificar as opções de cor da tela de fundo de uma única ou de várias células dentro de uma região de dados ou de uma caixa de texto.  
  
## <a name="options"></a>Opções  
 **Cor de preenchimento**  
 Clique no botão de cor para selecionar uma cor de preenchimento para o retângulo. Clique no botão **Expressão** _(fx)_ para editar a expressão, que pode ser um valor hexadecimal para a cor RGB ou um dos nomes de cor predefinidos que foram fornecidos na caixa de diálogo **Expressão**. Para consultar uma lista de cores predefinidas, selecione **Web** no painel **Item**. Os nomes de cor listados no painel **Título** podem ser digitados no painel de texto da expressão. Não use sinal de igual (=) ou aspas ("") ao digitar o nome da cor.  
  
 **Selecione a origem da imagem**  
 Indique onde a imagem está armazenada para que, quando o relatório for renderizado, o processador de relatórios possa exibi-la.  
  
-   **Externa** Escolha essa opção quando quiser que a imagem continue existindo como um arquivo em um servidor Web ou um servidor de relatórios.  
  
-   **Inserido** Escolha essa opção quando quiser inserir a imagem no relatório.  
  
-   **Banco de Dados** Escolha essa opção quando quiser incluir um nome de campo do banco de dados que representa as imagens que deseja incluir em seu relatório.  
  
 **Usar esta imagem**  
 Essa opção aparece quando você seleciona a opção **Inserido** ou **Externo** .  
  
 Se estiver inserindo a imagem, na lista suspensa, escolha a imagem a ser adicionada ao relatório. Clique em **Importar** para adicionar a imagem à lista suspensa. Se você adicionou uma imagem ao painel **Dados** , poderá selecioná-la escolhendo a opção **Inserido** e, em seguida, selecionar a imagem na lista suspensa.  
  
 Se você selecionar a opção **Externo** , digite a URL da imagem. Para um relatório publicado em um servidor de relatório configurado para o modo nativo, use um caminho completo ou relativo (por exemplo, http://*\<servername >*  /images/Image1.jpg). Para um relatório publicado em um servidor de relatório configurado no modo integrado do SharePoint, use uma URL totalmente qualificada (por exemplo, http://*\<SharePointservername > /\<site >*  /documentos/imagens / Image1.jpg).  
  
 **Importar**  
 Disponível quando você seleciona **Inserido**. Clique para adicionar uma imagem à lista suspensa **Usar esta imagem** .  
  
 **Use este campo**  
 Disponível quando você seleciona **Banco de Dados**. Selecione o nome do campo.  
  
 **Use esse tipo MIME**  
 Escolha o formato apropriado das imagens contidas no banco de dados (por exemplo, .bmp, .jpeg, .gif, .png ou .x-png).  
  
## <a name="see-also"></a>Consulte também  
 [Formatando itens de relatório &#40;Construtor de Relatórios e SSRS&#41;](report-design/formatting-report-items-report-builder-and-ssrs.md)   
 [Formatando texto e espaços reservados &#40;Construtor de Relatórios e SSRS&#41;](report-design/formatting-text-and-placeholders-report-builder-and-ssrs.md)   
 [Imagens &#40;Construtor de Relatórios e SSRS&#41;](report-design/images-report-builder-and-ssrs.md)  
  
  
