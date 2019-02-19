---
title: Conceitos de parâmetros de relatório (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: b0aa2159-4e49-4713-8824-5ef9a9edbc62
author: markingmyname
ms.author: maghan
ms.openlocfilehash: d01b399ed7e19fb6015c5439442b27cfca88ea46
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/15/2019
ms.locfileid: "56285524"
---
# <a name="report-parameters-concepts-report-builder-and-ssrs"></a>Conceitos de parâmetros de relatório (Construtor de Relatórios e SSRS)
  Você pode adicionar parâmetros a um relatório para vincular relatórios relacionados, controlar a aparência do relatório, filtrar dados de relatórios ou restringir o escopo de um relatório a usuários ou locais específicos.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
 Os parâmetros de relatório são criados das seguintes formas:  
  
-   Automaticamente, quando você define a consulta de conjunto de dados que contém variáveis de consulta. Para cada variável de consulta, são criados um parâmetro de consulta de conjunto de dados e um parâmetro de relatório correspondentes com os mesmos nomes. Um parâmetro de consulta pode ser uma referência a uma variável de consulta ou a um parâmetro de entrada para um procedimento armazenado.  
  
-   Automaticamente, quando você adiciona uma referência a um conjunto de dados compartilhado que contém parâmetros de consulta.  
  
-   Manualmente, quando você cria parâmetros de relatório no painel de dados do relatório. Os parâmetros são umas das coleções internas que você pode incluir em uma expressão em um relatório. Como as expressões são usadas para definir valores em uma definição de relatório, você pode usar parâmetros para controlar a aparência do relatório ou transmitir valores aos sub-relatórios ou relatórios relacionados que também usam parâmetros.  
  
 Para obter mais informações, consulte [Parâmetros de relatório &#40;Construtor de Relatórios e Designer de Relatórios&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md).  
  
 Os parâmetros costumam ser usados para filtrar dados de relatório antes e depois que os dados são retornados ao relatório. Para obter mais informações, consulte [Filtrar, agrupar e classificar dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md).  
  
 Quando você cria um relatório, os parâmetros de relatório são salvos na definição de relatório. Quando você publica um relatório, os parâmetros de relatório são salvos e gerenciados separadamente da definição de relatório. Depois de salvar o relatório no servidor de relatório, você pode fazer o seguinte:  
  
-   Altere os valores de parâmetros de relatório diretamente no servidor de relatório, de modo independente da definição de relatório.  
  
-   Crie vários relatórios vinculados em que cada relatório vinculado é um link para a definição de relatório com um conjunto separado de valores de parâmetros que podem ser gerenciados independentemente no servidor de relatório.  
  
 Se você pretende criar instantâneos de relatório, históricos ou assinaturas para um relatório publicado, precisa compreender como os parâmetros de relatório afetam os requisitos de design para o relatório.  
  
## <a name="see-also"></a>Consulte Também  
 [Conceitos de criação de relatórios &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/report-authoring-concepts-report-builder-and-ssrs.md)   
 [Conjuntos de dados inseridos e compartilhados de relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [Tutorial: Adicionar um parâmetro ao relatório &#40;Construtor de Relatórios&#41;](../../reporting-services/tutorial-add-a-parameter-to-your-report-report-builder.md)  
  
  
