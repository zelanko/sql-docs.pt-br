---
title: As regras de nomenclatura (Analysis Services) do objeto | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords: objects [Analysis Services], naming
ms.assetid: b338a60d-4802-4b68-862a-6dc6a3f75e48
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 1493d5236d4c44fe4a496a67a2c435aab703daa8
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="object-naming-rules-analysis-services"></a>Regras de nomenclatura de objeto (Analysis Services)
  Este tópico descreve as convenções de nomenclatura de objeto, bem como as palavras e os caracteres reservados que não podem ser usados em nomes de objetos, códigos ou scripts no [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
##  <a name="bkmk_Names"></a>Convenções de nomenclatura  
 Todo objeto tem as propriedades **Name** e **ID** que devem ser exclusivas no escopo da coleção pai. Por exemplo, duas dimensões podem ter o mesmo nome, desde que cada uma resida em um banco de dados diferente.  
  
 Embora você possa especificar isso manualmente, a **ID** costuma ser gerada automaticamente quando o objeto é criado. Após começar a criar um modelo, nunca altere a **ID** . Todas as referências de objeto em um modelo se baseiam na **ID**. Então, a alteração de uma **ID** pode facilmente resultar na corrupção do modelo.  
  
 Os objetos**DataSource** e **DataSourceView** têm exceções consideráveis para convenções de nomenclatura. A ID**DataSource** pode ser definida como um único ponto (.), que não é exclusivo, como referência ao banco de dados atual. Uma segunda exceção é **DataSourceView**, que cumpre as convenções de nomenclatura definidas por objetos **DataSet** no .NET Framework, onde o **Name** é usado como o identificador.  
  
 As regras a seguir se aplicam às propriedades **Name** e **ID** .  
  
-   Os nomes não diferenciam maiúsculas de minúsculas. Não é possível ter um cubo chamado "vendas" e outro chamado "Vendas" no mesmo banco de dados.  
  
-   Não são permitidos espaços à esquerda ou à direita em um nome de objeto, embora você possa inserir espaços em um nome. Os espaços de abertura e fechamento são eliminados implicitamente. Isso se aplica a **Name** e **ID** de um objeto.  
  
-   O número máximo de caracteres é 100.  
  
-   Não há nenhum requisito especial para o primeiro caractere de um identificador. O primeiro caractere pode ser qualquer caractere válido.  
  
##  <a name="bkmk_reserved"></a>Caracteres e palavras reservadas  
 As palavras reservadas estão em inglês e se aplicam a nomes de objetos, e não a legendas. Se você usar inadvertidamente uma palavra reservada em um nome de objeto, ocorrerá um erro de validação. Nos modelos multidimensionais e de mineração de dados, as palavras reservadas descritas a seguir não podem ser usadas em qualquer objeto, a qualquer momento.  
  
 Em modelos de tabela, em que a compatibilidade do banco de dados é definida como 1103, as regras de validação foram atenuadas para certos objetos, fora de conformidade para os requisitos de caracteres estendidos e convenções de nomenclatura de determinados aplicativos cliente. Os bancos de dados que atendem a esses critérios estão sujeitos a regras de validação menos rigorosas. Nesse caso, é possível que um nome de objeto inclua um caractere restrito e ainda passe na validação.  
  
 **Palavras reservadas**  
  
-   AUX  
  
-   CLOCK$  
  
-   COM1 a COM9 (COM1, COM2, COM3 e assim por diante)  
  
-   CON  
  
-   LPT1 a LPT9 (LPT1, LPT2, LPT3 e assim por diante)  
  
-   NUL  
  
-   PRN  
  
-   NULL não é permitido como um caractere em qualquer cadeia de caracteres dentro do XML  
  
 **Caracteres reservados**  
  
 A tabela a seguir lista caracteres inválidos para objetos específicos.  
  
|Objeto|Caracteres inválidos|  
|------------|------------------------|  
|**Servidor**|Ao nomear um objeto de servidor, siga as convenções de nomenclatura de servidor do Windows. Para obter detalhes, consulte [Convenções de nomenclatura (Windows)](http://msdn.microsoft.com/library/windows/desktop/ms682856\(v=vs.85\).aspx) .|  
|**DataSource**|: / \ * &#124; ? " () [] {} <>|  
|**Level** ou **Attribute**|. , ; ' ` : / \ * &#124; ? " & % $ ! + = [] {} < >|  
|**Dimension** ou **Hierarchy**|. , ; ' ` : / \ * &#124; ? " & % $ ! + = () [] {} \<,>|  
|Todos os outros objetos|. , ; ' ` : / \ * &#124; ? " & % $ ! + = () [] {} < >|  
  
 **Exceções: Quando caracteres reservados são permitidos**  
  
 Conforme observado, os bancos de dados de uma modalidade e de um nível de compatibilidade específicos podem ter nomes de objetos que incluam caracteres reservados. Os nomes de objeto de atributo de dimensão, hierarquia, nível, medida e KPI podem incluir caracteres reservados, para bancos de dados de tabelas (1103 ou superior) que permitem o uso de caracteres estendidos:  
  
|Modo de servidor e nível de compatibilidade de banco de dados|Caracteres reservados permitidos?|  
|--------------------------------------------------|----------------------------------|  
|MOLAP (todas as versões)|Não|  
|Tabela - 1050|Não|  
|Tabela - 1100|Não|  
|Tabela – 1130 e superior|Sim|  
  
 Bancos de dados podem ter um ModelType padrão. O padrão é equivalente a multidimensional e, portanto, não dá suporte ao uso de caracteres reservados em nomes de colunas.  
  
## <a name="see-also"></a>Consulte também  
 [Palavras reservadas para MDX](../../../mdx/mdx-reserved-words.md)   
 [Suporte a tradução no Analysis Services](../../../analysis-services/translation-support-in-analysis-services.md)   
 [XML for Analysis conformidade &#40; XMLA &#41;](../../../analysis-services/xmla/xml-for-analysis-compliance-xmla.md)  
  
  
