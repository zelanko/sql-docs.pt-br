---
title: Exibir números de página ou outras propriedades do relatório (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: c7d95245-4709-4d04-acb4-59bf71e60d97
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 576d2fc5ba8ea023e69fe9b6136a676b188366e4
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/15/2019
ms.locfileid: "56296794"
---
# <a name="display-page-numbers-or-other-report-properties-report-builder-and-ssrs"></a>Exibir números de página ou outras propriedades do relatório (Construtor de Relatórios e SSRS)
  É fácil adicionar números de página, um título de relatório, nome de arquivo e outras propriedades de relatório aos cabeçalhos ou rodapés de seu relatório. Essas propriedades são armazenadas como campos na pasta Campos Internos no painel de dados do relatório:  
  
-   Tempo de execução  
  
-   Número de página  
  
-   Pasta Relatório  
  
-   Nome do relatório  
  
-   URL do servidor de relatório  
  
-   Total de páginas  
  
-   ID de usuário  
  
-   Linguagem  
  
 Para um número de página, talvez você queira adicionar a palavra "Página" antes do número. Você também pode desejar mostrar o número total de páginas.  
  
> [!NOTE]  
>  A adição do número total de páginas ao rodapé pode reduzir a velocidade desempenho quando você executar ou visualizar seu relatório.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-page-number-or-other-report-properties"></a>Para adicionar um número de página ou outras propriedades de relatório  
  
1.  No painel de dados do relatório, expanda a pasta Campos Internos.  
  
    > [!NOTE]  
    >  Se o painel de dados do relatório não estiver visível, na guia Exibir, clique em **Dados do Relatório**.  
  
2.  Arraste o campo **Número da Página** do painel de dados do relatório para o cabeçalho ou o rodapé do relatório.  
  
    > [!NOTE]  
    >  O rodapé de página é adicionado automaticamente ao relatório. Para adicionar um cabeçalho de página, na guia **Inserir** , clique em **Cabeçalho**e em **Adicionar Cabeçalho**.  
    >   
    >  Uma caixa de texto que contém a expressão simples [&PageNumber] é adicionada.  
  
### <a name="to-add-the-word-page-before-the-page-number"></a>Para adicionar a palavra "Página" antes do número de página  
  
1.  Clique com o botão direito do mouse na caixa de texto que contém [&PageNumber] e clique em **Expressões**.  
  
     A caixa de texto **Definir expressão para: Valor** contém a expressão =Globals!PageNumber.  
  
2.  Coloque o cursor depois do sinal de = e digite **"Page " &**.  
  
     Agora, a expressão é ="Página "&Globals! PageNumber  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-add-total-number-of-pages-after-the-page-number"></a>Para adicionar o número total de páginas após o número de página  
  
1.  Clique com o botão direito do mouse na caixa de texto com a expressão e clique em **Expressões**.  
  
2.  Digite **&" de "&** no final da expressão.  
  
3.  No painel Categoria, expanda **Campos Internos** e clique duas vezes em **TotalPages**.  
  
     Agora, a expressão é ="Página "&Globals!PageNumber &" de "&Globals!TotalPages  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Consulte Também  
 [Cabeçalhos e rodapés de página &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/page-headers-and-footers-report-builder-and-ssrs.md)   
 [Formatar texto em uma caixa de texto &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/format-text-in-a-text-box-report-builder-and-ssrs.md)  
  
  
