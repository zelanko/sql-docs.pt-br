---
title: Solucionar problemas de partes de relatório (construtor de relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: d9fe1932-46e7-421b-a8a9-4c54d9576e94
author: maggiesmsft
ms.author: douglasl
manager: craigg
ms.openlocfilehash: e43bbb27fc94d9fc7a32fb95b90e0b4e2cd53bd9
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48189316"
---
# <a name="troubleshoot-report-parts-report-builder-and-ssrs"></a>Solução de problemas de partes de relatório (Construtor de Relatórios e SSRS)
  Estas dicas podem ajudar a trabalhar com partes de relatório.  
  
## <a name="why-do-my-co-worker-and-i-see-different-instances-of-the-same-report-part-when-we-search-for-it"></a>Por que meu colaborador e eu vemos instâncias diferentes da mesma parte de relatório quando pesquisamos?  
 Pode haver várias instâncias de uma única parte de relatório em um servidor de relatório ou site do SharePoint integrado com um servidor de relatório e todas as instâncias terão o mesmo identificador exclusivo (GUID). Apenas a instância mais recente é exibida na lista de resultados da pesquisa. Em algumas situações, instâncias diferentes de uma única parte de relatório podem ter permissões diferentes. Se o seu colega de trabalho e você tiverem permissões diferentes no servidor, você não verá a mesma instância. Por exemplo, digamos que sejam salvas várias cópias de uma parte de relatório, todas com o mesmo GUID, em pastas diferentes em um servidor de relatório em modo integrado do SharePoint. Se as pastas tiverem permissões diferentes, as partes de relatório nessas pastas também terão permissões diferentes.  
  
 Para ver quais permissões você e seu colaborador têm, pergunte ao administrador do servidor de relatório.  
  
## <a name="when-i-search-for-report-parts-that-i-uploaded-to-a-sharepoint-server-i-do-not-see-them-why-not"></a>Quando eu procuro partes de relatório que eu carreguei em um servidor do SharePoint, eu não consigo vê-las. Por que não?  
 Partes de relatório que você carregou manualmente em uma biblioteca de documentos do SharePoint, em vez de publicar usando o Construtor de Relatórios, podem não aparecer na Galeria de Partes de Relatório. O servidor de relatório usado para a pesquisa de galeria pode precisar ser sincronizado com o conteúdo da biblioteca de documentos do SharePoint. Para obter mais informações, consulte [ativar o recurso de sincronização de arquivos de servidor de relatório na Administração Central do SharePoint](../../2014/reporting-services/activate-report-server-file-sync-feature-sharepoint-central-administration.md) na [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [Manuais Online do](http://go.microsoft.com/fwlink/?LinkId=154888) em msdn.microsoft.com.  
  
## <a name="why-cant-others-see-the-image-in-their-reports"></a>Por que outras pessoas não podem ver a imagem em seus relatórios?  
 Se você publicar uma parte de relatório que é um link para um arquivo de imagem, na realidade a parte de relatório será apenas um link. Se outras pessoas não puderem ver a imagem quando adicionarem a parte de relatório de imagem aos seus relatórios, talvez elas não tenham permissões para a imagem que você está vinculando.  
  
 Algumas soluções possíveis:  
  
-   Faça o arquivo de imagem ser uma parte de relatório, em vez de fazer o link para o arquivo de imagem ser uma parte de relatório.  
  
-   Mova o arquivo de imagem para um local em que outras pessoas tenham permissões.  
  
-   Peça ao administrador do servidor de relatório para alterar as permissões.  
  
## <a name="why-do-i-get-a-circular-reference-error-message-when-i-try-to-publish-my-report-part"></a>Por que eu recebo uma mensagem de erro de "referência circular" quando tento publicar minha parte de relatório?  
 Se os itens de relatório tiverem uma referência circular, você não poderá publicá-los como partes de relatório. Por exemplo, um item de relatório aponta para um conjunto de dados que aponta para um parâmetro. O parâmetro, por sua vez, também aponta para o conjunto de dados. Você precisará excluir uma das referências primeiro antes de publicar a parte de relatório.  
  
## <a name="see-also"></a>Consulte também  
 [Partes de relatório &#40;relatórios e SSRS&#41;](report-parts-report-builder-and-ssrs.md)  
  
  
