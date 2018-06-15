---
title: Acessar assemblies personalizados por meio de expressões | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.component: custom-assemblies
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- expressions [Reporting Services], custom assemblies
- static member calls
- instance member calls [Reporting Services]
- calling class members
- custom assemblies [Reporting Services], expressions
ms.assetid: 917c4d47-1a95-4f54-98b1-e8cb2165d90f
caps.latest.revision: 32
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 726f21d764504fc72fc833dbff10acd380f4087d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33017403"
---
# <a name="accessing-custom-assemblies-through-expressions"></a>Acessando assemblies personalizados por meio de expressões
  Depois de criar um assembly personalizado, disponibilize-o para o Designer de Relatórios ou para o servidor de relatório, de ter adicionado a política de segurança apropriada, e de ter adicionado uma referência ao seu assembly personalizado à sua definição de relatório, você poderá acessar os membros das classes do seu assembly usando expressões de relatório. Para consultar o código personalizado em uma expressão, você deve chamar o membro de uma classe dentro do assembly. A maneira de fazer isso depende do método ser estático ou baseado em instância.  
  
## <a name="calling-static-members-from-a-report-definition-file"></a>Chamando membros estáticos de um arquivo de definição de relatório  
 Os membros estáticos pertencem à própria classe ou tipo e não a um objeto instanciado. Esses membros podem ser acessados por sua chamada direta a partir da classe. Você deve usar os membros estáticos para chamar funções personalizadas em um relatório sempre que possível, porque eles têm um desempenho melhor. Para chamar um membro estático, você precisa referenciá-lo como uma expressão que usa a forma =*Namespace.Class.Method*.  
  
#### <a name="to-call-static-members"></a>Para chamar membros estáticos  
  
-   Para chamar um membro estático, defina a sua expressão como o nome totalmente qualificado do membro, que inclui o namespace, o nome da classe e o nome do membro. O exemplo a seguir chama o método **ToGBP**, que converte o valor do campo **StandardCost** de dólares para libras esterlinas e o exibe em um relatório:  
  
    ```  
    =CurrencyConversion.DollarCurrencyConversion.ToGBP(Fields!StandardCost.Value)  
    ```  
  
### <a name="important-information-regarding-static-fields-and-properties"></a>Informações importantes sobre campos estáticos e propriedades  
 Atualmente, todos os relatórios são executados no mesmo domínio do aplicativo. Isso significa que relatórios com dados específicos do usuário e estáticos exibem esses dados a outras instâncias do mesmo relatório. Essa condição pode fazer com que os dados estáticos de um usuário estejam disponíveis a todos os usuários que executam um relatório específico no momento. Por esse motivo, é altamente recomendável que você não use campos estáticos ou propriedades em assemblies personalizados ou no elemento **Code**. Em vez disso, use campos de instância ou propriedades em seus relatórios. Os métodos estáticos ainda poderão ser usados, já que não armazenam estado ou dados.  
  
## <a name="calling-instance-members-from-a-report-definition-file"></a>Chamando membros de instância de um arquivo de definição de relatório  
 Se o seu assembly personalizado contém membros de instância que você precisa acessar em uma definição de relatório, adicione um nome de instância para a sua classe ao relatório. Você pode adicionar um nome de instância a uma classe usando a guia **Código** da caixa de diálogo **Propriedades do Relatório**. Para obter mais informações sobre adição de instâncias de classes a um relatório, consulte [Referências a código personalizado e assemblies em expressões no Designer de Relatórios &#40;SSRS&#41;](../../reporting-services/report-design/custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md).  
  
 Para chamar um membro estático, você terá de referenciá-lo como uma expressão com a forma =Code *.InstanceName.Method*.  
  
#### <a name="to-call-instance-members"></a>Para chamar membros de instância  
  
-   Para chamar um membro de instância de um assembly personalizado, referencie a palavra-chave **Code** seguida pelo nome de instância e o método. O exemplo a seguir chama um método de instância **ToEUR** que converte o valor do campo **StandardCost** de dólares para euros e o exibe em um relatório:  
  
    ```  
    =Code.m_myDollarCoversion.ToEUR(Fields!StandardCost.Value)  
    ```  
  
## <a name="see-also"></a>Consulte Também  
 [Usar assemblies personalizados com relatórios](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)  
  
  
