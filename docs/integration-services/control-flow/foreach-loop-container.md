---
title: "Cont&#234;iner Loop Foreach | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.foreachloopcontainer.f1"
  - "sql13.dts.designer.foreachloopcontainer.general.f1"
  - "sql13.dts.designer.foreachloopcontainer.collection.f1"
  - "sql13.dts.designer.foreachloopcontainer.mapping.f1"
  - "sql13.dts.designer.schemarestrictions.f1"
  - "sql13.dts.designer.foreachitemcolumns.f1"
  - "sql13.dts.designer.selectsmoenumeration.f1"
helpviewer_keywords: 
  - "repeating control flow"
  - "Foreach Loop containers"
  - "foreach enumerators [Integration Services]"
  - "contêineres [Integration Services], Loop Foreach"
ms.assetid: dd6cc2ba-631f-4adf-89dc-29ef449c6933
caps.latest.revision: 73
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 72
---
# Cont&#234;iner Loop Foreach
  O contêiner Loop Foreach define um fluxo de controle repetitivo em um pacote. A implementação de loop é semelhante à estrutura de loop **Foreach** em linguagens de programação. Em um pacote, o looping é habilitado por um enumerador Foreach.  O contêiner Loop Foreach repete o fluxo de controle para cada membro de um enumerador especificado.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] fornece os seguintes tipos de enumerador:  
  
-   Enumerador Foreach ADO para enumerar linhas em tabelas. Por exemplo, você pode obter as linhas em um conjunto de registros ADO.  
  
     O destino do Conjunto de Registros salva dados na memória em um conjunto de registros armazenado em uma variável de pacote do tipo de dados **Object** . Geralmente você usa um contêiner Loop Foreach com o enumerador ADO Foreach para processar uma linha do conjunto de registros de cada vez. A variável especificada para o enumerador Foreach ADO deve ser de tipo de dados Object. Para obter mais informações sobre o destino Recordeset, consulte [Use a Recordset Destination](../../integration-services/data-flow/use-a-recordset-destination.md).  
  
-   O Enumerador de Conjunto de Linhas de Esquema ADO.NET Foreach enumera informações de esquema sobre uma fonte de dados. Por exemplo, você pode enumerar e obter uma lista das tabelas do banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Enumerador de Arquivo Foreach para enumerar arquivos em uma pasta. O enumerador pode desviar subpastas. Por exemplo, você pode ler todos os arquivos que têm extensão de nome de arquivo * .log na pasta e respectivas subpastas do Windows.  
  
-   Enumerador Foreach de Variável para enumerar o objeto enumerável que uma variável especificada contém. O objeto enumerável pode ser uma matriz, um **DataTable** ADO.NET, um enumerador do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], e assim por diante. Por exemplo, você pode enumerar os valores de uma matriz que contém o nome de servidores.  
  
-   Enumerador de Item Foreach para enumerar itens que são coleções. Por exemplo, você pode enumerar os nomes de executáveis e diretórios em funcionamento utilizados por uma tarefa Executar Processo.  
  
-   Enumerador Nodelist Foreach para enumerar o conjunto de resultados de uma expressão Xpath (XML Path Language). Por exemplo, essa expressão enumera e obtém uma lista de todos os autores do período clássico: `/authors/author[@period='classical']`.  
  
-   Enumerador SMO Foreach para enumerar objetos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Objects (SMO). Por exemplo, você pode enumerar e obter uma lista das exibições em um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Enumerador de Arquivos Foreach HDFS para enumerar arquivos HDFS no local de HDFS especificado.  
  
-   Enumerador de Blob do Azure Foreach para enumerar blobs em um contêiner de blob no Armazenamento do Azure.  
  
 O diagrama a seguir mostra um contêiner Loop Foreach que tem uma tarefa Sistema de Arquivos. O loop Foreach usa o enumerador de Arquivo Foreach e a tarefa Sistema de Arquivos é configurada para copiar um arquivo. Se a pasta que o enumerador especifica contiver quatro arquivos, o loop repetirá quatro vezes e copiará quatro arquivos.  
  
 ![Um contêiner Loop Foreach que enumera uma pasta](../../integration-services/control-flow/media/ssis-foreachloop.gif "Um contêiner Loop Foreach que enumera uma pasta")  
  
 Você pode usar uma combinação de variáveis e expressões de propriedade para atualizar a propriedade do objeto de pacote com o valor de coleção do enumerador. Primeiro você mapeia o valor de coleção para uma variável definida pelo usuário e, depois, implementa uma expressão na propriedade que usa a variável. Por exemplo, o valor de coleção do enumerador de Arquivo Foreach é mapeado para uma variável denominada **MyFile** e, depois, a variável é usada na expressão para a propriedade Subject de uma tarefa Enviar Email. Quando o pacote é executado, a propriedade Subject é atualizada com o nome de um arquivo cada vez que o loop é repetido. Para obter mais informações, consulte [Usar expressões de propriedade em pacotes](../../integration-services/expressions/use-property-expressions-in-packages.md).  
  
 Variáveis mapeadas para o valor de coleção do enumerador também podem ser usadas em expressões e scripts.  
  
 Um contêiner Loop Foreach pode incluir várias tarefas e contêineres , mas só pode usar um tipo de enumerador. Se o contêiner Loop Foreach incluir várias tarefas, você poderá mapear o valor de coleção do enumerador para várias propriedades de cada tarefa.  
  
 Você pode definir um atributo de transação no contêiner Loop Foreach para definir uma transação para um subconjunto do fluxo de controle de pacotes. Deste modo, é possível gerenciar as transações em nível de Loop Foreach em vez de pacote. Por exemplo, se um contêiner Loop Foreach repetir um fluxo de controle que atualiza dimensões e tabelas de fato em um esquema de estrela, você poderá configurar uma transação para assegurar que todas as tabelas de fato sejam atualizadas com êxito, ou que nenhuma seja atualizada. Para obter mais informações, consulte [Transações do Integration Services](../../integration-services/integration-services-transactions.md).  
  
