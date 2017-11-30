---
title: Entrega de biblioteca do SharePoint no Reporting Services | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SharePoint integration [Reporting Services], report delivery
- delivering reports [Reporting Services]
- subscriptions [Reporting Services], SharePoint library delivery
ms.assetid: cb4e4f71-f2d5-475a-9284-ea324c93c7de
caps.latest.revision: "15"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 57b269676875edbb4a250a9bfd1e45c894239282
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="sharepoint-library-delivery-in-reporting-services"></a>Entrega de biblioteca do SharePoint no Reporting Services
  Um servidor de relatório configurado para integração com o SharePoint inclui uma extensão de entrega que você pode usar para enviar um relatório a uma biblioteca do SharePoint.  
  
 Para usar a extensão de entrega do SharePoint, você deve criar uma assinatura por meio da página do aplicativo em um site do SharePoint e, então, selecionar **Bibliotecas de Documentos SharePoint** como o tipo de entrega. Você não pode usar a extensão de entrega do SharePoint para assinaturas criadas no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] ou no Gerenciador de Relatórios.  
  
> [!NOTE]  
>  A extensão de entrega não oferece suporte à entrega de relatórios a um site do SharePoint se o servidor de relatório estiver sendo executado no modo nativo. Se você tentar chamar a extensão de entrega programaticamente para um servidor de relatório no modo nativo, o servidor retornará o erro **rsDeliveryExtensionNotFound** e registrará o erro **rsOperationNotSupportedSharePointMode** nos arquivos de log do servidor de relatório.  
  
## <a name="requirements"></a>Requisitos  
 Os requisitos para entrega de relatórios renderizados para uma biblioteca incluem os seguintes:  
  
-   O servidor de relatório deve estar configurado para o modo de integração do SharePoint.  
  
-   O servidor de relatório deve ter a extensão de entrega do SharePoint instalada e configurada.  
  
-   O relatório deve ser um arquivo (.rdl) de definição de relatório. Você não pode entregar outros tipos de conteúdo do servidor de relatório, como modelos ou recursos, por uma assinatura. Você não pode assinar relatórios ad hoc que usam modelos como fonte de dados.  
  
-   O relatório deve usar credenciais armazenadas. Esse é um pré-requisito para criação de qualquer assinatura em um relatório, independentemente do tipo de entrega.  
  
-   O destino deve ser uma biblioteca do SharePoint. Ao escolher uma biblioteca de destino, você deve escolher uma que esteja no mesmo site do SharePoint. Não é possível entregar um relatório a uma biblioteca em outro servidor ou em outro site na mesma coleção de sites.  
  
 As propriedades e metadados não fazem parte da entrega de relatório. Quando o relatório é entregue pela primeira vez, ele herda as configurações de segurança da pasta ou lista que o contém. Se você modificar as configurações de segurança ou as propriedades de relatório do conjunto subsequentemente, essas configurações serão mantidas. A assinatura apenas atualiza o relatório armazenado no local especificado.  
  
## <a name="sharepoint-permissions"></a>Permissões do SharePoint  
 Para criar a assinatura, você deve ter a permissão Exibir Itens no relatório. Para entregar o relatório, você deve ter a permissão Adicionar Itens na biblioteca na qual o relatório será entregue.  
  
## <a name="how-to-create-modify-and-delete-subscriptions"></a>Como criar, modificar e excluir assinaturas  
  
1.  Vá para o site do SharePoint do qual você acessa o relatório.  
  
2.  Selecione o relatório, clique na seta para baixo do lado do relatório e selecione **Gerenciar Assinaturas**.  
  
3.  Clique em **Criar**, **Editar**ou **Excluir**.  
  
 Uma mensagem de status na lista Gerenciar Assinaturas exibe as informações atuais sobre a assinatura, incluindo se ela foi bem-sucedida e a data e hora em que a assinatura foi executada pela última vez.  
  
## <a name="setting-delivery-options"></a>Definindo opções de entrega  
 Você pode definir as opções de entrega a seguir em uma assinatura que entrega um relatório a uma biblioteca do SharePoint.  
  
 Renderizar formato de saída  
 Especifique o formato de aplicativo no qual deseja que o relatório seja entregue. O relatório é renderizado nesse formato antes da entrega. O formato de saída que você selecionar determinará a extensão de arquivo padrão.  
  
 A lista de formatos de saída a serem escolhidos é o conjunto de extensões de renderização instalados no servidor de relatório.  
  
 Observe que você não pode especificar formatos de saída que são apenas para uso interno ou que não têm suporte para servidores de relatório executados no modo integrado do SharePoint. Esses formatos incluem Null, RGDI e HTMLOWC.  
  
 Nome e extensão do arquivo  
 Especifique o nome de arquivo e extensão do relatório como deseja que apareça na biblioteca de destino. Se você não especificar uma extensão de arquivo, o servidor de relatório criará uma com base no formato de saída do relatório. Esse valor é necessário. O nome de arquivo não deve incluir os seguintes caracteres: : \ / * ? " < > | # { } %  
  
 Título  
 Especifica uma propriedade **Título** opcional para o relatório na biblioteca de destino. Essa é uma propriedade padrão para todos os itens armazenados em uma biblioteca. Os usuários podem especificar se mostram ou ocultam essa propriedade ao exibir conteúdos de biblioteca em um site do SharePoint.  
  
 Caminho  
 Especifica uma URL completamente qualificada para a biblioteca do SharePoint, inclusive o aplicativo Web e o site do SharePoint. Por exemplo: `http://mySharePointWeb/MySite/MyDocLib`, em que `http://mySharePointWeb` indica o aplicativo Web, “MySite” é o site do SharePoint e “MyDocLib” é a biblioteca do SharePoint na qual o relatório será entregue.  
  
 Você não pode especificar uma página, um site nem uma lista. O contêiner de destino deve ser uma biblioteca no mesmo site ou farm.  
  
 Opções de substituição  
 Especifica se um arquivo com o mesmo nome e extensão é substituído por uma versão mais recente quando a assinatura é processada. Escolha **Substituir** se quiser substituir um arquivo existente por uma versão mais recente. Escolha **Nenhum** se não quiser que a assinatura substitua um arquivo. Nesse caso, não ocorrerá entrega se um arquivo existir com o nome e extensão de destino. Escolha **Incrementação automática** se quiser adicionar versões sucessivas do mesmo arquivo anexando um número ao final do nome do arquivo.  
  
 Autocopy  
 Se você estiver usando o recurso Autocopy para copiar automaticamente a última versão de um arquivo para vários locais, o arquivo será copiado se **Substituir** estiver habilitado. Se você tiver usado **Incrementação automática** ou **Nenhum**, a entrega falhará e ocorrerá o erro **rsDeliveryError** .  
  
## <a name="see-also"></a>Consulte também  
 [Criar e gerenciar assinaturas de servidores de relatório no modo SharePoint](../../reporting-services/subscriptions/create-and-manage-subscriptions-for-sharepoint-mode-report-servers.md)   
 [Assinaturas e entrega &#40;Reporting Services&#41;](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [Especificar informações de credenciais e de conexão para fontes de dados de relatório](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)  
  
  
