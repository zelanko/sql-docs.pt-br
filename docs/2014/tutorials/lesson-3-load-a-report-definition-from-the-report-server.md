---
title: 'Lição 3: Carregar uma definição de relatório do servidor de relatório | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 5ad8b31c-43b0-4481-a31b-090cbed4a438
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: d4c51002c8c829417c63a0dd6c59a3538604fd81
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63042502"
---
# <a name="lesson-3-load-a-report-definition-from-the-report-server"></a>Lição 3: Carregar uma definição de relatório do Servidor de Relatório
  Depois que você criar seu projeto e gerar as classes do esquema RDL, estará pronto para carregar uma definição de relatório do servidor de relatório.  
  
### <a name="to-load-a-report-definition"></a>Para carregar uma definição de relatório  
  
1.  Adicione um campo particular na parte superior a `ReportUpdater` classe (módulo se você estiver usando [!INCLUDE[vbprvb](../includes/vbprvb-md.md)]) para o `Report` classe. Este campo será usado para manter uma referência ao relatório carregado do servidor de relatório enquanto durar o aplicativo.  
  
    ```csharp  
    private Report _report;  
    ```  
  
    ```vb  
    Private m_report As Report  
    ```  
  
2.  Substitua o código para o método `LoadReportDefinition()` no arquivo Program.cs (Module1.vb para o [!INCLUDE[vbprvb](../includes/vbprvb-md.md)]) pelo seguinte código:  
  
    ```csharp  
    private void LoadReportDefinition()  
    {  
        System.Console.WriteLine("Loading Report Definition");  
  
        string reportPath =   
            "/AdventureWorks 2012 Sample Reports/Company Sales 2012";  
  
        // Retrieve the report definition   
        // from the report server  
        byte[] bytes =   
            _reportService.GetItemDefinition(reportPath);  
  
        if (bytes != null)  
        {  
            XmlSerializer serializer =   
                new XmlSerializer(typeof(Report));  
  
            // Load the report bytes into a memory stream  
            using (MemoryStream stream = new MemoryStream(bytes))  
            {  
                // Deserialize the report stream to an   
                // instance of the Report class  
                _report = (Report)serializer.Deserialize(stream);  
            }  
        }  
    }  
    ```  
  
    ```vb  
    Private Sub LoadReportDefinition()  
  
        System.Console.WriteLine("Loading Report Definition")  
  
        Dim reportPath As String = _  
            "/AdventureWorks 2012 Sample Reports/Company Sales 2012"  
  
        'Retrieve the report definition   
        'from the report server  
        Dim bytes As Byte() = _  
            m_reportService.GetItemDefinition(reportPath)  
  
        If Not (bytes Is Nothing) Then  
  
            Dim serializer As XmlSerializer = _  
                New XmlSerializer(GetType(Report))  
  
            'Load the report bytes into a memory stream  
            Using stream As MemoryStream = New MemoryStream(bytes)  
  
                'Deserialize the report stream to an   
                'instance of the Report class  
                m_report = CType(serializer.Deserialize(stream), _  
                                 Report)  
  
            End Using  
  
        End If  
  
    End Sub  
    ```  
  
## <a name="next-lesson"></a>Próxima lição  
 Na próxima lição, você escreverá código para atualizar a definição de relatório carregada do servidor de relatório. Confira [Lição 4: Atualizar a definição de relatório de modo programático](../../2014/tutorials/lesson-4-update-the-report-definition-programmatically.md).  
  
## <a name="see-also"></a>Consulte também  
 [Atualizando relatórios por meio de Classes geradas a partir do esquema RDL &#40;Tutorial do SSRS&#41;](../../2014/tutorials/updating-reports-using-classes-generated-from-the-rdl-schema-ssrs-tutorial.md)   
 [Linguagem RDL &#40;SSRS&#41;](../reporting-services/reports/report-definition-language-ssrs.md)  
  
  
