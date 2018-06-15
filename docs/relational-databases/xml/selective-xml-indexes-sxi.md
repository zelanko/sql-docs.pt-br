---
title: SXI (índices XML seletivos) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: xml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 598ecdcd-084b-4032-81b2-eed6ae9f5d44
caps.latest.revision: 9
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 1bc3e5c4f5476fe97a096a2e1a1e4ca9748f709e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33015953"
---
# <a name="selective-xml-indexes-sxi"></a>SXI (índices XML seletivos)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Os índices XML seletivos são outro tipo de índice XML que está disponível para você além de índices XML comuns. Os objetivos do recurso de índice XML seletivo são os seguintes:  
  
-   Melhorar o desempenho das consultas em dados XML armazenados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Dar suporte à indexação mais rápida de grandes cargas de trabalho de dados XML.  
  
-   Melhorar a escalabilidade e reduzir os custos de armazenamento de índices XML.  
  
 A principal limitação de índices XML comuns é que eles indexam todo o documento XML. Isso apresenta várias desvantagens significativas, como menor desempenho durante as consultas e maior custo de manutenção do índice, relacionados principalmente aos custos de armazenamento do índice.  
  
 O recurso de índice XML seletivo permite promover somente alguns caminhos dos documentos XML a serem indexados. No momento da criação do índice, esses caminhos são avaliados, e os nós para os quais eles apontam são fragmentados e armazenados em uma tabela relacional no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esse recurso usa um algoritmo de mapeamento eficiente desenvolvido pela [!INCLUDE[msCoName](../../includes/msconame-md.md)] Research em colaboração com a equipe do produto [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Esse algoritmo mapeia os nós XML para uma única tabela relacional, com desempenho exZip Codecional, exigindo espaço de armazenamento modesto.  
  
 O recurso de índice XML seletivo também dá suporte a índices XML seletivos secundários em nós que foram indexados por um índice XML seletivo. Esses índices seletivos secundários são mais eficientes e melhoram o desempenho das consultas.  
  
##  <a name="benefits"></a> Benefícios de índices XML seletivos  
 Os índices XML seletivos apresentam os seguintes benefícios:  
  
1.  Desempenho significativamente melhor em consultas no tipo de dados XML para cargas típicas de consulta.  
  
2.  Requisitos de armazenamento reduzidos em relação aos índices XML comuns.  
  
3.  Custos de manutenção de índice reduzidos em relação aos índices XML comuns.  
  
4.  Não há necessidade de atualizar aplicativos para se beneficiar dos índices XML seletivos.  
  
  
##  <a name="compare"></a> Índices XML seletivos e índices XML primários  
  
> [!IMPORTANT]  
>  Na maioria das vezes, crie um índice XML seletivo, em vez de um índice XML comum, para obter melhor desempenho e um armazenamento mais eficiente.  
  
 Entretanto, um índice XML seletivo não é recomendado quando uma das seguintes condições é verdadeira:  
  
-   Você mapeia um grande número de caminhos de nós.  
  
-   Você dá suporte a consultas de elementos desconhecidos ou de elementos em um local desconhecido na estrutura do documento.  
  
  
##  <a name="example"></a> Exemplo simples de índice XML seletivo  
 Considere o fragmento XML a seguir como um documento XML em uma tabela de aproximadamente 500.000 linhas:  
  
```xml  
<book>  
    <created>2004-03-01</created>   
    <authors>Various</authors>  
    <subjects>  
        <subject>English wit and humor -- Periodicals</subject>  
        <subject>AP</subject>   
    </subjects>  
    <title>Punch, or the London Charivari, Volume 156, April 2, 1919</title>  
    <id>etext11617</id>  
</book>  
```  
  
 A criação de índice XML primário em muitas linhas desse esquema simples demora muito. A consulta desses dados também é prejudicada porque um índice XML primário não dá suporte à indexação seletiva.  
  
 Se você precisa consultar somente esses dados no caminho `/book/title` e no caminho `/book/subjects` , poderá criar o seguinte índice XML seletivo:  
  
```sql  
CREATE SELECTIVE XML INDEX SXI_index  
ON Tbl(xmlcol)  
FOR   
(  
    pathTitle = '/book/title/text()' AS XQUERY 'xs:string',   
    pathAuthors = '/book/authors' AS XQUERY 'node()',  
    pathId = '/book/id' AS SQL NVARCHAR(100)  
)  
```  
  
 A instrução anterior é um bom exemplo da sintaxe CREATE que você usa ao criar um índice XML seletivo. Na instrução CREATE, primeiro você fornece um nome para o índice e identifica a tabela e a coluna XML para indexação. Em seguida, você fornece os caminhos a serem indexados. Um caminho tem três partes:  
  
1.  Um nome que identifica exclusivamente o caminho.  
  
2.  Uma expressão XQuery que descreve o caminho.  
  
3.  Dicas de otimização opcionais.  
  
 Para obter mais informações sobre esses elementos, consulte [Tarefas relacionadas](#reltasks).  
  
  
## <a name="supported-features-prerequisites-and-limitations"></a>Recursos com suporte, pré-requisitos e limitações  
  
###  <a name="features"></a> Recursos XML com suporte  
 Os índices XML seletivos dão suporte à XQuery com suporte no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nos métodos exist(), value() e nodes().  
  
-   Para os métodos exist(), value() e nodes(), os índices XML seletivos contêm informações suficientes para transformar a expressão inteira.  
  
-   Para os métodos query() e modify(), os índices XML seletivos podem ser usados somente para filtragem de nós.  
  
-   Para o método query(), os índices XML seletivos não são usados para recuperar resultados.  
  
-   Para o método modify(), os índices XML seletivos não são usados para atualizar documentos XML.  
  
  
###  <a name="unsupported"></a> Recursos XML sem suporte  
 Os índices XML seletivos não dão suporte aos recursos a seguir que têm suporte na implementação de XML do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :  
  
-   Indexação de nós com tipos XS complexos: tipos de união, tipos de sequência e tipos de lista.  
  
-   Indexação de nós com tipos XS binários: por exemplo, base64Binary e hexBinary.  
  
-   Especificação dos nós a serem indexados com expressões XPath que contêm o caractere curinga `*` ao final: por exemplo,  `/a/b/c/*`, `/a//b/*`ou `/a/b/*:c`.  
  
-   Indexação de qualquer eixo que não seja o filho, o atributo ou o descendente. A ocorrência `//<step>` é permitida como um caso especial.  
  
-   Indexação de instruções e comentários de processamento XML.  
  
-   Especificação e recuperação do identificador de um nó usando a função id().  
  
  
###  <a name="prereq"></a> Pré-requisitos  
 Os pré-requisitos a seguir devem existir para que se possa criar um índice XML seletivo em uma coluna XML em uma tabela de usuário:  
  
-   Um índice clusterizado deve existir na chave primária da tabela do usuário.  
  
-   A chave primária da tabela de usuário é limitada a um tamanho de 128 bytes quando usada com índices XML seletivos.  
  
-   A chave de clustering da tabela de usuário é limitada a 15 colunas quando usada com índices XML seletivos.  
  
  
###  <a name="limits"></a> Limitações  
 **Requisitos e limitações gerais**  
  
-   Cada índice XML seletivo só pode ser criado em uma única coluna XML.  
  
-   Não é possível criar um índice XML seletivo em uma coluna que não seja XML.  
  
-   Cada coluna XML em uma tabela só pode ter um índice XML seletivo.  
  
-   Cada tabela pode ter até 249 índices XML seletivos.  
  
 **Limitações em objetos com suporte**  
  
 Não é possível criar índices XML seletivos nos seguintes objetos:  
  
1.  Colunas XML em uma exibição.  
  
2.  Variável com valor de tabela com colunas XML.  
  
3.  Variáveis do tipo XML.  
  
4.  Colunas XML computadas.  
  
5.  Colunas XML com uma profundidade de mais de 128 nós aninhados.  
  
 **Limitações relacionadas ao armazenamento**  
  
 Há um limite finito no número de nós do documento XML que pode ser adicionado ao índice. Um índice XML seletivo mapeia documentos XML para uma única tabela relacional. Portanto, ele não pode ter mais de 1.024 colunas não nulas em nenhuma linha especificada da tabela. Além de isso, muitas das limitações de colunas esparsas também se aplicam a índices XML seletivos, porque os índices usam colunas esparsas para armazenamento.  
  
 O número máximo de colunas não nulas com suporte em qualquer linha especificada depende do tamanho dos dados nas colunas:  
  
-   Na melhor das hipóteses, 1024 colunas não nulas têm suporte quando todas as colunas são do tipo **bit**.  
  
-   Na pior das hipóteses, somente 236 colunas não nulas têm suporte quando todas as colunas são grandes objetos do tipo **varchar**.  
  
 Os índices XML seletivos usam de uma a quatro colunas internamente para cada caminho de nó que é indexado. O número total de nós que pode ser indexado varia de 60 a várias centenas de nós, dependendo do tamanho real dos dados nos caminhos indexados.  
  
-   Na pior das hipóteses, quando alguns ou todos os nós são mapeados usando `//` na definição do caminho de nó, o número máximo de nós indexados é 60.  
  
-   Na melhor das hipóteses, quando os nós são mapeados sem usar `//` na definição do caminho de nó, o número máximo de nós indexados é 200.  
  
 **Os índices XML seletivos são recriados quando você usa a instrução CREATE ou ALTER no índice.**  
  
 Quando você usa a instrução CREATE ou ALTER em um índice XML seletivo, ele será recriado offline em um modo de thread único. Frequentemente, as instruções ALTER afetam negativamente o desempenho das consultas em documentos XML indexados.  
  
 **Outras limitações**  
  
-   Não há suporte para índices XML seletivos em dicas de consulta.  
  
-   Não há suporte para índices XML seletivos e índices XML seletivos secundários no Orientador de Otimização de Banco de Dados.  
  
  
##  <a name="reltasks"></a> Tarefas relacionadas  
  
|||  
|-|-|  
|**Tarefa**|**Tópico**|  
|Especifique os caminhos de nós que você deseja indexar e dicas de otimização opcionais ao criar ou alterar um índice XML seletivo.|[Especificar caminhos e dicas de otimização para índices XML seletivos](../../relational-databases/xml/specify-paths-and-optimization-hints-for-selective-xml-indexes.md)|  
|Crie, altere ou remova um índice XML seletivo.|[Criar, alterar e remover índices XML seletivos](../../relational-databases/xml/create-alter-and-drop-selective-xml-indexes.md)|  
|Crie, altere ou remova um índice XML seletivo secundário.|[Criar, alterar e remover índices XML seletivos secundários](../../relational-databases/xml/create-alter-and-drop-secondary-selective-xml-indexes.md)|  
  
  
  