## Tipos de enumerador  
 Enumeradores são configuráveis, e você deve fornecer informações diferentes, dependendo do enumerador.  
  
 A tabela a seguir resume as informações que cada tipo de enumerador requer.  
  
|Enumerador|Requisitos de configuração|  
|----------------|--------------------------------|  
|ADO Foreach|Especifique a variável de origem de objeto ADO e o modo do enumerador. A variável deve ser do tipo de dados Object.|  
|Conjunto de Linhas de Esquema ADO.NET Foreach|Especifique a conexão com um banco de dados e o esquema a ser enumerado.|  
|Arquivo Foreach|Especifique uma pasta e os arquivos a serem enumerados, o formato do nome de arquivo dos arquivos recuperados, e se as subpastas devem ser desviadas.|  
|Foreach de Variável|Especifique a variável que contém os objetos a serem enumerados.|  
|Item Foreach|Defina os itens na coleção Itens Foreach, inclusive colunas e tipos de dados de coluna.|  
|Nodelist Foreach|Especifique a origem do documento XML e configure a operação XPath.|  
|SMO Foreach|Especifique a conexão com um banco de dados e os objetos SMO a serem enumerados.|  
|Enumerador de Arquivos Foreach HDFS|Especifique uma pasta e os arquivos a serem enumerados, o formato do nome de arquivo dos arquivos recuperados, e se as subpastas devem ser desviadas.|  
|Blob do Azure Foreach|Especifica o contêiner de Blob do Azure em que os blobs de contêineres serão enumerados.|  
  
## Expressões de propriedade em contêineres Loop Foreach  
 É possível configurar pacotes para executar simultaneamente vários executáveis. Essa configuração deve ser usada com cautela quando o pacote incluir um contêiner Loop Foreach que implementa expressões de propriedade.  
  
 Geralmente é útil implementar uma expressão de propriedade para definir o valor da propriedade ConnectionString dos gerenciadores de conexões que os enumeradores Loop Foreach usam. A expressão de propriedade de ConnectionString é definida por uma variável que mapeia para o valor de coleção do enumerador e é atualizada a cada iteração do loop.  
  
 Para evitar consequências negativas do controle não determinante da execução paralela de tarefas no loop, o pacote deve ser configurado para executar só um executável de cada vez. Por exemplo, se um pacote puder executar várias tarefas simultaneamente; um contêiner Loop Foreach que enumera arquivos na pasta, recupera os nomes de arquivo e, depois, usa uma tarefa Executar SQL para inserir os nomes de arquivo em uma tabela podem gerar conflitos de gravação quando duas instâncias da tarefa Executar SQL tentarem gravar ao mesmo tempo. Para obter mais informações, consulte [Usar expressões de propriedade em pacotes](../../integration-services/expressions/use-property-expressions-in-packages.md).  
  
## Tarefas relacionadas  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter detalhes sobre como definir essas propriedades no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique em um dos tópicos a seguir:  
  
-   [Configurar um contêiner Loop Foreach](../Topic/Configure%20a%20Foreach%20Loop%20Container.md)  
  
-   [Definir as propriedades de uma tarefa ou contêiner](../Topic/Set%20the%20Properties%20of%20a%20Task%20or%20Container.md)  
  
 Para obter detalhes sobre como definir essas propriedades programaticamente, clique no tópico a seguir:  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.ForEachLoop>  
  
## Conteúdo relacionado  
 Entrada de blog, [SSIS For Each Node List Enumerator](http://go.microsoft.com/fwlink/?LinkId=220671), em bidn.com.  
  
## Consulte também  
 [Fluxo de Controle](../../integration-services/control-flow/control-flow.md)   
 [Contêineres do Integration Services](../../integration-services/control-flow/integration-services-containers.md)  
  
  