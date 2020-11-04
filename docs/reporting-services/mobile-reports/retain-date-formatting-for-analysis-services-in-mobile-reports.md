---
title: Reter a formatação de data para o Analysis Services em relatórios móveis | Reporting Services | Microsoft Docs
description: No Publicador de Relatórios Móveis, adicione uma medida a um conjunto de dados compartilhado no Construtor de Relatórios para que as fontes de dados do Analysis Services mantenham seu tipo de dados.
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.topic: conceptual
ms.assetid: e9a9a199-40e3-4381-b250-1b99fb83aa62
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 5fef66452820975107e06e20a4085978163d957d
ms.sourcegitcommit: ea0bf89617e11afe85ad85309e0ec731ed265583
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/28/2020
ms.locfileid: "92907074"
---
# <a name="retain-date-formatting-for-analysis-services-in-mobile-reports"></a>Reter a formatação de data para Analysis Services em relatórios móveis
Adicione uma medida para um conjunto de dados compartilhado no Construtor de Relatórios até as datas em fontes de dados [!INCLUDE[ssASnoversion_md](../../includes/ssasnoversion-md.md)] que mantêm seus tipos de dados em [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-short.md)].

O tipo de retorno padrão para consultas do [!INCLUDE[ssASnoversion_md](../../includes/ssasnoversion-md.md)] é uma cadeia de caracteres.  Quando você cria um conjunto de dados no Construtor de Relatórios do [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] , o tipo de cadeia de caracteres é respeitado e salvo no servidor. 

No entanto, quando o renderizador de tabela JSON processa o conjunto de dados, ele lê o valor da coluna como uma cadeia de caracteres e renderiza as cadeias de caracteres.  Em seguida, quando [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-long.md)] busca da tabela, ele também vê apenas cadeias de caracteres.

A solução para isso é adicionar um membro calculado quando você estiver criando um conjunto de dados compartilhado no Construtor de Relatórios. Ele funciona para ambos os modelos multidimensionais e tabulares do [!INCLUDE[ssASnoversion_md](../../includes/ssasnoversion-md.md)] .

## <a name="create-a-measure-to-retain-a-date-field-data-type"></a>Criar uma medida para reter um tipo de dados do campo de data

1. Criar uma medida para armazenar o valor do campo de data em questão e, no campo expressão, escolha o nível hierárquico/da data e acrescente **.CurrentMember.MemberValue**. Por exemplo:
 
   [Internet Sales].[Ship Date].CurrentMember.MemberValue
   
   ![Captura de tela da caixa de diálogo Construtor de Membro Calculado com a caixa de texto Expressão em destaque.](../../reporting-services/mobile-reports/media/ssas-calculated-member-report-builder.png)
   
2. Agora você pode acrescentar esse membro calculado para o conjunto de colunas arrastando-o da lista de Membros Calculados na parte inferior esquerda e soltá-lo na grade da coluna à direita.  

   ![Captura de tela do Designer de Consultas com a seção de Membros Calculados em destaque.](../../reporting-services/mobile-reports/media/ssas-query-designer-calculated-member-report-builder.png) 
   
### <a name="see-also"></a>Confira também

-  [Dados para relatórios móveis do Reporting Services](../../reporting-services/mobile-reports/data-for-reporting-services-mobile-reports.md)
-  [Preparar dados para relatórios móveis do Reporting Services](../../reporting-services/mobile-reports/prepare-data-for-reporting-services-mobile-reports.md)
