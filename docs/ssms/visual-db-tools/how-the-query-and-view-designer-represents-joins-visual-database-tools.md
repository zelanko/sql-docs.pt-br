---
title: Como o Designer de Consulta e Exibição representa junções | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL pane [Visual Database Tools]
- joins [SQL Server], Query and View Designer
- Diagram pane [Visual Database Tools]
ms.assetid: 20a99dcb-83bd-4aa6-9139-92e2e5ba4887
author: markingmyname
ms.author: maghan
manager: jroth
ms.openlocfilehash: 833dfd2b9f6fc9cefb785db70369969004e52e13
ms.sourcegitcommit: 5d839dc63a5abb65508dc498d0a95027d530afb6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67682305"
---
# <a name="how-the-query-and-view-designer-represents-joins-visual-database-tools"></a>Como o Designer de Consulta e Exibição representa junções (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Se as tabelas forem unidas, o [Designer de Consulta e Exibição](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md) representará a junção graficamente no [painel Diagrama](../../ssms/visual-db-tools/diagram-pane-visual-database-tools.md) e pelo uso da sintaxe SQL no [painel SQL](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md).  
  
## <a name="diagram-pane"></a>painel Diagrama  
No painel Diagrama, o Designer de Consulta e Exibição exibe uma linha de junção entre as colunas de dados envolvidas na junção. O Designer de Consulta e Exibição exibe uma linha de junção para cada condição de junção. Por exemplo, a ilustração seguinte mostra uma linha de junção entre duas tabelas unidas:  
  
![A linha de junção mostra a relação entre duas tabelas](../../ssms/visual-db-tools/media/dv3wbig.gif "A linha de junção mostra a relação entre duas tabelas")  
  
Se as tabelas forem unidas usando mais de um critério de junção, o Designer de Consulta e Exibição exibirá várias linhas de junção, como no exemplo seguinte:  
  
![Tabelas unidas usando mais de uma condição de junção](../../ssms/visual-db-tools/media/dv3w9n1.gif "Tabelas unidas usando mais de uma condição de junção")  
  
Se as colunas de dados unidas não forem exibidas (por exemplo, o retângulo que representa a tabela ou o objeto estruturado por tabela é minimizado ou a junção envolve uma expressão), o Designer de Consulta e Exibição colocará a linha de junção na barra de títulos do retângulo que representa a tabela ou objeto estruturado por tabela.  
  
A forma do ícone no meio da linha de junção indica como são unidas as tabelas ou objetos com estrutura de tabela. Se a cláusula de junção usar um operador diferente de igual (=), o operador aparecerá no ícone de linha de junção. A tabela a seguir lista os ícones que aparecem na linha de junção.  
  
|**Ícone de linha de junção**|**Descrição**|  
|----------------------|-------------------|  
|![Ícone das Ferramentas de Banco de Dados Visual](../../ssms/visual-db-tools/media/dv3wbih.gif "Ícone das Ferramentas de Banco de Dados Visual")|Junção interna (criada usando um sinal de igual).|  
|![Ícone das Ferramentas de Banco de Dados Visual](../../ssms/visual-db-tools/media/dv3wbii.gif "Ícone das Ferramentas de Banco de Dados Visual")|Junção interna baseada no operador "maior que".|  
|![Ícone das Ferramentas de Banco de Dados Visual](../../ssms/visual-db-tools/media/dv3wbij.gif "Ícone das Ferramentas de Banco de Dados Visual")|A junção externa em que todas as linhas da tabela representada à esquerda serão incluídas, mesmo se não tiverem correspondências na tabela relacionada.|  
|![Ícone das Ferramentas de Banco de Dados Visual](../../ssms/visual-db-tools/media/dv3wbik.gif "Ícone das Ferramentas de Banco de Dados Visual")|A junção externa em que todas as linhas da tabela representada à direita serão incluídas, mesmo se não tiverem correspondências na tabela relacionada.|  
|![Ícone das Ferramentas de Banco de Dados Visual](../../ssms/visual-db-tools/media/dv3wbil.gif "Ícone das Ferramentas de Banco de Dados Visual")|Junção externa completa na qual serão incluídas todas as linhas de ambas as tabelas, mesmo se elas não tiverem correspondências com a tabela relacionada.|  
  
Os símbolos no final da linha de junção indicam o tipo de junção. A tabela a seguir lista os tipos de junções e os ícones exibidos no final da linha de junção.  
  
|**Ícone nas extremidades da linha de junção**|**Tipo de junção**|  
|---------------------------------|--------------------|  
|![Ícone das Ferramentas de Banco de Dados Visual](../../ssms/visual-db-tools/media/dv3wbim.gif "Ícone das Ferramentas de Banco de Dados Visual")|Junção uma a uma.|  
|![Ícone das Ferramentas de Banco de Dados Visual](../../ssms/visual-db-tools/media/dv3wbin.gif "Ícone das Ferramentas de Banco de Dados Visual")|Junção uma para muitas.|  
|![Ícone das Ferramentas de Banco de Dados Visual](../../ssms/visual-db-tools/media/dv3wbio.gif "Ícone das Ferramentas de Banco de Dados Visual")|O Designer de Consulta e Exibição não pode determinar o tipo de junção. Essa situação ocorre com mas frequência quando você cria uma junção manualmente.|  
  
## <a name="sql-pane"></a>painel SQL  
Uma junção pode ser expressada de vários modos em uma instrução SQL. A sintaxe exata depende do banco de dados que você está usando e de como você definiu a junção.  
  
Opções de sintaxe para unir tabelas incluem:  
  
-   **Qualificador JOIN para a cláusula FROM**.   As palavras-chave INNER e OUTER especificam o tipo de junção. Essa sintaxe é o padrão para ANSI 92 SQL.  
  
    Por exemplo, se você unir as tabelas `publishers` e `pub_info` baseadas na coluna `pub_id` em cada tabela, a instrução SQL resultante poderia se parecer com:  
  
    ```  
    SELECT *  
    FROM publishers INNER JOIN pub_info ON  
       publishers.pub_id = pub_info.pub_id  
    ```  
  
    Se você criar uma junção externa, as palavras LEFT OUTER ou RIGHT OUTER serão exibidas em vez da palavra INNER.  
  
-   **A cláusula WHERE compara as colunas em ambas as tabelas**.   Uma cláusula WHERE será exibida se o banco de dados não oferecer suporte à sintaxe JOIN (ou se você mesmo a tiver inserido). Se a junção for criada na cláusula WHERE , ambos os nomes de tabela aparecerão na cláusula FROM.  
  
    Por exemplo, a instrução a seguir une as tabelas `publishers` e `pub_info` .  
  
    ```  
    SELECT *  
    FROM publishers, pub_info  
    WHERE publishers.pub_id = pub_info.pub_id  
    ```  
  
## <a name="see-also"></a>Consulte Também  
[Consultar com junções &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-with-joins-visual-database-tools.md)  
[Caixa de diálogo Unir &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/join-dialog-box-visual-database-tools.md)  
  
