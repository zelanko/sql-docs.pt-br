---
title: "Solucionar problemas de processamento de relatórios do Reporting Services | Microsoft Docs"
ms.custom: 
ms.date: 08/26/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
- reporting-services-sharepoint
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: bb309231-68be-4d68-a44c-c098999c67a2
caps.latest.revision: 4
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 8df3dd891b236ca295a4cc0deebdc5768d06dffa
ms.contentlocale: pt-br
ms.lasthandoff: 08/09/2017

---
# <a name="troubleshoot-processing-of-reporting-services-reports"></a>Processamento de solução de problemas dos relatórios do Reporting Services
Após a recuperação dos dados do relatório, o processador de relatório combina esses dados e as informações de layout. Cada propriedade de item de relatório que tenha uma expressão é avaliada no contexto dos dados e do layout combinado. Use este tópico para ajudar a solucionar esses problemas.   
  
## <a name="my-report-definition-is-not-valid"></a>Minha definição de relatório não é válida.  
Em tempo de execução, o processador de relatório combina dados e elementos de layout na definição do relatório, e avalia as expressões para as propriedades de item de relatório.   
  
O processador de relatório verifica se a definição do relatório (arquivo .rdl) segue o esquema especificado na declaração de namespace no início do arquivo .rdl. Para obter mais informações sobre esquemas RDL, consulte [Localizar a Versão de Esquema de Definição de Relatórios (SSRS)](../../reporting-services/reports/find-the-report-definition-schema-version-ssrs.md).  
  
Além disso, as expressões do relatório avaliadas em tempo de execução devem seguir um conjunto de regras que asseguram que os dados e o layout do relatório possam ser combinados corretamente. Quando o processador de relatório detectar um problema, talvez você veja a seguinte mensagem: A definição do relatório `<report name>` é inválida.  
  
### <a name="report-item-expressions-can-only-refer-to-fields-within-the-current-dataset-scope-or-if-inside-an-aggregate-the-specified-dataset-scope"></a>As expressões de item de relatório só podem fazer referência a campos que estejam no escopo do conjunto de dados atual ou, se estiverem dentro de uma agregação, no escopo do conjunto de dados especificado."  
  
Use a lista a seguir para ajudá-lo a determinar a causa do erro:  
* Quando um relatório tem mais de um conjunto de dados, uma expressão de agregação em uma caixa de texto no corpo do relatório deve especificar um parâmetro de escopo. Por exemplo, `=First(Fields!FieldName.Value, "DataSet1")`.  
  
Para especificar um parâmetro de escopo, forneça o nome de um conjunto de dados, região de dados ou grupo que esteja no escopo para o item de relatório. Para obter mais informações, consulte [Compreendendo o escopo das expressões para totais, agregações e coleções internas (Construtor de Relatórios 3.0 e SSRS)](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md) e [Referência de Expressão (Construtor de Relatórios 3.0 e SSRS)](../../reporting-services/report-design/expression-reference-report-builder-and-ssrs.md).  
  
### <a name="names-of-objects-must-be-greater-than-0-and-less-than-or-equal-to-256-characters"></a>Os nomes de objetos devem ter mais de 0 e menos ou até 256 caracteres.  
O comprimento dos identificadores de objeto em uma definição de relatório está restrito a 256 caracteres. Os identificadores devem diferenciar maiúsculas e minúsculas e ser compatíveis com CLS. Os nomes devem começar com uma letra, consistir em letras, números ou sublinhados (_) e não devem ter espaços. Por exemplo, os nomes de caixas de texto ou de regiões de dados devem seguir estas diretrizes:   
  
Para alterar o nome de um objeto, na barra de ferramentas do painel Propriedades, selecione o item na lista suspensa, vá para **Nome** e insira um nome de objeto válido.   
  
## <a name="a-text-box-displays-error-how-do-i-fix-it"></a>Uma caixa de texto exibe "#Erro"; como faço para corrigir isso?  
A mensagem "#Erro" ocorre quando o processador de relatório avalia expressões nas propriedades de item de relatório em tempo de execução e detecta um erro de conversão de tipo de dados, escopo ou outro.   
  
Um erro de tipo de dados geralmente significa que o tipo de dados padrão ou especificado não tem suporte. Um erro de escopo significa que o escopo especificado não estava disponível na hora em que a expressão foi avaliada.   
  
Para eliminar a mensagem  #Erro, escreva novamente a expressão que causa essa mensagem. Para determinar mais detalhes sobre o problema, exiba a mensagem de erro detalhada.   
  
Na visualização, no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull.md)], exiba a janela Saída. No servidor de relatório, exiba a pilha de chamadas. 
  
  
## <a name="see-also"></a>Consulte também  
[Erros e eventos (Reporting Services)](../../reporting-services/troubleshooting/errors-and-events-reference-reporting-services.md)
[!INCLUDE[feedback_stackoverflow_msdn_connect](../../includes/feedback-stackoverflow-msdn-connect.md)]


