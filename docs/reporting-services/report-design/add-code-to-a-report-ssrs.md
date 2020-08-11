---
title: Adicionar código a um relatório | Microsoft Docs
description: Saiba como chamar o próprio código personalizado para qualquer expressão que você tenha em seu relatório no Construtor de Relatórios.
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
helpviewer_keywords:
- code [Reporting Services]
- custom code [Reporting Services]
- expressions [Reporting Services], code
- adding code
- reports [Reporting Services], code
ms.assetid: 00ef8fc6-99fe-49b2-8a22-7eb475881dc4
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 9d54e2ce879e78787b9b51d20c8df83367038c7b
ms.sourcegitcommit: 93e4fd75e8fe0cc85e7949c9adf23b0e1c275465
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/01/2020
ms.locfileid: "84255679"
---
# <a name="add-code-to-a-report-ssrs"></a>Adicionar código a um relatório (SSRS)
  Em qualquer expressão, você pode chamar seu próprio código personalizado. Você pode fornecer código das duas maneiras a seguir:  
  
-   Insira código gravado no [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] diretamente no seu relatório. Se o código fizer referência a um [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] que não é <xref:System.Math> nem <xref:System.Convert>, você deverá adicionar a referência ao relatório. Para obter mais informações, consulte [Adicionar uma referência de assembly a um relatório &#40;SSRS&#41;](../../reporting-services/report-design/add-an-assembly-reference-to-a-report-ssrs.md). Para obter mais informações sobre outras referências que podem ser feitas no código, consulte [Referências a código personalizado e assemblies em expressões no Designer de Relatórios &#40;SSRS&#41;](../../reporting-services/report-design/custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md).  
  
-   Forneça um assembly de código personalizado usando o [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]. Se você fornecer um assembly personalizado, deverá instalá-lo no computador no qual o relatório é criado e no servidor de relatórios no qual o relatório é exibido. Para obter mais informações, consulte [Using Custom Assemblies with Reports](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md).  
  
### <a name="to-add-embedded-code-to-a-report"></a>Para adicionar código inserido em um relatório  
  
1.  No modo de exibição de **Design** , clique com o botão direito do mouse na superfície de design fora da borda do relatório e clique em **Propriedades do Relatório**.  
  
2.  Clique em **Código**.  
  
3.  No **Código personalizado**, digite o código. Erros no código geram avisos quando o relatório é executado. O exemplo a seguir cria uma função personalizada chamada `ChangeWord` que substitui a palavra "`Bike`" por "`Bicycle`".  
  
    ```  
    Public Function ChangeWord(ByVal s As String) As String  
       Dim strBuilder As New System.Text.StringBuilder(s)  
       If s.Contains("Bike") Then  
          strBuilder.Replace("Bike", "Bicycle")  
          Return strBuilder.ToString()  
          Else : Return s  
       End If  
    End Function  
    ```  
  
4.  O exemplo a seguir mostra como transmitir um campo de conjunto de dados nomeado Categoria para esta função em uma expressão:  
  
    ```  
    =Code.ChangeWord(Fields!Category.Value)  
    ```  
  
     Se você adicionar essa expressão a uma célula de tabela que exibe valores de categoria, sempre que a palavra "Bike" estiver no campo de conjunto de dados daquela linha, o valor da célula de tabela exibirá a palavra "Bicicleta".  
  
## <a name="see-also"></a>Consulte Também  
 [Caixa de diálogo Propriedades do Relatório, Código](https://msdn.microsoft.com/library/955d4b11-17b4-4f1c-9690-6e7af54caea7)   
 [Exemplos de expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Referências de coleções de parâmetros &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/built-in-collections-parameters-collection-references-report-builder.md)  
  
  
