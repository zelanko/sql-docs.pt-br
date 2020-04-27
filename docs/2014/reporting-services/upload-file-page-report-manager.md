---
title: Página carregar arquivo (Report Manager) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 7bb3166f-9374-4449-b66a-ffb77298507d
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 1100baa3cd72a04d208b2076d91ca4efed7d38e6
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66098873"
---
# <a name="upload-file-page-report-manager"></a>Página Carregar Arquivo (Gerenciador de Relatórios)
  Use a página Carregar Arquivo para publicar um arquivo do sistema de arquivos no banco de dados do servidor de relatório. Arquivos carregados são representados como itens na hierarquia de pasta de servidor de relatório.  
  
-   Arquivos .rdl carregados são publicados em um servidor de relatório como relatórios.  
  
-   Arquivos .smdl carregados são publicados como modelos de relatório se contiverem informações de exibição da fonte de dados. Se não tiverem uma referência de exibição da fonte de dados, um erro ocorrerá durante o carregamento. As informações de exibição da fonte de dados podem estar ausentes se você carregar um [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] arquivo. smdl de um projeto de modelo de relatório. Nos projetos de modelo de relatório, informações de exibição da fonte de dados são armazenadas em um arquivo separado e não no próprio arquivo .smdl.  
  
     Arquivos de modelo que não contêm informações de exibição da fonte de dados (e podem, portanto, ser carregados com êxito) são aqueles que foram publicados anteriormente em um servidor de relatórios e salvos em um arquivo do sistema de arquivos. Se você abrir a página Propriedades Gerais de um modelo e clicar em **Editar** para abrir o modelo, poderá salvá-lo em um arquivo e carregá-lo como um novo modelo no servidor de relatório. O arquivo .smdl carregado subsequentemente terá todas as informações necessárias para a publicação do modelo.  
  
-   Todos os outros tipos de arquivo que você carrega são armazenados como recursos. Isso inclui arquivos .rds que contêm informações de conexão da fonte de dados de relatório. O carregamento de um arquivo .rds não produz um item da fonte de dados compartilhada no servidor de relatório.  
  
 Quando você carrega um item, ele é colocado na pasta atual. Quando o carregamento estiver concluído, você poderá mover o item para outro local.  
  
> [!NOTE]  
>  Este recurso não está disponível em todas as edições do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], consulte [Features Supported by the Editions of SQL Server 2014](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
## <a name="navigation"></a>Navegação  
 Use o procedimento a seguir para navegar para este local na interface do usuário.  
  
### <a name="to-open-the-upload-file-page"></a>Para abrir a página Carregar Arquivo  
  
1.  Abra o Gerenciador de Relatórios e navegue até a pasta na qual você deseja carregar um arquivo.  
  
2.  Na barra de ferramentas, clique em **Carregar Arquivo**.  
  
## <a name="options"></a>Opções  
 **Arquivo a ser Carregado**  
 Exibe o caminho totalmente qualificado do arquivo que você está copiando do sistema de arquivos.  
  
 **Procurar**  
 Clique para escolher um arquivo do sistema de arquivos.  
  
 **Nome**  
 Digite o nome do arquivo como ele aparecerá no namespace do servidor de relatório. Um nome deve conter pelo menos um caractere alfanumérico. Também pode conter espaços e certos símbolos. Não use os caracteres ; ? : \@ & = +, $ * \< > | "ou/ao especificar um nome de item.  
  
 **Substituir item, se existir**  
 Marque esta caixa de seleção se você quiser substituir um item existente por uma versão mais nova. Para substituir uma versão existente, o nome do novo item e o item existente devem corresponder exatamente.  
  
## <a name="see-also"></a>Consulte Também  
 [Gerenciador de Relatórios &#40;Modo Nativo do SSRS&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [Página de conteúdo &#40;Report Manager&#41;](../../2014/reporting-services/contents-page-report-manager.md)   
 [Ajuda F1 Report Manager](../../2014/reporting-services/report-manager-f1-help.md)   
 [Carregar arquivos em uma pasta](report-server/upload-files-to-a-folder.md)  
  
  
