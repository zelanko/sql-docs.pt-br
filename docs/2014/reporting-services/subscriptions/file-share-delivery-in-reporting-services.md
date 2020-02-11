---
title: Entrega de compartilhamento de arquivos no Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [Reporting Services], file share delivery
- file share delivery [Reporting Services]
ms.assetid: 9f338dd3-f68a-4355-b9d7-9b25dacf3b5e
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d3d042530f69d34fde377ffc7c6e0a9200b9cc48
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66100904"
---
# <a name="file-share-delivery-in-reporting-services"></a>Entrega de compartilhamento de arquivos no Reporting Services
  O SQL Server [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] inclui uma extensão de entrega de compartilhamento de arquivos que possibilita entregar um relatório a uma pasta. A extensão de entrega de compartilhamento de arquivos está disponível por padrão e não requer configuração adicional. Para que a entrega do arquivo seja bem-sucedida, você deve definir permissões de acesso de gravação na pasta compartilhada. Além disso, os usuários que precisam acessar os relatórios devem ter permissões de leitura na pasta compartilhada.  
  
 Para distribuir um relatório a um compartilhado de arquivos, defina uma assinatura padrão ou uma assinatura controlada por dados. Você pode assinar e solicitar entrega de apenas um relatório por vez. Para saber como usar a entrega de compartilhamento de arquivos em uma assinatura controlada por dados, consulte [Criar uma assinatura controlada por dados &#40;Tutorial do SSRS&#41;](../create-a-data-driven-subscription-ssrs-tutorial.md). Além disso, a conta que executa assinaturas de compartilhamentos de arquivos remotos exige direitos para logon local no computador [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]Modo nativo &#124; [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] modo do SharePoint|  
  
 Neste tópico:  
  
-   [Características de um relatório entregues a uma pasta compartilhada](#bkmk_Characteristics)  
  
-   [Pastas de destino](#bkmk_target_folders)  
  
-   [Formatos de arquivo](#bkmk_file_formats)  
  
-   [Opções de arquivo](#bkmk_file_options)  
  
##  <a name="bkmk_Characteristics"></a>Características de um relatório que é entregue a uma pasta compartilhada  
 Diferentemente de relatórios hospedados e gerenciados por um servidor de relatório, os relatórios entregues a uma pasta compartilhada são arquivos estáticos. Os recursos interativos definidos para o relatório não funcionam para relatórios armazenados como arquivos no sistema de arquivos. Os recursos de interação são representados como elementos estáticos. Por exemplo, se você entregar um relatório de matriz, o arquivo resultante mostrará a exibição de nível superior do relatório; não será possível expandir as linhas e colunas para exibir os dados com suporte. Se o relatório incluir gráficos, a apresentação padrão será usada. Se o relatório estiver vinculado a outro relatório, o vínculo será renderizado como texto estático. Se você quiser reter recursos interativos em um relatório entregue, use a entrega de emails. Para obter mais informações, consulte [Entrega de email no Reporting Services](e-mail-delivery-in-reporting-services.md).  
  
##  <a name="bkmk_target_folders"></a>Pastas de destino  
 Ao definir uma assinatura que usa a entrega de compartilhamento de arquivos, você deve especificar uma pasta existente como a pasta de destino. O servidor de relatório não cria pastas no sistema de arquivos. A pasta especificada deve ser acessível por uma conexão de rede.  
  
 Verifique se os usuários que exibirão os relatórios na pasta compartilhada têm a permissão de leitura.  
  
 Ao especificar a pasta de destino em uma assinatura, use o formato UNC (convenção de nomenclatura uniforme) que inclui o nome de rede do computador. Não inclua barras invertidas à direita no caminho da pasta. O seguinte exemplo ilustra o caminho UNC:  
  
```  
\\<servername>\reportarchive\operations\2003  
```  
  
 Quando você criar a pasta, considere os limites de conexão desejados. O servidor de relatório precisa de duas conexões, mas você deve incluir conexões suficientes para acomodar usuários adicionais que queiram abrir relatórios na pasta compartilhada.  
  
##  <a name="bkmk_file_formats"></a>Formatos de arquivo  
 Os relatórios podem ser renderizados em vários formatos de arquivo, como HTML ou Excel. Para salvar o relatório em um formato de arquivo específico, selecione o formato de renderização ao criar sua assinatura. Por exemplo, se escolher **Excel** , salvará o relatório como um arquivo do [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] . Embora você possa escolher qualquer formato de renderização com suporte, alguns formatos funcionam melhor que outros na renderização em um arquivo.  
  
 Para obter a entrega de compartilhamento de arquivos, escolha um formato que entrega o relatório em um único arquivo, no qual todas as imagens e conteúdo relacionado são incluídos no relatório. Formatos adequados incluem o arquivo da Web, PDF, TIFF e Excel. Evite o HTML4.0. Se seu relatório incluir imagens, os formatos HTML 4.0 não as incluirão no arquivo.  
  
##  <a name="bkmk_file_options"></a>Opções de arquivo  
 Ao criar uma assinatura, você pode escolher opções que determinam como o nome de arquivo é criado e se ele é substituído por novas versões ao longo do tempo. Um nome de arquivo totalmente qualificado possui três partes: nome, extensão e texto ou número anexado ao arquivo para criar um nome de arquivo exclusivo. As opções de substituição determinam se o texto ou número é adicionado ao nome de arquivo.  
  
 O nome de arquivo é tem base no nome do relatório, mas você pode fornecer um nome personalizado na assinatura. A extensão é opcional, mas se você especificá-la, o servidor de relatório criará uma extensão que corresponda ao formato de renderização.  
  
 Você pode especificar as opões de substituição para reusar o mesmo nome de arquivo para cada entrega de relatório ou para criar um novo arquivo. Para substituir o arquivo, é necessário usar o mesmo nome e extensão de arquivo.  
  
 Uma abordagem alternativa para criar arquivos exclusivos para cada entrega é incluir um carimbo de hora no nome de arquivo. Para fazer isso, adicione a variável `@timestamp` ao nome de arquivo (por exemplo, *CompanySales@timestamp*). Com essa abordagem, o nome de arquivo será exclusivo por definição, portanto, nunca será substituído.  
  
## <a name="see-also"></a>Consulte Também  
 [Criar, modificar e excluir assinaturas padrão &#40;Reporting Services no modo nativo&#41;](create-and-manage-subscriptions-for-native-mode-report-servers.md)  
  
  
