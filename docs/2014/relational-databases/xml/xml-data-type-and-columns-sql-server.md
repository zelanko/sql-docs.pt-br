---
title: Colunas e tipos de dados XML (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
ms.assetid: 00db8f21-7d4b-4347-ae43-3a7c314d2fa1
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: f26049671f6276b125e06355d7fa15bb5b3febea
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48205276"
---
# <a name="xml-data-type-and-columns-sql-server"></a>Tipos e colunas de dados XML (SQL Server)
  Este tópico discute as vantagens e as limitações do `xml` tipo de dados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]e ajuda você a escolher como armazenar dados XML.  
  
## <a name="relational-or-xml-data-model"></a>Modelo de dados relacional ou XML  
 Se os dados estiverem altamente estruturados com esquema conhecido, o modelo relacional provavelmente funcionará melhor para armazenamento de dados. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece a funcionalidade exigida e ferramentas que podem ser necessárias. Por outro lado, se a estrutura estiver semiestruturada, desestruturada ou desconhecida, será necessário considerar a modelagem desses dados.  
  
 O XML é uma boa opção se você desejar um modelo independente de plataforma para garantir a portabilidade dos dados usando marcação estrutural e semântica. Além disso, ele será uma opção apropriada se algumas das seguintes propriedades forem atendidas:  
  
-   Os dados são esparsos ou você não conhece a estrutura dos dados ou a estrutura dos dados pode ser alterada significativamente no futuro.  
  
-   Seus dados representam hierarquia de confinamento, em vez de referências entre entidades, e podem ser recursivos.  
  
-   A ordem é inerente em seus dados.  
  
-   Você deseja consultar os dados ou atualizar partes dos dados com base em sua estrutura.  
  
 Se nenhuma dessas condições for atendida, você deverá usar o modelo de dados relacional. Por exemplo, se os dados estiverem em formato XML, seu aplicativo usar apenas o banco de dados para armazenar e recuperar os dados, mas um `[n]varchar(max)` coluna é tudo o que você precisa. O armazenamento de dados em uma coluna XML traz benefícios adicionais. Isso inclui fazer com que o mecanismo determine se os dados estão bem formados ou válidos e, também, inclui suporte para atualizações e consultas refinadas nos dados XML.  
  
## <a name="reasons-for-storing-xml-data-in-sql-server"></a>Razões para o armazenamento de dados XML no SQL Server  
 A seguir estão algumas das razões para usar recursos do XML nativo no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em vez do gerenciamento de dados XML no sistema de arquivos:  
  
-   Você deseja compartilhar, consultar e modificar dados XML de uma maneira eficiente e transacionada. O acesso a dados refinados é importante para seu aplicativo. Por exemplo, você pode desejar extrair algumas das seções dentro de um documento XML ou inserir uma nova seção sem substituir todo o documento.  
  
-   Você tem dados relacionais e dados XML e deseja ter interoperabilidade entre os dados relacionais e XML dentro de seu aplicativo.  
  
-   Você precisa de suporte a idioma para consulta e modificação de dados para aplicativos entre domínios.  
  
-   Você deseja que o servidor garanta que os dados estejam bem formados além de, opcionalmente, validar os dados de acordo com esquemas XML.  
  
-   Você deseja indexação de dados XML para processamento eficiente de consultas e boa escalabilidade e o uso de um otimizador de consulta de primeira classe.  
  
-   Você deseja acesso de OLE DB, SOAP e ADO.NET a dados XML.  
  
-   Você deseja usar a funcionalidade administrativa do servidor de banco de dados para gerenciar dados XML. Por exemplo, backup, recuperação e replicação.  
  
 Se nenhuma dessas condições for atendida, talvez seja melhor armazenar os dados como não XML, tipo de objeto grande, como `[n]varchar(max)` ou `varbinary(max)`.  
  
## <a name="xml-storage-options"></a>Opções de armazenamento XML  
 As opções de armazenamento de XML no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] incluem o seguinte:  
  
