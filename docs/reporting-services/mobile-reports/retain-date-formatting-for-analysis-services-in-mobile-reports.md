---
title: "Manter a formatação de data para Analysis Services em relatórios móveis | O Reporting Services | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e9a9a199-40e3-4381-b250-1b99fb83aa62
caps.latest.revision: 3
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 0a4da31bb1ed09024c6278193e8011b5c7981922
ms.contentlocale: pt-br
ms.lasthandoff: 08/09/2017

---
# <a name="retain-date-formatting-for-analysis-services-in-mobile-reports"></a>Reter a formatação de data para Analysis Services em relatórios móveis
Adicione uma medida para um conjunto de dados compartilhado no Construtor de Relatórios até as datas em fontes de dados [!INCLUDE[ssASnoversion_md](../../includes/ssasnoversion-md.md)] que mantêm seus tipos de dados em [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-short.md)].

O tipo de retorno padrão para consultas do [!INCLUDE[ssASnoversion_md](../../includes/ssasnoversion-md.md)] é uma cadeia de caracteres.  Quando você cria um conjunto de dados no Construtor de Relatórios do [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] , o tipo de cadeia de caracteres é respeitado e salvo no servidor. 

No entanto, quando o renderizador de tabela JSON processa o conjunto de dados, ele lê o valor da coluna como uma cadeia de caracteres e renderiza as cadeias de caracteres.  Em seguida, quando [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-long.md)] busca da tabela, ele também vê apenas cadeias de caracteres.

A solução para isso é adicionar um membro calculado quando você estiver criando um conjunto de dados compartilhado no Construtor de Relatórios. Ele funciona para ambos os modelos multidimensionais e tabulares do [!INCLUDE[ssASnoversion_md](../../includes/ssasnoversion-md.md)] .

## <a name="create-a-measure-to-retain-a-date-field-data-type"></a>Criar uma medida para reter um tipo de dados do campo de data

1. Criar uma medida para armazenar o valor do campo de data em questão e, no campo expressão, escolha o nível hierárquico/da data e acrescente **.CurrentMember.MemberValue**. Por exemplo:
 
   [Internet Sales].[Ship Date].CurrentMember.MemberValue
   
   ![ssas-calculated-member-report-builder](../../reporting-services/mobile-reports/media/ssas-calculated-member-report-builder.png)
   
2. Agora você pode acrescentar esse membro calculado para o conjunto de colunas arrastando-o da lista de Membros Calculados na parte inferior esquerda e soltá-lo na grade da coluna à direita.  

   ![ssas-query-designer-calculated-member-report-builder](../../reporting-services/mobile-reports/media/ssas-query-designer-calculated-member-report-builder.png) 
   
### <a name="see-also"></a>Consulte também

-  [Dados para relatórios móveis do Reporting Services](../../reporting-services/mobile-reports/data-for-reporting-services-mobile-reports.md)
-  [Preparar dados para relatórios móveis do Reporting Services](../../reporting-services/mobile-reports/prepare-data-for-reporting-services-mobile-reports.md)
