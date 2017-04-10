---
title: "Formatar o texto em uma caixa de texto (Construtor de Relat&#243;rios e SSRS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: df0794b5-96b0-4034-bd17-1be7f31e29db
caps.latest.revision: 8
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 8
---
# Formatar o texto em uma caixa de texto (Construtor de Relat&#243;rios e SSRS)
  Você pode formatar qualquer parte do texto dentro de uma caixa de texto de forma independente e mesclar texto de espaço reservado e texto estático em uma caixa de texto. Essa capacidade de mesclar formatos e adicionar texto de espaço reservado permite criar mesclagens de mensagens ou modelos de texto no seu relatório. Qualquer expressão pode ser definida e formatada separadamente usando um espaço reservado.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### Para combinar vários formatos em uma caixa de texto  
  
1.  Na guia **Inserir** , clique em **Caixa de Texto**. Clique na superfície de design e arraste-a para criar uma caixa com o tamanho desejado.  
  
2.  Na caixa de texto, selecione o texto que deseja formatar.  
  
3.  Clique com o botão direito do mouse no texto selecionado e clique em **Propriedades do Texto**.  
  
4.  Defina as opções de formatação. Por exemplo, na guia **Geral**:  
  
    -   **Dica de Ferramenta** Digite um texto ou uma expressão que seja avaliada como uma Dica de Ferramenta. A Dica de Ferramenta é exibida quando o usuário pausa o ponteiro sobre o item em um relatório  
  
    -   **Tipo de marcação** Selecione uma opção para indicar como o texto selecionado será renderizado:  
  
         **Texto Sem Formatação** Exibe o texto selecionado como texto simples. O HTML será tratado como texto literal.  
  
         **HTML** Exibe o texto selecionado como HTML. Se o valor da expressão do espaço reservado contiver marcas HTML válidas, elas serão renderizadas como HTML. Para obter mais informações, consulte [Importando HTML para um relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/importing-html-into-a-report-report-builder-and-ssrs.md).  
  
5.  Clique em **OK**.  
  
6.  Repita as etapas de 2 a 5 para cada texto restante que desejar formatar.  
  
### Para formatar o texto e os espaços reservados diferentemente na mesma caixa de texto  
  
1.  Na guia **Inserir**, clique em **Lista**. Clique na superfície de design e arraste-a para criar uma caixa com o tamanho desejado. A caixa de diálogo **Propriedades do Conjunto de Dados** é aberta. Você pode usar um conjunto de dados compartilhado ou um conjunto de dados inserido em seu relatório. Para obter mais informações, clique em [Caixa de diálogo Propriedades do Conjunto de Dados, Consulta &#40;Construtor de Relatórios&#41;](../../reporting-services/report-data/dataset-properties-dialog-box-query-report-builder.md) ou [Caixa de diálogo Propriedades do Conjunto de Dados, Consulta](../Topic/Dataset%20Properties%20Dialog%20Box,%20Query.md).  
  
2.  Na guia **Inserir** , clique em **Caixa de Texto**. Clique na lista e arraste-a para criar uma caixa com o tamanho desejado.  
  
3.  Digite um rótulo na caixa de texto — por exemplo, **Meu Campo**:.  
  
4.  Arraste um campo do conjunto de dados para a caixa de texto. Será criado um espaço reservado para seu campo.  
  
5.  Para formatação básica, selecione o texto do espaço reservado e clique em um das opções de formatação no grupo **Fonte** na guia **Página Inicial**. Por exemplo, clique no botão **Negrito**.  
  
     Para obter mais opções de formatação, clique com o botão direito do mouse no texto do espaço reservado e clique em **Propriedades do Espaço Reservado**.  
  
6.  Clique em **OK**. No modo de exibição de Design de relatório, a caixa de texto deverá conter "**Meu Campo**: [*FieldName*]", em que *FieldName* é o nome do seu campo.  
  
7.  Clique em **Executar**.  
  
 A lista é repetida uma vez para cada valor no campo e o espaço reservado *FieldName* é substituído sempre pelo valor daquele campo no conjunto de dados.  
  
## Consulte também  
 [Caixas de texto &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/text-boxes-report-builder-and-ssrs.md)   
 [Formatando texto e espaços reservados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/formatting-text-and-placeholders-report-builder-and-ssrs.md)   
 [Usos de expressões em relatórios &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Exemplos de expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Adicionar um HTML a um relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/add-html-into-a-report-report-builder-and-ssrs.md)   
 [Tabelas, matrizes e listas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [Formatando números e datas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/formatting-numbers-and-dates-report-builder-and-ssrs.md)   
 [Caixa de diálogo Propriedades do Espaço Reservado, Geral &#40;Construtor de Relatórios e SSRS&#41;](../Topic/Placeholder%20Properties%20Dialog%20Box,%20General%20\(Report%20Builder%20and%20SSRS\).md)  
  
  