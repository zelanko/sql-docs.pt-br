---
title: "Acessando Assemblies personalizados por meio de expressões | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
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
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 70ff488827e5289d401bf62b67a82a08ecc25f70
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="accessing-custom-assemblies-through-expressions"></a>Acessando assemblies personalizados por meio de expressões
  Depois de criar um assembly personalizado, disponibilize-o para o Designer de Relatórios ou para o servidor de relatório, de ter adicionado a política de segurança apropriada, e de ter adicionado uma referência ao seu assembly personalizado à sua definição de relatório, você poderá acessar os membros das classes do seu assembly usando expressões de relatório. Para consultar o código personalizado em uma expressão, você deve chamar o membro de uma classe dentro do assembly. A maneira de fazer isso depende do método ser estático ou baseado em instância.  
  
## <a name="calling-static-members-from-a-report-definition-file"></a>Chamando membros estáticos de um arquivo de definição de relatório  
 Os membros estáticos pertencem à própria classe ou tipo e não a um objeto instanciado. Esses membros podem ser acessados por sua chamada direta a partir da classe. Você deve usar os membros estáticos para chamar funções personalizadas em um relatório sempre que possível, porque eles têm um desempenho melhor. Para chamar um membro estático, você precisa referenciá-lo como uma expressão que usa a forma =*Method*.  
  
#### <a name="to-call-static-members"></a>Para chamar membros estáticos  
  
-   Para chamar um membro estático, defina a sua expressão como o nome totalmente qualificado do membro, que inclui o namespace, o nome da classe e o nome do membro. A exemplo a seguir chama o **ToGBP** método, que converte o **StandardCost** campo valor de dólares para libras esterlinas e o exibe em um relatório:  
  
    ```  
    =CurrencyConversion.DollarCurrencyConversion.ToGBP(Fields!StandardCost.Value)  
    ```  
  
### <a name="important-information-regarding-static-fields-and-properties"></a>Informações importantes sobre campos estáticos e propriedades  
 Atualmente, todos os relatórios são executados no mesmo domínio do aplicativo. Isso significa que relatórios com dados específicos do usuário e estáticos exibem esses dados a outras instâncias do mesmo relatório. Essa condição pode fazer com que os dados estáticos de um usuário estejam disponíveis a todos os usuários que executam um relatório específico no momento. Por esse motivo, é altamente recomendável que você não use campos estáticos ou propriedades em assemblies personalizados ou no **código** elemento; em vez disso, use propriedades ou campos de instância em seus relatórios. Os métodos estáticos ainda poderão ser usados, já que não armazenam estado ou dados.  
  
## <a name="calling-instance-members-from-a-report-definition-file"></a>Chamando membros de instância de um arquivo de definição de relatório  
 Se o seu assembly personalizado contém membros de instância que você precisa acessar em uma definição de relatório, adicione um nome de instância para a sua classe ao relatório. Você pode adicionar um nome de instância para uma classe usando o **código** guia o **propriedades do relatório** caixa de diálogo. Para obter mais informações sobre como adicionar instâncias de classes para um relatório, consulte [código personalizado e referências de Assembly em expressões no Designer de relatórios &#40; SSRS &#41; ](../../reporting-services/report-design/custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md).  
  
 Para chamar um membro estático, você precisa referenciá-lo como uma expressão que usa a forma = Code*. Method*.  
  
#### <a name="to-call-instance-members"></a>Para chamar membros de instância  
  
-   Para chamar um membro de instância de um assembly personalizado, você deve fazer referência a **código** seguido pelo nome da instância e o método de palavra-chave. O exemplo a seguir chama um método de instância **ToEUR** que converte o **StandardCost** campo valor de dólares em euros e o exibe em um relatório:  
  
    ```  
    =Code.m_myDollarCoversion.ToEUR(Fields!StandardCost.Value)  
    ```  
  
## <a name="see-also"></a>Consulte também  
 [Usando assemblies personalizados com relatórios](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)  
  
  