-   Armazenamento nativo como tipo de dados `xml`  
  
     Os dados são armazenados em uma representação interna que preserva o conteúdo XML dos dados. Essa representação interna inclui informações sobre a hierarquia de confinamento, a ordem dos documentos e os valores do elemento e do atributo. Especificamente, o conteúdo de InfoSet dos dados XML é preservado. Para obter mais informações sobre InfoSet, visite [http://www.w3.org/TR/xml-infoset](http://go.microsoft.com/fwlink/?LinkId=48843). O conteúdo de InfoSet não pode ser uma cópia idêntica do XML de texto porque as seguintes informações não são mantidas: espaços em branco insuficientes, ordem dos atributos, prefixos de namespace e declaração XML.  
  
     Para tipo `xml` tipo de dados, um `xml` tipo de dados associado a esquemas XML, a-schema validation InfoSet (PSVI) adiciona informações de tipo ao InfoSet e é codificado na representação interna. Isto melhora a velocidade da análise significativamente. Para obter mais informações, consulte as especificações de Esquema XML do W3C em [http://www.w3.org/TR/xmlschema-1](http://go.microsoft.com/fwlink/?LinkId=48881) e [http://www.w3.org/TR/xmlschema-2](http://go.microsoft.com/fwlink/?LinkId=4871).  
  
-   Mapeando entre XML e armazenamento relacional  
  
     Usando um AXSD (annotated schema), o XML é decomposto em colunas em uma ou mais tabelas. Isso preserva a fidelidade dos dados no nível relacional. Como resultado, a estrutura hierárquica é preservada, embora a ordem entre os elementos seja ignorada. O esquema não pode ser recursivo.  
  
-   Armazenamento de objeto grande, `[n]varchar(max)` e `varbinary(max)`  
  
     Uma cópia idêntica dos dados é armazenada. Isso é útil para aplicativos com finalidades especiais, como documentos legais. A maioria dos aplicativos não exige uma cópia exata e ficam satisfeitos com o conteúdo XML (fidelidade de InfoSet).  
  
 Geralmente, você pode precisar usar uma combinação dessas abordagens. Por exemplo, você pode desejar armazenar dados XML em um `xml` coluna de tipo de dados e promover propriedades dela em colunas relacionais. Ou, você talvez queira usar tecnologia de mapeamento para armazenar partes não recursivas em colunas não XML e apenas as partes recursivas em `xml` colunas de tipo de dados.  
  
### <a name="choice-of-xml-technology"></a>Opção de tecnologia XML  
 A opção de tecnologia XML, XML nativo versus exibição de XML, geralmente depende dos seguintes fatores:  
  
-   Opções de armazenamento  
  
     Os dados XML podem ser mais apropriados para armazenamento de objetos grandes (por exemplo, um manual do produto) ou mais compatível para armazenamento em colunas relacionais (por exemplo, um item de linha convertido em XML). Cada opção de armazenamento preserva a fidelidade do documento a uma extensão diferente.  
  
-   Capacidades de consulta  
  
     Uma opção de armazenamento pode ser mais apropriada do que outra com base na natureza de suas consultas e na extensão na qual os dados XML são consultados. Nas duas opções de armazenamento, há suporte em vários níveis para consulta refinada de seus dados XML, por exemplo, para avaliação de predicado em nós XML.  
  
-   Indexando dados XML  
  
     Talvez você deseje indexar os dados XML para acelerar o desempenho de consultas XML. As opções de indexação variam de acordo com as opções de armazenamento. É necessário fazer a escolha apropriada para otimizar sua carga de trabalho.  
  
-   Capacidades de modificação de dados  
  
     Algumas cargas de trabalho envolvem modificação refinada de dados XML. Por exemplo, isso pode incluir a adição de uma nova seção dentro de um documento, enquanto outras cargas de trabalho, como conteúdo da Web, não incluem. O suporte à linguagem de modificação de dados pode ser importante para seu aplicativo.  
  
-   Suporte de esquema  
  
     Os dados XML podem ser descritos por um esquema que pode ou não ser um documento de esquema XML. O suporte para XML associado a esquema depende da tecnologia XML.  
  
 Opções diferentes também têm características diferentes de desempenho.  
  
### <a name="native-xml-storage"></a>Armazenamento XML nativo  
 Você pode armazenar dados XML em um `xml` coluna de tipo de dados no servidor. Essa escolha será apropriada se as seguintes condições forem aplicadas:  
  
-   Você deseja uma maneira direta de armazenar dados XML no servidor e, ao mesmo tempo, preservar a ordem e a estrutura do documento.  
  
-   Você pode ou não ter um esquema para seus dados XML.  
  
-   Você deseja consultar e modificar os dados XML.  
  
-   Você deseja indexar os dados XML para acelerar o processamento de consultas.  
  
-   Seu aplicativo precisa de exibições do catálogo do sistema para administrar seus dados e esquemas XML.  
  
 O armazenamento XML nativo é útil quando você tem documentos XML que têm um intervalo de estruturas ou documentos XML que estão de acordo com esquemas diferentes ou complexos muito difíceis de mapear para estruturas relacionais.  
  
#### <a name="example-modeling-xml-data-using-the-xml-data-type"></a>Exemplo: Modelando dados XML com o tipo de dados xml  
 Considere o manual de um produto em formato XML composto por um capítulo separado para cada tópico e com várias seções dentro de cada capítulo. Uma seção pode conter subseções. Como resultado, \<section> é um elemento recursivo. Os manuais de produtos contêm uma grande quantidade de conteúdo misto, diagramas e material técnico. Os dados são semiestruturados. Os usuários podem desejar executar uma pesquisa contextual para obter tópicos de interesse, como pesquisar a seção sobre "índice clusterizado" dentro do capítulo sobre "indexação" e consultar as quantidades técnicas.  
  
 Um modelo de armazenamento apropriado para seus documentos XML é uma coluna de tipo de dados `xml`. Isso preserva o conteúdo de InfoSet de seus dados XML. A indexação de colunas XML beneficia o desempenho de consultas.  
  
#### <a name="example-retaining-exact-copies-of-xml-data"></a>Exemplo: Mantendo cópias exatas de dados XML  
 Para ilustrar, assuma que os regulamentos governamentais exigem que você mantenha cópias textuais exatas de seus documentos XML. Por exemplo, isso pode incluir documentos assinados, documentos legais ou pedidos de transação de estoque. Você pode desejar armazenar seus documentos em um `[n]varchar(max)` coluna.  
  
 Para consultar, converta os dados em tipo de dados `xml` em tempo de execução e execute Xquery sobre eles. A conversão em tempo de execução pode ser dispendiosa, principalmente quando o documento é grande. Se a consulta for feita com frequência, você poderá armazenar os documentos de maneira redundante em uma coluna de tipo de dados `xml` e indexá-los enquanto retorna cópias exatas dos documentos da coluna `[n]varchar(max)`.  
  
 A coluna XML pode ser uma coluna computada, com base no `[n]varchar(max)` coluna. No entanto, você não pode criar um índice XML em uma coluna XML computada nem um índice XML pode ser criado no `[n]varchar(max)` ou `varbinary(max)` colunas.  
  
### <a name="xml-view-technology"></a>Tecnologia de exibição XML  
 Ao definir um mapeamento entre seus esquemas XML e as tabelas em um banco de dados, você cria uma "exibição XML" dos dados persistentes. O carregamento de XML em massa pode ser usado para popular as tabelas subjacentes usando a exibição XML. É possível consultar a exibição XML usando XPath versão 1.0. A consulta é convertida em consultas SQL nas tabelas. De maneira semelhante, as atualizações também são propagadas para essas tabelas.  
  
 Essa tecnologia é útil nas seguintes situações:  
  
-   Você deseja ter um modelo de programação centrado em XML usando exibições XML sobre seus dados relacionais existentes.  
  
-   Você tem um esquema (XSD, XDR) para seus dados XML que um parceiro externo pode ter fornecido.  
  
-   A ordem não é importante nos dados, os dados da tabela de consulta não são recursivos ou a profundidade máxima da recursão é conhecida antecipadamente.  
  
-   Você deseja consultar e modificar os dados pela exibição XML usando XPath versão 1.0.  
  
-   Você deseja carregar dados XML em massa e decompô-los nas tabelas subjacentes usando a exibição XML.  
  
 Os exemplos incluem dados relacionais expostos como XML para troca de dados e serviços da Web e dados XML com esquema fixo. Para obter mais informações, consulte [MSDN Online Library](http://go.microsoft.com/fwlink/?linkid=31174).  
  
#### <a name="example-modeling-data-using-an-annotated-xml-schema-axsd"></a>Exemplo: Modelando dados usando um AXSD (Annotated XML Schema)  
 Para ilustrar, assuma que você tem dados relacionais existentes, como clientes, pedidos e itens de linha que deseja tratar como XML. Defina uma exibição XML usando AXSD sobre dados relacionais. A exibição XML permite carregar dados XML em massa em suas tabelas e consultar e atualizar os dados relacionais usando a exibição XML. Esse modelo é útil se você precisar trocar dados que contêm marcação XML com outros aplicativos enquanto seus aplicativos SQL funcionam sem interrupção.  
  
### <a name="hybrid-model"></a>Modelo híbrido  
 Frequentemente, uma combinação de relacional e `xml` colunas de tipo de dados é apropriada para modelagem de dados. Alguns dos valores de seus dados XML podem ser armazenados em colunas relacionais e o restante, ou todo o valor XML, armazenado em uma coluna XML. Isso pode resultar em um melhor desempenho no qual você terá mais controle sobre os índices criados nas colunas relacionais e características de bloqueio.  
  
 Os valores a serem armazenados em colunas relacionais dependem de sua carga de trabalho. Por exemplo, você pode conseguir um desempenho mais rápido da consulta se recuperar todos os valores XML com base na expressão de caminho, /Customer/@CustId, promovendo o valor do atributo **CustId** em uma coluna relacional e indexando-o. Por outro lado, se os dados XML forem decompostos de maneira extensiva e não redundante em colunas relacionais, o custo de remontagem poderá ser significativo.  
  
 Para dados XML altamente estruturados, por exemplo, o conteúdo de uma tabela foi convertido em XML, você pode mapear todos os valores para colunas relacionais e provavelmente usar tecnologia de exibição XML.  
  
## <a name="granularity-of-xml-data"></a>Granularidade de dados XML  
 A granularidade dos dados XML armazenados em uma coluna XML é muito importante para bloqueio e, em um nível menor, também é importante para atualizações. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa o mesmo mecanismo de bloqueio para dados XML e não XML. Portanto, o bloqueio em nível de linha faz com que todas as instâncias XML na linha sejam bloqueadas. Quando a granularidade é grande, o bloqueio de grandes instâncias XML para atualizações faz com que a taxa de transferência decline em um cenário multiusuário. Por outro lado, a decomposição grave perde o encapsulamento de objetos e aumenta o custo de reassembly.  
  
 Um equilíbrio entre requisitos de modelagem de dados e características de atualização e bloqueio é importante para um bom design. No entanto, no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o tamanho de instâncias XML armazenadas reais não é crítico.  
  
 Por exemplo, as atualizações em uma instância XML são executadas usando novo suporte para atualizações de BLOB (objetos binários grandes) parciais e de índices parciais nas quais a instância XML armazenada existente é comparada com sua versão atualizada. A atualização de BLOB (objetos binários grandes) parcial executa uma comparação diferencial entre as duas instâncias XML e atualiza apenas as diferenças. As atualizações parciais de índice modificam apenas as linhas que devem ser alteradas no índice XML.  
  
## <a name="limitations-of-the-xml-data-type"></a>Limitações do tipo de dados xml  
 Observe as seguintes limitações gerais que se aplicam ao tipo de dados `xml`:  
  
-   A representação armazenada de `xml` instâncias do tipo de dados não podem exceder 2 GB.  
  
-   Ele não pode ser usado como um subtipo de uma instância **sql_variant** .  
  
-   Ele não oferece suporte à conversão de `text` ou `ntext`. Use `varchar(max)` ou `nvarchar(max)` em vez disso.  
  
-   Ele não pode ser comparado ou classificado. Isto significa que um tipo de dados `xml` não pode ser usado em uma instrução GROUP BY.  
  
-   Ele não pode ser usado como um parâmetro para nenhuma função escalar interna além de ISNULL, COALESCE e DATALENGTH.  
  
-   Ele não pode ser usado como uma coluna de chaves em um índice. No entanto ele pode ser incluído como dados em um índice clusterizado ou adicionado explicitamente em um índice não clusterizado usando a palavra-chave INCLUDE quando o índice não clusterizado é criado.  
  
## <a name="see-also"></a>Consulte também  
 [Exemplos de importação e exportação em massa de documentos XML &#40;SQL Server&#41;](../import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)  
  
  
