---
title: Preencha a caixa de diálogo (construtor de relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
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
caps.latest.revision: 11
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 1378fb461e3a52f751f79cb0d31e0dcd498d8c0b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36009507"
---
# <a name="fill-dialog-box-report-builder-and-ssrs"></a>Caixa de diálogo Preenchimento (Construtor de Relatórios e SSRS)
  Na guia **Preenchimento**, você pode especificar as opções de cor da tela de fundo de uma única ou de várias células dentro de uma região de dados ou de uma caixa de texto.  
  
## <a name="options"></a>Opções  
 **Cor de preenchimento**  
 Clique no botão de cor para selecionar uma cor de preenchimento para o retângulo. Clique no **Expression***(fx)* botão para editar a expressão, que pode ser um valor hexadecimal para a cor RGB ou um dos nomes de cor predefinidos que são fornecidos no **expressão** caixa de diálogo. Para consultar uma lista de cores predefinidas, selecione **Web** no painel **Item**. Os nomes de cor listados no painel **Título** podem ser digitados no painel de texto da expressão. Não use sinal de igual (=) ou aspas ("") ao digitar o nome da cor.  
  
 **Selecione a origem da imagem**  
 Indique onde a imagem está armazenada para que, quando o relatório for renderizado, o processador de relatórios possa exibi-la.  
  
-   **Externa** Escolha essa opção quando quiser que a imagem continue existindo como um arquivo em um servidor Web ou um servidor de relatórios.  
  
-   **Inserido** Escolha essa opção quando quiser inserir a imagem no relatório.  
  
-   **Banco de Dados** Escolha essa opção quando quiser incluir um nome de campo do banco de dados que representa as imagens que deseja incluir em seu relatório.  
  
 **Use esta imagem**  
 Essa opção aparece quando você seleciona a opção **Inserido** ou **Externo** .  
  
 Se estiver inserindo a imagem, na lista suspensa, escolha a imagem a ser adicionada ao relatório. Clique em **Importar** para adicionar a imagem à lista suspensa. Se você adicionou uma imagem ao painel **Dados** , poderá selecioná-la escolhendo a opção **Inserido** e, em seguida, selecionar a imagem na lista suspensa.  
  
 Se você selecionar a opção **Externo** , digite a URL da imagem. Para um relatório publicado em um servidor de relatório configurado para o modo nativo, use um caminho completo ou relativo (por exemplo, http://*\<servername >*/imagens/Imagem1.jpg). Para um relatório publicado em um servidor de relatório configurado no modo integrado do SharePoint, use uma URL totalmente qualificada (por exemplo, http://*\<SharePointservername > /\<site >*  /documentos/imagens Image1.jpg).  
  
 **Importar**  
 Disponível quando você seleciona **Inserido**. Clique para adicionar uma imagem à lista suspensa **Usar esta imagem** .  
  
 **Use este campo**  
 Disponível quando você seleciona **Banco de Dados**. Selecione o nome do campo.  
  
 **Use esse tipo MIME**  
 Escolha o formato apropriado das imagens contidas no banco de dados (por exemplo, .bmp, .jpeg, .gif, .png ou .x-png).  
  
## <a name="see-also"></a>Consulte também  
 [Formatando itens de relatório &#40;Construtor de Relatórios e SSRS&#41;](report-design/formatting-report-items-report-builder-and-ssrs.md)   
 [Formatando texto e espaços reservados &#40;SSRS e construtor de relatórios&#41;](report-design/formatting-text-and-placeholders-report-builder-and-ssrs.md)   
 [Imagens &#40;SSRS e construtor de relatórios&#41;](report-design/images-report-builder-and-ssrs.md)  
  
  