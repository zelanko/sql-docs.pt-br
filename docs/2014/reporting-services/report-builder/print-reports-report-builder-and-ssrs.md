---
title: Imprimir relatórios (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 4bad1b6e-7d94-4b17-9502-ccd3dce0fdd9
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 7f916e8acf45c822439a116bc5ad1ff40a11d2de
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66107703"
---
# <a name="print-reports-report-builder-and-ssrs"></a>Imprimir relatórios (Construtor de Relatórios e SSRS)
  Depois de salvar um relatório em um servidor de relatório, você pode exibir e imprimir o relatório de um navegador, do Gerenciador de Relatórios ou qualquer aplicativo usado para exibir um relatório exportado. Antes de salvar um relatório, você pode imprimi-lo quando o visualiza.  
  
 Todo o processamento de impressão é executado sob demanda e no computador cliente. Não existe funcionalidade de impressão no servidor que permita encaminhar um trabalho de impressão diretamente de um servidor de relatório para uma impressora conectada ao servidor Web. As impressoras e opções de impressão são selecionadas por usuários de relatórios individuais, usando uma caixa de diálogo **Imprimir** padrão.  
  
 Os autores de relatório que criam relatórios especificamente para a saída de impressão podem usar as quebras de página, cabeçalhos/ rodapés de página, expressões e imagens de plano de fundo para criar um design com base na impressão. Os exemplos de elementos de design de relatório destinados à saída de impressão podem incluir termos e condições impressas no verso de cada relatório ou elementos gráficos e de texto que imitam papel timbrado.  
  
 Devido à maneira como a paginação é implementada para formatos de renderização distintos, talvez você não consiga obter resultados de saída de impressão ideais para todos os relatórios em todos os formatos de renderização. Esta lista apresenta exemplos:  
  
1.  As páginas de relatórios se destinam a acomodar volumes de dados variáveis. Os relatórios que incluem uma matriz, por exemplo, podem fazer com que uma página aumente tanto na horizontal quanto na vertical, conforme um usuário alternar interativamente linhas e colunas. Um usuário que não expande uma matriz obterá resultados de impressão diferentes de um usuário que o faz.  
  
2.  Não é possível combinar as páginas nos modos retrato e paisagem no mesmo relatório, nem criar um layout com base na impressão que substitua ou coexista com o layout de um relatório, conforme renderizado em um navegador ou em outro aplicativo.  
  
3.  Para a maioria dos relatórios exportados, as impressões de relatório incluem tudo que é visível no relatório, conforme visualizado pelo usuário em um monitor de computador. O espaço em branco da superfície de design do relatório é preservado. Para adicionar ou remover páginas em branco adicionais horizontalmente, altere a largura de página do relatório.  
  
> [!NOTE]  
>  As impressões de relatórios HTML só poderão incluir o conteúdo na primeira página se você estiver usando o comando Imprimir do navegador. Você pode obter resultados melhores se imprimir relatórios HTML usando o recurso de impressão do cliente [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Para obter mais informações, consulte [Imprimir relatórios em um navegador com o controle de impressão &#40;Construtor de Relatórios e SSRS&#41;](print-reports-from-a-browser-with-the-print-control-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="in-this-section"></a>Nesta seção  
 [Imprimir relatórios em um navegador com o controle de impressão &#40;Construtor de Relatórios e SSRS&#41;](print-reports-from-a-browser-with-the-print-control-report-builder-and-ssrs.md)  
 Descreve como usar a impressão do lado do cliente para imprimir relatórios de seu navegador da Web ou Gerenciador de Relatórios.  
  
 [Imprimir relatórios de outros aplicativos &#40;Construtor de Relatórios e SSRS&#41;](print-reports-from-other-applications-report-builder-and-ssrs.md)  
 Descreve como imprimir relatórios exportados para outro aplicativo.  
  
 [Imprimir um relatório &#40;Construtor de Relatórios e SSRS&#41;](print-a-report-report-builder-and-ssrs.md)  
 Fornece instruções passo a passo sobre como imprimir um relatório, como controlar as margens em uma página e como especificar o tamanho do papel para os relatórios que serão renderizados por renderizadores de quebra de página não flexíveis: PDF, Imagem ou Impressão.  
  
## <a name="see-also"></a>Consulte também  
 [Exportando relatórios &#40;relatórios e SSRS&#41;](export-reports-report-builder-and-ssrs.md)   
 [Cabeçalhos e rodapés de página &#40;Construtor de Relatórios e SSRS&#41;](../report-design/page-headers-and-footers-report-builder-and-ssrs.md)   
 [Imagens &#40;Construtor de Relatórios e SSRS&#41;](../report-design/images-report-builder-and-ssrs.md)   
 [Paginação no Reporting Services &#40;Construtor de Relatórios e SSRS&#41;](../report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)  
  
  
