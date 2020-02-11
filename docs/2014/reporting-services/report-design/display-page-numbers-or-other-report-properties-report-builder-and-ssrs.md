---
title: Exibir números de página ou outras propriedades do relatório (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: c7d95245-4709-4d04-acb4-59bf71e60d97
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 8530a13af0e0ae6f1b769adcaa7cb6e9a3fbc0ae
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66106043"
---
# <a name="display-page-numbers-or-other-report-properties-report-builder-and-ssrs"></a>Exibir números de página ou outras propriedades do relatório (Construtor de Relatórios e SSRS)
  É fácil adicionar números de página, um título de relatório, nome de arquivo e outras propriedades de relatório aos cabeçalhos ou rodapés de seu relatório. Essas propriedades são armazenadas como campos na pasta Campos Internos no painel de dados do relatório:  
  
-   Tempo de execução  
  
-   Número da página  
  
-   Pasta Relatório  
  
-   Nome do relatório  
  
-   URL do servidor de relatório  
  
-   Total de páginas  
  
-   Id de Usuário  
  
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
  
     A caixa de texto **Definir Expressão para: Valor** contém a expressão =Globals!PageNumber.  
  
2.  Coloque o cursor depois do sinal de = e digite `"Page " &`.  
  
     Agora, a expressão é ="Página "&Globals! PageNumber  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-add-total-number-of-pages-after-the-page-number"></a>Para adicionar o número total de páginas após o número de página  
  
1.  Clique com o botão direito do mouse na caixa de texto com a expressão e clique em **Expressões**.  
  
2.  Digite **&" de "&** no final da expressão.  
  
3.  No painel Categoria, expanda **Campos Internos** e clique duas vezes em **TotalPages**.  
  
     Agora, a expressão é ="Página "&Globals!PageNumber &" de "&Globals!TotalPages  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Consulte Também  
 [Cabeçalhos e rodapés de página &#40;Construtor de Relatórios e SSRS&#41;](page-headers-and-footers-report-builder-and-ssrs.md)   
 [Formatar o texto em uma caixa de texto &#40;Construtor de Relatórios e SSRS&#41;](format-text-in-a-text-box-report-builder-and-ssrs.md)  
  
  
