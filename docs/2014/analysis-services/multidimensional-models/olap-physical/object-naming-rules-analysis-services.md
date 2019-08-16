---
title: Regras de nomenclatura de objeto (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- objects [Analysis Services], naming
ms.assetid: b338a60d-4802-4b68-862a-6dc6a3f75e48
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f45ccaa0caab2e1dcc7e96e80e217d82d4f1f805
ms.sourcegitcommit: 187f6d327421e64f1802a3085f88bbdb0c79b707
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/16/2019
ms.locfileid: "69530886"
---
# <a name="object-naming-rules-analysis-services"></a>Regras de nomenclatura de objeto (Analysis Services)
  Este tópico descreve as convenções de nomenclatura de objeto, bem como as palavras e os caracteres reservados que não podem ser usados em nomes de objetos, códigos ou scripts no [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
##  <a name="bkmk_Names"></a>Convenções de nomenclatura  
 Todo objeto tem as propriedades `Name` e `ID` que devem ser exclusivas no escopo da coleção pai. Por exemplo, duas dimensões podem ter o mesmo nome, desde que cada uma resida em um banco de dados diferente.  
  
 Embora você possa especificar isso manualmente, a `ID` costuma ser gerada automaticamente quando o objeto é criado. Após começar a criar um modelo, nunca altere a `ID`. Todas as referências de objeto em um modelo se baseiam na `ID`. Então, a alteração de uma `ID` pode facilmente resultar na corrupção do modelo.  
  
 Os objetos `DataSource` e `DataSourceView` têm exceções consideráveis para convenções de nomenclatura. A ID `DataSource` pode ser definida como um único ponto (.), que não é exclusivo, como referência ao banco de dados atual. Uma segunda exceção é `DataSourceView`, que cumpre as convenções de nomenclatura definidas por objetos `DataSet` no .NET Framework, onde o `Name` é usado como o identificador.  
  
 As regras a seguir se aplicam às propriedades `Name` e `ID`.  
  
-   Os nomes não diferenciam maiúsculas de minúsculas. Você não pode ter um cubo chamado "Sales" e outro chamado "Sales" no mesmo banco de dados.  
  
-   Não são permitidos espaços à esquerda ou à direita em um nome de objeto, embora você possa inserir espaços em um nome. Os espaços de abertura e fechamento são eliminados implicitamente. Isso se aplica a `Name` e `ID` de um objeto.  
  
-   O número máximo de caracteres é 100.  
  
-   Não há nenhum requisito especial para o primeiro caractere de um identificador. O primeiro caractere pode ser qualquer caractere válido.  
  
##  <a name="bkmk_reserved"></a>Palavras reservadas e caracteres  
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
|`Server`|Ao nomear um objeto de servidor, siga as convenções de nomenclatura de servidor do Windows. Para obter detalhes, consulte [Convenções de nomenclatura (Windows)](/windows/desktop/DNS/naming-conventions) .|  
|`DataSource`| `: / \ * \| ? " () [] {} <>` |  
|`Level` ou `Attribute`|````. , ; ' ` : / \ * & \| ? " & % $ ! + = [] {} < >````|  
|`Dimension` ou `Hierarchy`|````. , ; ' ` : / \ * \| ? " & % $ ! + = () [] {} <,>````|  
|Todos os outros objetos|````. , ; ' ` : / \ * \| ? " & % $ ! + = () [] {} < >````|  
  
 **Exceção Quando caracteres reservados são permitidos**  
  
 Conforme observado, os bancos de dados de uma modalidade e de um nível de compatibilidade específicos podem ter nomes de objetos que incluam caracteres reservados. Os nomes de objeto de atributo de dimensão, hierarquia, nível, medida e KPI podem incluir caracteres reservados, para bancos de dados de tabelas (1103 ou superior) que permitem o uso de caracteres estendidos:  
  
|Modo de servidor e nível de compatibilidade de banco de dados|Caracteres reservados permitidos?|  
|--------------------------------------------------|----------------------------------|  
|MOLAP (todas as versões)|Não|  
|Tabela - 1050|Não|  
|Tabela - 1100|Não|  
|Tabular-1130 e superior|Sim|  
  
 Bancos de dados podem ter um ModelType padrão. O padrão é equivalente a multidimensional e, portanto, não dá suporte ao uso de caracteres reservados em nomes de colunas.  
  
## <a name="see-also"></a>Consulte também  
 [Palavras reservadas MDX](/sql/mdx/mdx-reserved-words)   
 [Traduções &#40;Analysis Services&#41;](/analysis-services/translation-support-in-analysis-services)   
 [XMLA de &#40;conformidade do XML for Analysis&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-for-analysis-compliance-xmla)  
  
  
