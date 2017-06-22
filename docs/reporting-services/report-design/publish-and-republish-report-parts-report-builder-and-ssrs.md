---
title: "Publicar e republicar partes de relatório (construtor de relatórios e SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 92dce484-f39b-403c-9caf-d8772bc3aca3
caps.latest.revision: 9
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 03b06d981e4ff824fbdca3f598271fce666237af
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="publish-and-republish-report-parts-report-builder-and-ssrs"></a>Publicar e republicar partes de relatório (Construtor de Relatórios e SSRS)
  Partes de relatório são itens de relatório paginados que foram publicados separadamente em um servidor de relatório e que podem ser reutilizados em outros relatórios paginados. Você pode publicar uma parte de relatório com configurações padrão em um local padrão ou pode editar os metadados de parte do relatório, como nome e descrição e salvá-lo em outro lugar no servidor de relatório. Também será possível salvá-lo em um site do SharePoint integrado com um servidor de relatório se você tiver as permissões corretas.  
  
 Você pode publicar apenas a parte de relatório, com o conjunto de dados do qual ela depende ou está inserida, ou pode publicar o conjunto de dados separadamente. Se você publicar o conjunto de dados separadamente, ele se tornará um conjunto de dados compartilhado e a parte de relatório será vinculada a ele. Para obter mais informações, consulte [Partes de relatório e conjuntos de dados no Construtor de Relatórios](../../reporting-services/report-data/report-parts-and-datasets-in-report-builder.md).  
  
 Você pode publicar novamente uma parte de relatório existente. Se tiver permissões, você poderá salvar sobre a instância original da parte de relatório no servidor, mesmo que não a tenha criado. Também é possível publicá-la como uma nova parte de relatório e salvá-la no mesmo ou em outro local.  
  
## <a name="to-publish-a-report-part"></a>Para publicar uma parte de relatório  
  
1.  No menu Construtor de Relatórios, clique em **Publicar Partes de Relatório**.  
  
     Se você não estiver conectado a um servidor de relatório, receberá uma solicitação para se conectar. Se você não puder se conectar a um servidor de relatório, não poderá publicar partes de relatório.  
  
2.  Para salvar suas partes de relatório com configurações padrão para o local padrão, clique em **Publicar todas as partes de relatório com configurações padrão**.  
  
     Caso contrário, clique em **Examine e modifique as partes de relatório antes da publicação**.  
  
3.  Edite o nome da parte de relatório e a descrição: clique duas vezes no nome para editá-lo e clique no campo **Descrição** para adicionar uma descrição.  
  
    > [!NOTE]  
    >  É conveniente dar à parte de relatório nome e descrição claros, para facilitar a identificação durante a pesquisa. O comprimento máximo para o nome de uma parte de relatório é 260 caracteres para o caminho inteiro, inclusive os nomes das pastas no servidor, seguido pelo nome real da parte de relatório.  
  
4.  Para salvar sua parte de relatório em outra pasta que não a padrão, clique no botão **Procurar** .  
  
5.  Depois de definir as opções para todas as partes de relatório no relatório, clique em **Publicar**.  
  
     Depois que você publicar as partes de relatório, a caixa de diálogo mostrará as que foram publicadas com êxito e as que não foram. Você pode exibir detalhes na caixa de diálogo **Publicar Partes de Relatório** para as partes de relatório que não foram publicadas.  
  
6.  Clique em **Fechar**.  
  
## <a name="to-republish-a-report-part"></a>Para publicar uma parte de relatório novamente  
  
1.  Siga o procedimento anterior para publicar uma parte de relatório.  
  
2.  Na caixa de diálogo **Publicar Partes de Relatório** , se você clicar em **Publicar como uma Nova Cópia da Parte de Relatório**, o Construtor de Relatórios não salvará sobre a parte de relatório existente no servidor, mas criará outra parte de relatório.  
  
> [!NOTE]  
>  Se você publicá-la como uma nova parte de relatório, ela terá uma nova ID exclusiva. Ela não receberá mais atualizações se a parte de relatório original for alterada.  
  
## <a name="see-also"></a>Consulte também  
 [Partes de relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/report-parts-report-builder-and-ssrs.md)   
 [Partes de relatório e conjuntos de dados no Construtor de Relatórios](../../reporting-services/report-data/report-parts-and-datasets-in-report-builder.md)   
 [Solução de problemas de partes de relatório (Construtor de Relatórios e SSRS)](http://msdn.microsoft.com/en-us/d9fe1932-46e7-421b-a8a9-4c54d9576e94)   
 [Verificar ou desativar atualizações (Construtor de Relatórios e SSRS)](http://msdn.microsoft.com/en-us/9c69792d-d7c4-453b-ae2f-6d2d071d8606)   
 [Procurar partes de relatório e definir uma pasta padrão &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/browse-for-report-parts-and-set-a-default-folder-report-builder-and-ssrs.md)  
  
  
