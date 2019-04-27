---
title: Extensões do AdventureWorks para demonstrar o OLTP in-memory | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 0186b7f2-cead-4203-8360-b6890f37cde8
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7c2c7059c5c6ff6a770c1658d260da04f2a042ab
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62779941"
---
# <a name="extensions-to-adventureworks-to-demonstrate-in-memory-oltp"></a>Extensões do AdventureWorks para demonstrar OLTP na memória
    
## <a name="overview"></a>Visão geral  
 Este exemplo apresenta o novo recurso [!INCLUDE[hek_2](../includes/hek-2-md.md)] , que faz parte do [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]. Ele mostra as novas tabelas com otimização de memória e os procedimentos armazenados compilados nativamente, e pode ser usado para demonstrar os benefícios de desempenho do [!INCLUDE[hek_2](../includes/hek-2-md.md)].  
  
> [!NOTE]  
>  Para exibir esse tópico para o SQL Server 2016, consulte [Extensões do AdventureWorks para demonstrar OLTP na memória](https://msdn.microsoft.com/library/mt465764.aspx)  
  
 O exemplo a seguir migra 5 tabelas do banco de dados do AdventureWorks para a otimização de memória, e inclui uma carga de trabalho de demonstração para o processamento de pedidos de vendas. Você pode usar essa carga de trabalho de demonstração para consultar o benefício de desempenho em usar [!INCLUDE[hek_2](../includes/hek-2-md.md)] no servidor.  
  
 Na descrição do exemplo, abordamos as compensações que foram feitas na migração das tabelas para o [!INCLUDE[hek_2](../includes/hek-2-md.md)] , para levar em consideração os recursos que (ainda) não têm suporte para tabelas com otimização de memória no [!INCLUDE[ssSQL14](../includes/sssql14-md.md)].  
  
 A documentação do exemplo foi estruturada como segue:  
  
-   [Pré-requisitos](#Prerequisites) para instalar o exemplo e executar a carga de trabalho de demonstração  
  
-   Instruções para [Instalando a amostra OLTP In-Memory com base no AdventureWorks](#InstallingtheIn-MemoryOLTPsamplebasedonAdventureWorks)  
  
-   [Descrição das tabelas de exemplo e procedimentos](#Descriptionofthesampletablesandprocedures) -isso inclui descrições das tabelas e dos procedimentos adicionados ao AdventureWorks pelo [!INCLUDE[hek_2](../includes/hek-2-md.md)] exemplo, bem como considerações para migrar algumas das original AdventureWorks tabelas para otimização de memória  
  
-   Instruções para executar [Medidas de desempenho usando a carga de trabalho de demonstração](#PerformanceMeasurementsusingtheDemoWorkload) – inclui instruções para instalar e executar ostress, uma ferramenta usada para direcionar a carga de trabalho, bem como executar a própria carga de trabalho de demonstração  
  
-   [Utilização de memória e espaço em disco na amostra](#MemoryandDiskSpaceUtilizationintheSample)  
  
##  <a name="Prerequisites"></a> Pré-requisitos  
  
-   [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] RTM – edição Evaluation, Developer ou Enterprise  
  
-   Para testes de desempenho, um servidor com as especificações semelhantes ao ambiente de produção. Para este exemplo específico, você deve ter pelo menos 16 GB de memória disponível para o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Para obter diretrizes gerais sobre hardware para [!INCLUDE[hek_2](../includes/hek-2-md.md)], consulte postagem de blog a seguir:[http://blogs.technet.com/b/dataplatforminsider/archive/2013/08/01/hardware-considerations-for-in-memory-oltp-in-sql-server-2014.aspx](http://blogs.technet.com/b/dataplatforminsider/archive/2013/08/01/hardware-considerations-for-in-memory-oltp-in-sql-server-2014.aspx)  
  
##  <a name="InstallingtheIn-MemoryOLTPsamplebasedonAdventureWorks"></a> Instalando a amostra do [!INCLUDE[hek_2](../includes/hek-2-md.md)] baseada no AdventureWorks  
 Siga estas etapas para instalar o exemplo:  
  
1.  Baixe o arquivo morto do backup completo do banco de dados AdventureWorks2014:  
  
    1.  Abra o seguinte: [ http://msftdbprodsamples.codeplex.com/downloads/get/880661 ](http://msftdbprodsamples.codeplex.com/downloads/get/880661).  
  
    2.  Quando for solicitado salvar o arquivo em uma pasta local.  
  
2.  Extraia o arquivo **AdventureWorks2014.bak** para uma pasta local, por exemplo "c:\temp".  
  
3.  Restaure o backup de banco de dados usando o [!INCLUDE[tsql](../includes/tsql-md.md)] ou o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]:  
  
    1.  Identifique a pasta de destino e o nome de arquivo para o arquivo de dados, por exemplo,  
  
         'h:\DATA\AdventureWorks2014_Data.mdf'  
  
    2.  Identifique a pasta de destino e o nome de arquivo para o arquivo de log, por exemplo,  
  
         'i:\DATA\AdventureWorks2014_log.ldf'  
  
        1.  O arquivo de log deve ser colocado em uma unidade que não seja a do arquivo de dados, preferencialmente uma unidade de baixa latência como um armazenamento de SSD ou de PCIe, para obter o desempenho máximo.  
  
     Exemplo de script T-SQL:  
  
    ```  
    RESTORE DATABASE [AdventureWorks2014]   
      FROM DISK = N'C:\temp\AdventureWorks2014.bak'   
        WITH FILE = 1,    
      MOVE N'AdventureWorks2014_Data' TO N'h:\DATA\AdventureWorks2014_Data.mdf',    
      MOVE N'AdventureWorks2014_Log' TO N'i:\DATA\AdventureWorks2014_log.ldf'  
     GO  
    ```  
  
4.  Altere o proprietário do banco de dados para um logon no servidor, executando o seguinte comando na janela de consulta do [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]:  
  
    ```  
    ALTER AUTHORIZATION ON DATABASE::AdventureWorks2014 TO [<NewLogin>]  
    ```  
  
5.  Baixe o script de exemplo '[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] RTM [!INCLUDE[hek_2](../includes/hek-2-md.md)] Sample. SQL ' de [exemplo SQL Server 2014 RTM In-Memory OLTP](https://go.microsoft.com/fwlink/?LinkID=396372) em uma pasta local.  
  
6.  Atualize o valor da variável 'checkpoint_files_location' no script '[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] RTM [!INCLUDE[hek_2](../includes/hek-2-md.md)] Sample. SQL ', para apontar para o local de destino para o [!INCLUDE[hek_2](../includes/hek-2-md.md)] arquivos de ponto de verificação. Os arquivos de ponto de verificação devem ser colocados em uma unidade com bom desempenho sequencial de E/S.  
  
     Atualize o nome da variável 'database_name' para apontar para o banco de dados do AdventureWorks2014.  
  
    1.  Certifique-se de incluir a barra invertida '\' como parte do nome do caminho  
  
    2.  Exemplo:  
  
        ```  
        :setvar checkpoint_files_location "d:\DBData\"  
        ...  
        :setvar database_name "AdventureWorks2014"  
        ```  
  
7.  Execute o script de exemplo de uma destas duas maneiras:  
  
    1.  Usando o utilitário de linha de comando sqlcmd. Por exemplo, ao executar o seguinte comando do prompt de linha de comando na pasta que contém o script:  
  
        ```  
        sqlcmd -S . -E -i "ssSQL14 RTM hek_2 Sample.sql"  
        ```  
  
    2.  Usando o Management Studio:  
  
        1.  Abra o script '[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] RTM [!INCLUDE[hek_2](../includes/hek-2-md.md)] Sample. SQL ' em uma janela de consulta  
  
        2.  Conecte-se ao servidor de destino que contém o banco de dados AdventureWorks2014  
  
        3.  Habilitar o modo SQLCMD, clicando em 'Consulta -> modo SQLCMD'  
  
        4.  Clique no botão 'Executar' para executar o script  
  
##  <a name="Descriptionofthesampletablesandprocedures"></a> Descrição das tabelas e procedimentos de exemplo  
 O exemplo cria novas tabelas para produtos e pedidos de vendas, com base em tabelas existentes no AdventureWorks. O esquema das novas tabelas é semelhante às tabelas existentes, com algumas diferenças, conforme explicado a seguir.  
  
 As novas tabelas com otimização de memória têm o sufixo "_inmem". O exemplo também inclui as tabelas correspondentes que têm o sufixo "_ondisk" – essas tabelas podem ser usadas para fazer uma comparação um-para-um entre o desempenho de tabelas com otimização de memória e tabelas baseadas em disco em seu sistema.  
  
 Observe que as tabelas com otimização de memória usadas na carga de trabalho para a comparação de desempenho são totalmente duráveis e registradas. Elas não sacrificam a durabilidade ou a confiabilidade para ter o ganho de desempenho.  
  
 A carga de trabalho de destino para esse exemplo é o processamento de pedidos de vendas, onde também consideramos informações sobre produtos e descontos. Com esse fim, a tabela SalesOrderHeader, SalesOrderDetail, Product, SpecialOffer e SpecialOfferProduct.  
  
 Dois novos procedimentos armazenados, Sales.usp_InsertSalesOrder_inmem e Sales.usp_UpdateSalesOrderShipInfo_inmem, são usados para inserir pedidos de vendas e atualizar as informações de envio de um pedido de vendas específico.  
  
 O novo esquema 'Demonstração' contém tabelas e procedimentos armazenados auxiliares para executar uma carga de trabalho de demonstração.  
  
 Concretamente, o exemplo de [!INCLUDE[hek_2](../includes/hek-2-md.md)] adiciona os seguintes objetos ao AdventureWorks:  
  
### <a name="tables-added-by-the-sample"></a>Tabelas adicionadas pelo exemplo  
  
#### <a name="the-new-tables"></a>As novas tabelas  
 Sales.SalesOrderHeader_inmem  
  
-   Informações de cabeçalho sobre os pedidos de vendas. Cada pedido de vendas tem uma linha nesta tabela.  
  
 Sales.SalesOrderDetail_inmem  
  
-   Detalhes dos pedidos de vendas. Cada item de linha de um pedido de vendas tem uma linha nesta tabela.  
  
 Sales.SpecialOffer_inmem  
  
-   Informações sobre as ofertas especiais, incluindo o percentual de desconto associado a cada oferta especial.  
  
 Sales.SpecialOfferProduct_inmem  
  
-   Tabela de referência entre ofertas especiais e produtos. Cada oferta especial pode caracterizar zero ou mais produtos, e cada produto pode ser caracterizado em zero ou mais ofertas especiais.  
  
 Production.Product_inmem  
  
-   Informações sobre os produtos, inclusive o preço da lista.  
  
 Demo.DemoSalesOrderDetailSeed  
  
-   Usado na carga de trabalho de demonstração para criar exemplos de pedidos de vendas.  
  
 Variações das tabelas baseadas em disco:  
  
-   Sales.SalesOrderHeader_ondisk  
  
-   Sales.SalesOrderDetail_ondisk  
  
-   Sales.SpecialOffer_ondisk  
  
-   Sales.SpecialOfferProduct_ondisk  
  
-   Production.Product_ondisk  
  
#### <a name="differences-between-original-disk-based-and-the-and-new-memory-optimized-tables"></a>Diferenças entre as tabelas originais baseadas em disco e as novas tabelas com otimização de memória  
 Geralmente, as novas tabelas apresentadas por este exemplo usam as mesmas colunas e os mesmos tipos de dados que as tabelas originais. No entanto, há algumas diferenças. Listamos as diferenças abaixo, junto com uma razão para as alterações.  
  
 Sales.SalesOrderHeader_inmem  
  
-   *Restrições padrão* têm suporte para tabelas com otimização de memória, e migramos a maioria das restrições padrão como tal. No entanto, a tabela Sales.SalesOrderHeader original contém duas restrições padrão que recuperam a data atual, pata as colunas OrderDate e ModifiedDate. Em uma carga de trabalho de processamento de pedidos com alta taxa de transferência e muita simultaneidade, qualquer recurso global pode se tornar um ponto de contenção. O tempo do sistema é um recurso bem global, e observamos que ele pode se tornar um gargalo quando você executa uma carga de trabalho de [!INCLUDE[hek_2](../includes/hek-2-md.md)] que insere pedidos de vendas, em particular se o tempo do sistema precisa ser recuperado para várias colunas no cabeçalho do pedido de vendas, bem como os detalhes do pedido de vendas. O problema é tratado neste exemplo através da recuperação do tempo do sistema apenas uma vez para cada pedido de vendas que é inserido, e o uso desse valor para as colunas de data e hora em SalesOrderHeader_inmem e em SalesOrderDetail_inmem, no procedimento armazenado Sales.usp_InsertSalesOrder_inmem.  
  
-   *UDTs de alias* - a tabela original usa dois alias de tipos de dados definidos pelo usuário (UDTs), dbo.OrderNumber e dbo.AccountNumber, para as colunas PurchaseOrderNumber e AccountNumber, respectivamente. O[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] não dá suporte ao UDT de alias para tabelas com otimização de memória; portanto, as novas tabelas usam os tipos de dados do sistema nvarchar(25) e nvarchar(15), respectivamente.  
  
-   *Colunas que permitem valor nulo em chaves de índice* - na tabela original, a coluna SalesPersonID é anulável, enquanto em novas tabelas a coluna não é anulável e tem uma restrição padrão com valor (-1). Isso ocorre porque os índices nas tabelas com otimização de memória não podem ter colunas anuláveis na chave do índice; -1 é um substituto de NULL nesse caso.  
  
-   *Colunas computadas* - as colunas computadas SalesOrderNumber e TotalDue são omitidas, pois o [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] não oferece suporte a colunas computadas em tabelas com otimização de memória. A nova exibição Sales.vSalesOrderHeader_extended_inmem reflete as colunas SalesOrderNumber e TotalDue. Por disso, você pode usar essa exibição se essas colunas são necessárias.  
  
-   As*restrições de chave estrangeira* não têm suporte para tabelas com otimização de memória no [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]. Além disso, SalesOrderHeader_inmem é uma tabela ativa na carga de trabalho de exemplo, e as restrições de chaves estrangeiras exigem processamento adicional para todas as operações DML, pois são necessárias pesquisas em todas as outras tabelas referenciadas nessas restrições. Consequentemente, a suposição é a de que o aplicativo garante a integridade referencial, e a integridade referencial não é validada quando linhas são inseridas. A integridade referencial dos dados nessa tabela pode ser verificada usando o procedimento armazenado dbo.usp_ValidateIntegrity, através do seguinte script:  
  
    ```  
    DECLARE @o int = object_id(N'Sales.SalesOrderHeader_inmem')  
    EXEC dbo.usp_ValidateIntegrity @o  
    ```  
  
-   As*restrições check* não têm suporte para tabelas com otimização de memória no SQ Server 2014. A integridade de domínio é validada junto com a integridade referencial usando esse script:  
  
    ```  
    DECLARE @o int = object_id(N'Sales.SalesOrderHeader_inmem')  
    EXEC dbo.usp_ValidateIntegrity @o  
    ```  
  
-   *Rowguid* - a coluna rowguid é omitida. Apesar de uniqueidentifier ter suporte para tabelas com otimização de memória, a opção ROWGUIDCOL não tem suporte no [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]. As colunas desse tipo são geralmente usadas para a replicação de mesclagem ou para tabelas com colunas filestream. Este exemplo não inclui isso.  
  
 Sales.SalesOrderDetail  
  
-   *Restrições padrão* – semelhante ao SalesOrderHeader, a restrição padrão que requer a data/hora do sistema não é migrada; o procedimento armazenado que insere os pedidos de vendas fica responsável por inserir a data/hora atual do sistema na primeira inserção.  
  
-   *Colunas computadas* – a coluna computada LineTotal não foi migrada pois colunas computadas não são compatíveis com tabelas com otimização de memória no [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]. Para acessar essa coluna, use a exibição Sales.vSalesOrderDetail_extended_inmem.  
  
-   *Rowguid* - a coluna rowguid é omitida. Para obter detalhes, consulte a descrição da tabela SalesOrderHeader.  
  
-   Para as restrições de *verificação* e *chave estrangeira* , consulte a descrição de SalesOrderHeader. O seguinte script pode ser usado para verificar o domínio e a integridade referencial dessa tabela:  
  
    ```  
    DECLARE @o int = object_id(N'Sales.SalesOrderHeader_inmem')  
    EXEC dbo.usp_ValidateIntegrity @o  
    ```  
  
 Production.Product  
  
-   *UDTs de alias* – a tabela original usa tipo de dados definidos pelo usuário dbo.Flag, que equivalem ao tipo de dados bit do sistema. A tabela migrada usa o tipo de dados bit.  
  
-   *Agrupamento BIN2* -as colunas Name e ProductNumber são incluídas em chaves de índice e devem ter agrupamentos BIN2 no [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]. Aqui, a suposição é a de que o aplicativo não se baseia em especificações de ordenação, como a não diferenciação de maiúsculas e minúsculas.  
  
-   *Rowguid* - a coluna rowguid é omitida. Para obter detalhes, consulte a descrição da tabela SalesOrderHeader.  
  
-   As restrições*Unique*, *Check* e *Foreign Key* are accounted for in two ways: the stored procedures Product.usp_InsertProduct_inmem e Product.usp_DeleteProduct_inmem can be used to insert e delete products; these procedures validate domain e referential integrity, e will fail if integrity is violated. Além disso, o seguinte script pode ser usado para validar o domínio e a integridade referencial como tal:  
  
    ```  
    DECLARE @o int = object_id(N'Production.Product')  
    EXEC dbo.usp_ValidateIntegrity @o  
    ```  
  
    -   Observe que os procedimentos armazenados usp_InsertProduct_inmem e usp_DeleteProduct_inmem consideram apenas chaves estrangeiras entre as tabelas migradas. As referências a outras tabelas ProductModel, ProductSubcategory e UnitMeasure não são consideradas.  
  
 Sales.SpecialOffer  
  
-   As restrições*Check* e *Foreign Key* are accounted for in two ways: the stored procedures Sales.usp_InsertSpecialOffer_inmem e Sales.usp_DeleteSpecialOffer_inmem can be used to insert e delete special offers; these procedures validate domain e referential integrity, e will fail if integrity is violated. Além disso, o seguinte script pode ser usado para validar o domínio e a integridade referencial como tal:  
  
    ```  
    DECLARE @o int = object_id(N'Sales.SpecialOffer_inmem')  
    EXEC dbo.usp_ValidateIntegrity @o  
    ```  
  
-   *Rowguid* - a coluna rowguid é omitida. Para obter detalhes, consulte a descrição da tabela SalesOrderHeader.  
  
 Sales.SpecialOfferProduct  
  
-   As restrições*Foreign Key* são tratadas de duas maneiras: o procedimento armazenado Sales.usp_InsertSpecialOfferProduct_inmem pode ser usado para inserir relações entre ofertas especiais e produtos; esse procedimento valida a integridade referencial, e falhará se a integridade for violada. Além disso, o seguinte script pode ser usado para validar a integridade referencial como tal:  
  
    ```  
    DECLARE @o int = object_id(N'Sales.SpecialOfferProduct_inmem')  
    EXEC dbo.usp_ValidateIntegrity @o  
    ```  
  
-   *Rowguid* - a coluna rowguid é omitida. Para obter detalhes, consulte a descrição da tabela SalesOrderHeader.  
  
#### <a name="considerations-for-indexes-on-memory-optimized-tables"></a>Considerações para índices em tabelas com otimização de memória  
 O índice de linha de base para tabelas com otimização de memória é o índice NONCLUSTERED, que dá suporte a pesquisas de ponto (busca de índice em predicado de igualdade), exames de intervalo (busca de índice em predicado de desigualdade), verificações de índice completo e exames ordenados. Além disso, os índices NONCLUSTERED dão suporte à pesquisa nas colunas principais da chave de índice. De fato, os índices NONCLUSTERED com otimização de memória dão suporte a todas as operações com o suporte de índices NONCLUSTERED baseados em disco, exceto apenas para verificações regressivas. Portanto, o uso de índices NONCLUSTERED é uma opção confiável para seus índices.  
  
 Os índices de HASH podem ser usados para otimizar mais a carga de trabalho. Eles são particularmente otimizados para pesquisas de ponto e inserções de linhas. No entanto, lembre-se de que eles não dão suporte a exames de intervalo, exames ordenados ou pesquisas nas colunas de chave de índice. Consequentemente, tome cuidado ao usar esses índices. Além disso, é necessário especificar o bucket_count na hora da criação. Normalmente, ele deve ser definido entre uma e duas vezes o número de valores de chave de índice, mas valores superestimados não costumam ser um problema.  
  
 Consulte os Manuais Online para obter mais detalhes sobre [diretrizes de índice](https://technet.microsoft.com/library/dn133166\(v=sql.120\).aspx) e diretrizes para [escolher o bucket_count certo](https://technet.microsoft.com/library/dn494956\(v=sql.120\).aspx).  
  
 Os índices nas tabelas migradas foram ajustados para a carga de trabalho de processamento de pedidos de vendas de demonstração. A carga de trabalho se baseia em inserções e pesquisas de ponto nas tabelas Sales.SalesOrderHeader_inmem e Sales.SalesOrderDetail_inmem, e ela também se baseia em pesquisas de ponto nas colunas de chave primária nas tabelas Production.Product_inmem e Sales.SpecialOffer_inmem.  
  
 Sales.SalesOrderHeader_inmem tem três índices, que são todos os índices de HASH por motivos de desempenho, e porque exames ordenados ou de intervalo não são necessários para a carga de trabalho.  
  
-   Índice de HASH em (SalesOrderID): o bucket_count é dimensionado em 10 milhões (arredondado para 16 milhões), pois o número esperado de pedidos de vendas é de 10 milhões  
  
-   Índice de HASH em (SalesPersonID): o bucket_count é de 1 milhão. O conjunto de dados fornecido não tem muitos vendedores, mas permite futuro crescimento; além disso, não haverá uma penalidade de desempenho por pesquisas de ponto se o bucket_count for superdimensionado.  
  
-   Índice de HASH em (CustomerID): o bucket_count é de 1 milhão. O conjunto de dados fornecido não tem muitos clientes, mas permite futuro crescimento.  
  
 Sales.SalesOrderDetail_inmem tem três índices, que são todos os índices de HASH por motivos de desempenho, e porque exames ordenados ou de intervalo não são necessários para a carga de trabalho.  
  
-   Índice de HASH em (SalesOrderID, SalesOrderDetailID): esse é o índice de chave primária e, apesar de as pesquisas em (SalesOrderID, SalesOrderDetailID) serem raras, o uso de um índice de hash para a chave acelera as inserções de linhas. O bucket_count é dimensionado em 50 milhões (arredondado para 67 milhões): o número esperado de pedidos de vendas é de 10 milhões, e esse valor é dimensionado para ter uma média de 5 itens por pedido  
  
-   Índice de HASH em (SalesOrderID): as pesquisas por pedido de vendas são frequentes: você desejará localizar todos os itens de linha que correspondem a um único pedido.  O bucket_count é dimensionado em 10 milhões (arredondado para 16 milhões), pois o número esperado de pedidos de vendas é de 10 milhões  
  
-   Índice de HASH em (ProductID): o bucket_count é de 1 milhão. O conjunto de dados fornecido não tem muitos produtos, mas permite futuro crescimento.  
  
 Production.Product_inmem tem três índices  
  
-   Índice de HASH em (ProductID): as pesquisas em ProductID estão no caminho crítico para a carga de trabalho de demonstração; então, este é um índice de hash  
  
-   Índice NONCLUSTERED em (Name): isso permitirá exames ordenados de nomes de produtos  
  
-   Índice NONCLUSTERED em (ProductNumber): isso permitirá exames ordenados de números de produtos  
  
 Sales.SpecialOffer_inmem tem um índice de HASH em (SpecialOfferID): as pesquisas de ponto de ofertas especiais estão na parte essencial da carga de trabalho de demonstração. O bucket_count é dimensionado em 1 milhão para permitir futuro crescimento.  
  
 Sales.SpecialOfferProduct_inmem não é referenciado na carga de trabalho de demonstração e, assim, não há necessidade aparente de usar índices de hash nessa tabela para otimizar a carga de trabalho – os índices em (SpecialOfferID, ProductID) e (ProductID) são NONCLUSTERED.  
  
 Observe que, no exemplo anterior, alguns bucket_counts estão superdimensionados, mas não os bucket_counts para os índices em SalesOrderHeader_inmem e SalesOrderDetail_inmem: eles são dimensionados para apenas 10 milhões de pedidos de vendas. Isso visa permitir a instalação do exemplo em sistemas com baixa disponibilidade de memória, embora nesses casos a carga de trabalho de demonstração falhe quando a memória é insuficiente. Se você quiser dimensionar além de 10 milhões de pedidos de vendas, sinta-se à vontade para aumentar o número de buckets de forma correspondente.  
  
#### <a name="considerations-for-memory-utilization"></a>Considerações sobre a utilização de memória  
 A utilização de memória no banco de dados de exemplo, antes e após executar a carga de trabalho de demonstração, é abordada na seção [Utilização de memória para as tabelas com otimização de memória](#Memoryutilizationforthememory-optimizedtables).  
  
### <a name="stored-procedures-added-by-the-sample"></a>Procedimentos armazenados adicionados pelo exemplo  
 Os dois principais procedimentos armazenados para inserir o pedido de vendas e atualizar detalhes do envio são os seguintes:  
  
-   Sales.usp_InsertSalesOrder_inmem  
  
    -   Insere um novo pedido de vendas no banco de dados e gera o SalesOrderID para esse pedido. Como os parâmetros de entrada, ele requer detalhes no cabeçalho do pedido de vendas, bem como os itens de linha no pedido  
  
    -   Parâmetro de saída:  
  
        -   @SalesOrderID int – a SalesOrderID do pedido de venda recém-inserido  
  
    -   Parâmetros de entrada (obrigatório):  
  
        -   @DueDate datetime2  
  
        -   @CustomerID int  
  
        -   @BillToAddressID [int]  
  
        -   @ShipToAddressID [int]  
  
        -   @ShipMethodID [int]  
  
        -   @SalesOrderDetails Sales.SalesOrderDetailType_inmem – TVP que contém os itens de linha do pedido  
  
    -   Parâmetros de entrada (opcional):  
  
        -   @Status [tinyint]  
  
        -   @OnlineOrderFlag [bit]  
  
        -   @PurchaseOrderNumber [nvarchar](25\)  
  
        -   @AccountNumber [nvarchar](15\)  
  
        -   @SalesPersonID [int]  
  
        -   @TerritoryID [int]  
  
        -   @CreditCardID [int]  
  
        -   @CreditCardApprovalCode [varchar](15\)  
  
        -   @CurrencyRateID [int]  
  
        -   @Comment nvarchar(128)  
  
-   Sales.usp_UpdateSalesOrderShipInfo_inmem  
  
    -   Atualize as informações de envio de um pedido de vendas específico. Isso também atualizará as informações de envio para todos os itens de linha do pedido de vendas.  
  
    -   Este é um procedimento de wrapper para os procedimentos armazenados compilados nativamente Sales.usp_UpdateSalesOrderShipInfo_native, com a lógica de repetição para lidar com conflitos em potencial (inesperados) em transações simultâneas que atualizam o mesmo pedido. Para obter mais informações sobre a lógica de repetição, consulte o tópico dos Manuais Online [aqui](https://technet.microsoft.com/library/dn169141\(v=sql.120\).aspx).  
  
-   Sales.usp_UpdateSalesOrderShipInfo_native  
  
    -   Este é o procedimento armazenado compilado nativamente que efetivamente processa a atualização das informações de envio. Ele é o meio a ser chamado do procedimento armazenado de wrapper Sales.usp_UpdateSalesOrderShipInfo_inmem. Se o cliente pode tratar as falhas e implementa a lógica de repetição, você pode chamar esse procedimento diretamente, e não usar o procedimento armazenado de wrapper.  
  
 O procedimento armazenado a seguir é usado para a carga de trabalho de demonstração.  
  
-   Demo.usp_DemoReset  
  
    -   Redefine a demonstração, esvaziando e repropagando as tabelas SalesOrderHeader e SalesOrderDetail.  
  
 Os procedimentos armazenados a seguir são usados para inserir e excluir das tabelas com otimização de memória para garantir o domínio e a integridade referencial.  
  
-   Production.usp_InsertProduct_inmem  
  
-   Production.usp_DeleteProduct_inmem  
  
-   Sales.usp_InsertSpecialOffer_inmem  
  
-   Sales.usp_DeleteSpecialOffer_inmem  
  
-   Sales.usp_InsertSpecialOfferProduct_inmem  
  
 Finalmente, o procedimento armazenado a seguir é usado para verificar o domínio e a integridade referencial.  
  
1.  dbo.usp_ValidateIntegrity  
  
    -   Parâmetro opcional: @object_id – ID do objeto para o qual validar a integridade  
  
    -   Esse procedimento depende das tabelas dbo.DomainIntegrity, dbo.ReferentialIntegrity e dbo.UniqueIntegrity para as regras de integridade que precisam ser verificadas – o exemplo popula essas tabelas com base na verificação, na chave estrangeira e nas restrições exclusivas que existem para as tabelas originais no banco de dados do AdventureWorks.  
  
    -   Ele se baseia nos procedimentos auxiliares dbo.usp_GenerateCKCheck auxiliares, dbo.usp_GenerateFKCheck e dbo.GenerateUQCheck para gerar o T-SQL necessário para executar as verificações de integridade.  
  
##  <a name="PerformanceMeasurementsusingtheDemoWorkload"></a> Medidas de desempenho usando a carga de trabalho de demonstração  
 Ostress é uma ferramenta de linha de comando que foi desenvolvida pela equipe de suporte do [!INCLUDE[msCoName](../includes/msconame-md.md)] CSS [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Essa ferramenta pode ser usada para executar consultas ou executar procedimentos armazenados em paralelo. Você pode configurar o número de threads para executar em paralelo determinada instrução T-SQL, e pode especificar quantas vezes a instrução deve ser executada neste thread; ostress girará os threads e executará a instrução em todos os threads em paralelo. Ao término da execução de todos os threads, ostress relatará quanto tempo levou para concluir a execução de todos os threads.  
  
### <a name="installing-ostress"></a>Instalando ostress  
 Ostress é instalada como parte dos utilitários de RML; não há instalação autônoma para ostress.  
  
 Etapas da instalação:  
  
1.  Baixe e execute o pacote de instalação do x64 para os utilitários do RML na seguinte página: [https://blogs.msdn.com/b/psssql/archive/2013/10/29/cumulative-update-2-to-the-rml-utilities-for-microsoft-sql-server-released.aspx](https://blogs.msdn.com/b/psssql/archive/2013/10/29/cumulative-update-2-to-the-rml-utilities-for-microsoft-sql-server-released.aspx)  
  
2.  Se houver uma caixa de diálogo indicando que alguns arquivos estão em uso, clique em "Continuar"  
  
### <a name="running-ostress"></a>Executando ostress  
 Ostress é executada do prompt de linha de comando. É mais conveniente executar a ferramenta do “Prompt Cmd RML”, que é instalado como parte dos utilitários de RML.  
  
 Para abrir o Prompt Cmd RML, siga estas instruções:  
  
 No Windows Server 2012 [R2] e no Windows 8 e 8.1, abra o menu iniciar clicando na tecla Windows e digite "rml". Clique em "RML Cmd Prompt", que estará na lista de resultados da pesquisa.  
  
 Verifique se o prompt de comando está localizado na pasta de instalação Utilitários de RML. Por exemplo:   
  
 ![](../../2014/database-engine/media/SQLServer2014RTMIn-MemoryOLTP01.jpg)  
  
 As opções de linha de comando para ostress podem ser vista simplesmente ao executar ostress.exe sem opções de linha de comando. As opções principais a serem consideradas para executar ostress com este exemplo são:  
  
-   -S nome da instância do [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] à qual se conectar  
  
-   -E use a autenticação do Windows para se conectar (padrão); Se você usar [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] autenticação, use as opções-u e -P para especificar o nome de usuário e senha, respectivamente  
  
-   -d nome do banco de dados; para este exemplo, AdventureWorks2014  
  
-   -Q a instrução T-SQL a ser executada  
  
-   -n número de conexões que processam cada arquivo de entrada/consulta  
  
-   -r o número de iterações para cada conexão para executar cada arquivo de entrada/consulta  
  
### <a name="demo-workload"></a>Carga de trabalho de demonstração  
 O procedimento armazenado principal usado na carga de trabalho de demonstração é Sales.usp_InsertSalesOrder_inmem/ondisk. O script a seguir cria um parâmetro com valor de tabela (TVP) com dados de exemplo, e chama o procedimento para inserir um pedido de vendas com 5 itens de linha.  
  
 A ferramenta ostress é usada para executar as chamadas de procedimento armazenado em paralelo, para simular os clientes que inserem pedidos de vendas simultaneamente.  
  
 Redefinir a demonstração após cada verificação de estresse executando o Demo.usp_DemoReset. Este procedimento exclui as linhas nas tabelas com otimização de memória, trunca as tabelas baseadas em disco e executa um ponto de verificação de banco de dados.  
  
 O seguinte script é executado simultaneamente para simular uma carga de trabalho de processamento de pedido de vendas:  
  
```  
DECLARE   
      @i int = 0,   
      @od Sales.SalesOrderDetailType_inmem,   
      @SalesOrderID int,   
      @DueDate datetime2 = sysdatetime(),   
      @CustomerID int = rand() * 8000,   
      @BillToAddressID int = rand() * 10000,   
      @ShipToAddressID int = rand() * 10000,   
      @ShipMethodID int = (rand() * 5) + 1;   
  
INSERT INTO @od   
SELECT OrderQty, ProductID, SpecialOfferID   
FROM Demo.DemoSalesOrderDetailSeed   
WHERE OrderID= cast((rand()*106) + 1 as int);   
  
WHILE (@i < 20)   
BEGIN;   
      EXEC Sales.usp_InsertSalesOrder_inmem @SalesOrderID OUTPUT, @DueDate, @CustomerID, @BillToAddressID, @ShipToAddressID, @ShipMethodID, @od;   
      SET @i += 1   
END  
  
```  
  
 Com esse script, cada pedido de exemplo criado é inserido 20 vezes, com 20 procedimentos armazenados executados em um loop WHILE. O loop é usado para considerar o fato de que o banco de dados é usado para criar o pedido de exemplo. Em ambientes de produção típicos, o aplicativo da camada intermediária criará o pedido de vendas a ser inserido.  
  
 O script anterior insere pedidos de vendas em tabelas com otimização de memória. O script para inserir pedidos de vendas em tabelas baseadas em disco é derivado substituindo as duas ocorrências de "_inmem" por "_ondisk".  
  
 Usaremos a ferramenta ostress para executar os scripts através de várias conexões simultâneas. Usaremos o parâmetro "-n" para controlar o número de conexões e o parâmetro "r" para controlar quantas vezes o script é executado em cada conexão.  
  
#### <a name="functional-validation-of-the-workload"></a>Validação funcional da carga de trabalho  
 Para verificar se tudo funciona, começaremos com um teste de exemplo, usando 10 conexões simultâneas e 5 iterações, inserindo um total de 10 * 5 \* 20 = 1000 pedidos de vendas.  
  
 Com o comando a seguir, supomos que a instância padrão é usada no computador local. Se você estiver usando uma instância nomeada ou um servidor remoto, altere o nome do servidor em conformidade, usando o parâmetro -S.  
  
 Insira 1000 pedidos de vendas em tabelas com otimização de memória, usando o seguinte comando no Prompt Cmd RML:  
  
 Clique no botão Copiar para copiar o comando, e cole-o no prompt de comando Utilitários de RML.  
  
```  
ostress.exe -n10 -r5 -S. -E -dAdventureWorks2014 -q -Q"DECLARE @i int = 0, @od Sales.SalesOrderDetailType_inmem, @SalesOrderID int, @DueDate datetime2 = sysdatetime(), @CustomerID int = rand() * 8000, @BillToAddressID int = rand() * 10000, @ShipToAddressID int = rand() * 10000, @ShipMethodID int = (rand() * 5) + 1; INSERT INTO @od SELECT OrderQty, ProductID, SpecialOfferID FROM Demo.DemoSalesOrderDetailSeed WHERE OrderID= cast((rand()*106) + 1 as int); while (@i < 20) begin; EXEC Sales.usp_InsertSalesOrder_inmem @SalesOrderID OUTPUT, @DueDate, @CustomerID, @BillToAddressID, @ShipToAddressID, @ShipMethodID, @od; set @i += 1 end"  
```  
  
 Se tudo funcionar conforme esperado, a janela de comando terá a aparência a seguir. Mensagens de erro não são esperadas.  
  
 ![](../../2014/database-engine/media/SQLServer2014RTMIn-MemoryOLTP02.jpg)  
  
 Valide que a carga de trabalho também funciona conforme esperado para tabelas baseadas em disco, executando o seguinte comando no Prompt Cmd RML:  
  
 Clique no botão Copiar para copiar o comando, e cole-o no prompt de comando Utilitários de RML.  
  
```  
ostress.exe -n10 -r5 -S. -E -dAdventureWorks2014 -q -Q"DECLARE @i int = 0, @od Sales.SalesOrderDetailType_ondisk, @SalesOrderID int, @DueDate datetime2 = sysdatetime(), @CustomerID int = rand() * 8000, @BillToAddressID int = rand() * 10000, @ShipToAddressID int = rand() * 10000, @ShipMethodID int = (rand() * 5) + 1; INSERT INTO @od SELECT OrderQty, ProductID, SpecialOfferID FROM Demo.DemoSalesOrderDetailSeed WHERE OrderID= cast((rand()*106) + 1 as int); while (@i < 20) begin; EXEC Sales.usp_InsertSalesOrder_ondisk @SalesOrderID OUTPUT, @DueDate, @CustomerID, @BillToAddressID, @ShipToAddressID, @ShipMethodID, @od; set @i += 1 end"  
```  
  
#### <a name="running-the-workload"></a>Executando a carga de trabalho  
 Para testar na escala, inserimos 10 milhões de pedidos de vendas, usando 100 conexões. Esse teste é executado de forma razoável em um servidor modesto (por exemplo, 8 núcleos físicos, 16 núcleos lógicos), e o armazenamento básico de SSD para o log. Se o teste não for bem-executado no hardware, verifique a seção [Solução de problemas em testes com execução lenta](#Troubleshootingslow-runningtests). Se desejar reduzir o nível de estresse nesse teste, diminua o número de conexões, alterando o parâmetro "-n". Por exemplo, para diminuir a contagem de conexões para 40, altere o parâmetro "-n100" para "-n40".  
  
 Como medida de desempenho da carga de trabalho, usamos o tempo decorrido conforme relatado por ostress.exe após executar a carga de trabalho.  
  
##### <a name="memory-optimized-tables"></a>Tabelas com otimização de memória  
 Começaremos executando a carga de trabalho em tabelas com otimização de memória. O comando a seguir abre 100 threads, cada um executado para 5.000 iterações.  Cada iteração insere 20 pedidos de vendas em transações separadas. Há 20 inserções por iteração para compensar o fato de que o banco de dados é usado para gerar os dados a serem inseridos. Isso gera um total de 20 * 5.000 \* 100 = 10.000.000 inserções de pedidos de vendas.  
  
 Abra o Prompt Cmd RML e execute o seguinte comando:  
  
 Clique no botão Copiar para copiar o comando, e cole-o no prompt de comando Utilitários de RML.  
  
```  
ostress.exe -n100 -r5000 -S. -E -dAdventureWorks2014 -q -Q"DECLARE @i int = 0, @od Sales.SalesOrderDetailType_inmem, @SalesOrderID int, @DueDate datetime2 = sysdatetime(), @CustomerID int = rand() * 8000, @BillToAddressID int = rand() * 10000, @ShipToAddressID int = rand() * 10000, @ShipMethodID int = (rand() * 5) + 1; INSERT INTO @od SELECT OrderQty, ProductID, SpecialOfferID FROM Demo.DemoSalesOrderDetailSeed WHERE OrderID= cast((rand()*106) + 1 as int); while (@i < 20) begin; EXEC Sales.usp_InsertSalesOrder_inmem @SalesOrderID OUTPUT, @DueDate, @CustomerID, @BillToAddressID, @ShipToAddressID, @ShipMethodID, @od; set @i += 1 end"  
```  
  
 Em um servidor de teste com um número total de 8 núcleos físicos (16 lógicos), isso levou 2 minutos e 5 segundos. Em um segundo servidor de teste com 24 núcleos físicos (48 lógicos), isso levou 1 minuto e 0 segundos.  
  
 Observe a utilização da CPU enquanto a carga de trabalho está em execução. Use, por exemplo, o gerenciador de tarefas. Você verá que quase 100% da CPU é utilizada. Se esse não é o caso, você tem um gargalo de E/S de log. Consulte também [Solução de problemas em testes com execução lenta](#Troubleshootingslow-runningtests).  
  
##### <a name="disk-based-tables"></a>Tabelas baseadas em disco  
 O comando a seguir executará a carga de trabalho em tabelas baseadas em disco. Observe que essa carga de trabalho pode demorar um pouco para ser executada, o que em grande parte se deve a uma contenção de trava no sistema. A tabela com otimização de memória é livre de travas e, assim, não tem esse problema.  
  
 Abra o Prompt Cmd RML e execute o seguinte comando:  
  
 Clique no botão Copiar para copiar o comando, e cole-o no prompt de comando Utilitários de RML.  
  
```  
ostress.exe -n100 -r5000 -S. -E -dAdventureWorks2014 -q -Q"DECLARE @i int = 0, @od Sales.SalesOrderDetailType_ondisk, @SalesOrderID int, @DueDate datetime2 = sysdatetime(), @CustomerID int = rand() * 8000, @BillToAddressID int = rand() * 10000, @ShipToAddressID int = rand() * 10000, @ShipMethodID int = (rand() * 5) + 1; INSERT INTO @od SELECT OrderQty, ProductID, SpecialOfferID FROM Demo.DemoSalesOrderDetailSeed WHERE OrderID= cast((rand()*106) + 1 as int); while (@i < 20) begin; EXEC Sales.usp_InsertSalesOrder_ondisk @SalesOrderID OUTPUT, @DueDate, @CustomerID, @BillToAddressID, @ShipToAddressID, @ShipMethodID, @od; set @i += 1 end"  
```  
  
 Em um servidor de teste com um número total de 8 núcleos físicos (16 lógicos), isso levou 41 minutos e 25 segundos. Em um segundo servidor de teste com 24 núcleos físicos (48 lógicos), isso levou 52 minutos e 16 segundos.  
  
 O fator principal na diferença de desempenho entre tabelas com otimização de memória e tabelas baseadas em disco nesse teste é o fato de que, ao usar tabelas baseadas em disco, o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] não pode fazer uso total da CPU. A razão é a contenção de trava: as transações simultâneas estão tentando gravar na mesma página de dados; as travas são usadas para garantir que somente uma transação de cada vez possa gravar em uma página. O mecanismo [!INCLUDE[hek_2](../includes/hek-2-md.md)] é livre de travas, e as linhas de dados não são organizadas em páginas. Portanto, as transações simultâneas não bloqueiam as inserções umas das outras, permitindo [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para uso total da CPU.  
  
 Você pode observar a utilização da CPU enquanto a carga de trabalho está em execução. Use, por exemplo, o gerenciador de tarefas. Note que, em tabelas baseadas em disco, a utilização da CPU é bem inferior a 100%. Em uma configuração de teste com 16 processadores lógicos, a utilização fica em torno de 24%.  
  
 Opcionalmente, você pode exibir o número de esperas de trava por segundo usando o Monitor de Desempenho, com o contador de desempenho "\SQL Server:Latches\Latch Waits/sec".  
  
#### <a name="resetting-the-demo"></a>Redefinindo a demonstração  
 Para redefinir a demonstração, abra o Prompt Cmd RML e execute o seguinte comando:  
  
```  
ostress.exe -S. -E -dAdventureWorks2014 -Q"EXEC Demo.usp_DemoReset"  
```  
  
 Dependendo do hardware, isso pode levar alguns minutos para ser executado.  
  
 Recomendamos uma redefinição após cada demonstração executada. Como essa carga de trabalho é somente de inserção, cada execução consumirá mais memória e, portanto, uma redefinição é necessária para evitar ficar sem memória. A quantidade de memória consumida após uma execução é discutida na seção [Utilização de memória após executar a carga de trabalho](#Memoryutilizationafterrunningtheworkload).  
  
###  <a name="Troubleshootingslow-runningtests"></a> Solução de problemas em testes com execução lenta  
 Os resultados de testes variam de acordo com o hardware, e também com o nível de simultaneidade usado na execução do teste. Alguns itens a serem pesquisados se os resultados não forem os esperados:  
  
-   Número de transações simultâneas: Ao executar a carga de trabalho em um único thread, o ganho de desempenho com [!INCLUDE[hek_2](../includes/hek-2-md.md)] provavelmente será menor que 2x. A contenção de trava se torna um grande problema apenas se há um nível alto de simultaneidade.  
  
-   Baixo número de núcleos disponíveis para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]: Isso significa que haverá um nível baixo de simultaneidade no sistema, como só podem haver tantos transações executadas simultaneamente quanto há núcleos disponíveis para o SQL.  
  
    -   Sintoma: se há alta utilização da CPU ao executar a carga de trabalho em tabelas baseadas em disco, isso significa não há muita contenção, apontando para uma falta de simultaneidade.  
  
-   Velocidade da unidade de log: Se a unidade de log não é possível acompanhar o nível de taxa de transferência da transação no sistema, a carga de trabalho se torna um gargalo na e/s de log. Embora o log seja mais eficiente com [!INCLUDE[hek_2](../includes/hek-2-md.md)], se a E/S de log é um gargalo, o ganho de desempenho potencial é limitado.  
  
    -   Sintoma: caso quase 100% da CPU seja utilizada ou apresentar um pico de uso ao executar a carga de trabalho em tabelas com otimização de memória, talvez exista um gargalo de E/S de log. Isso pode ser confirmado abrindo o Monitor de Recursos e examinando o comprimento da fila para a unidade de log.  
  
##  <a name="MemoryandDiskSpaceUtilizationintheSample"></a> Utilização de memória e espaço em disco na amostra  
 A seguir, descrevemos o que esperar em termos de utilização da memória e do espaço em disco para o banco de dados de exemplo. Também mostramos os resultados observados em um servidor de teste com 16 núcleos lógicos.  
  
###  <a name="Memoryutilizationforthememory-optimizedtables"></a> Utilização de memória para as tabelas com otimização de memória  
  
#### <a name="overall-utilization-of-the-database"></a>Utilização geral do banco de dados  
 A consulta a seguir pode ser usada para obter a utilização total de memória de [!INCLUDE[hek_2](../includes/hek-2-md.md)] no sistema.  
  
```  
SELECT type  
   , name  
, pages_kb/1024 AS pages_MB   
FROM sys.dm_os_memory_clerks WHERE type LIKE '%xtp%'  
```  
  
 Instantâneo logo após a criação do banco de dados:  
  
||||  
|-|-|-|  
|**type**|**name**|**pages_MB**|  
|MEMORYCLERK_XTP|Padrão|94|  
|MEMORYCLERK_XTP|DB_ID_5|877|  
|MEMORYCLERK_XTP|Padrão|0|  
|MEMORYCLERK_XTP|Padrão|0|  
  
 Os administradores de memória padrão contêm estruturas de memória do sistema e são relativamente pequenos. O administrador de memória do banco de dados de usuário, nesse caso o banco de dados com ID 5, tem cerca de 900MB.  
  
#### <a name="memory-utilization-per-table"></a>Utilização da memória por tabela  
 A seguinte consulta pode ser usada para fazer uma busca detalhada na utilização da memória das tabelas individuais e de seus índices:  
  
```  
SELECT object_name(t.object_id) AS [Table Name]  
     , memory_allocated_for_table_kb  
 , memory_allocated_for_indexes_kb  
FROM sys.dm_db_xtp_table_memory_stats dms JOIN sys.tables t   
ON dms.object_id=t.object_id  
WHERE t.type='U'  
```  
  
 O seguinte exemplo mostra os resultados dessa consulta para uma instalação atualizada do exemplo:  
  
||||  
|-|-|-|  
|**Nome da tabela**|**memory_allocated_for_table_kb**|**memory_allocated_for_indexes_kb**|  
|SpecialOfferProduct_inmem|64|3840|  
|DemoSalesOrderHeaderSeed|1984|5504|  
|SalesOrderDetail_inmem|15316|663552|  
|DemoSalesOrderDetailSeed|64|10432|  
|SpecialOffer_inmem|3|8192|  
|SalesOrderHeader_inmem|7168|147456|  
|Product_inmem|124|12352|  
  
 Como você pode ver as tabelas são pequenas: SalesOrderHeader_inmem tem cerca de 7MB e SalesOrderDetail_inmem possui cerca de 15MB.  
  
 O que chama a atenção aqui é o tamanho da memória alocada para índices, comparado ao tamanho dos dados da tabela. Isso ocorre porque os índices de hash no exemplo são dimensionados previamente para um tamanho maior de dados. Observe que os índices de hash têm um tamanho fixo e, assim, seu tamanho não aumentará conforme o tamanho dos dados na tabela.  
  
####  <a name="Memoryutilizationafterrunningtheworkload"></a> Utilização de memória após executar a carga de trabalho  
 Após a inserção de 10 milhões de pedidos de vendas, qualquer utilização de memória superior terá a seguinte aparência:  
  
```  
SELECT type  
, name  
, pages_kb/1024 AS pages_MB   
FROM sys.dm_os_memory_clerks WHERE type LIKE '%xtp%'  
```  
  
||||  
|-|-|-|  
|**type**|**name**|**pages_MB**|  
|MEMORYCLERK_XTP|Padrão|146|  
|MEMORYCLERK_XTP|DB_ID_5|7374|  
|MEMORYCLERK_XTP|Padrão|0|  
|MEMORYCLERK_XTP|Padrão|0|  
  
 Como você pode notar, o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] está usando um pouco menos de 8GB para as tabelas e os índices com otimização de memória no banco de dados de exemplo.  
  
 Verificando o uso detalhado de memória pela tabela após a execução de um exemplo:  
  
```  
SELECT object_name(t.object_id) AS [Table Name]  
     , memory_allocated_for_table_kb  
 , memory_allocated_for_indexes_kb  
FROM sys.dm_db_xtp_table_memory_stats dms JOIN sys.tables t   
ON dms.object_id=t.object_id  
WHERE t.type='U'  
```  
  
||||  
|-|-|-|  
|**Nome da tabela**|**memory_allocated_for_table_kb**|**memory_allocated_for_indexes_kb**|  
|SalesOrderDetail_inmem|5113761|663552|  
|DemoSalesOrderDetailSeed|64|10368|  
|SpecialOffer_inmem|2|8192|  
|SalesOrderHeader_inmem|1575679|147456|  
|Product_inmem|111|12032|  
|SpecialOfferProduct_inmem|64|3712|  
|DemoSalesOrderHeaderSeed|1984|5504|  
  
 Podemos ver um total de aproximadamente 6,5 GB de dados. Observe que o tamanho dos índices nas tabelas SalesOrderHeader_inmem e SalesOrderDetail_inmem equivale ao tamanho dos índices antes de inserir os pedidos de vendas. O tamanho do índice não foi alterado porque ambas as tabelas estão usando índices de hash, e os índices de hash são estáticos.  
  
#### <a name="after-demo-reset"></a>Após a redefinição de demonstração  
 O procedimento armazenado Demo.usp_DemoReset pode ser usado para redefinir a demonstração. Ele exclui os dados nas tabelas SalesOrderHeader_inmem e SalesOrderDetail_inmem, e repropaga os dados das tabelas originais SalesOrderHeader e SalesOrderDetail.  
  
 Agora, apesar de as linhas das tabelas terem sido excluídas, isso não significa que a memória é recuperada imediatamente. O [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] recupera a memória das linhas excluídas em tabelas com otimização de memória no plano de fundo, conforme necessário. Note que, imediatamente após a redefinição da demonstração, sem a carga de trabalho transacional no sistema, a memória das linhas excluídas ainda não foi recuperada:  
  
```  
SELECT type  
, name  
, pages_kb/1024 AS pages_MB   
FROM sys.dm_os_memory_clerks WHERE type LIKE '%xtp%'  
```  
  
||||  
|-|-|-|  
|**type**|**name**|**pages_MB**|  
|MEMORYCLERK_XTP|Padrão|2261|  
|MEMORYCLERK_XTP|DB_ID_5|7396|  
|MEMORYCLERK_XTP|Padrão|0|  
|MEMORYCLERK_XTP|Padrão|0|  
  
 Isso é esperado: a memória será recuperada quando a carga de trabalho transacional estiver em execução.  
  
 Se você iniciar uma segunda execução da carga de trabalho de demonstração, notará que inicialmente a utilização da memória diminui, pois as linhas excluídas anteriormente são limpadas. Em algum momento, o tamanho da memória aumentará novamente, até que a carga de trabalho seja concluída. Após inserir 10 milhões de linhas após a redefinição de demonstração, a utilização da memória será muito semelhante à utilização após a primeira execução. Por exemplo:  
  
```  
SELECT type  
, name  
, pages_kb/1024 AS pages_MB   
FROM sys.dm_os_memory_clerks WHERE type LIKE '%xtp%'  
```  
  
||||  
|-|-|-|  
|**type**|**name**|**pages_MB**|  
|MEMORYCLERK_XTP|Padrão|1863|  
|MEMORYCLERK_XTP|DB_ID_5|7390|  
|MEMORYCLERK_XTP|Padrão|0|  
|MEMORYCLERK_XTP|Padrão|0|  
  
### <a name="disk-utilization-for-memory-optimized-tables"></a>Utilização de disco para as tabelas com otimização de memória  
 O tamanho geral em disco para os arquivos de ponto de verificação de um banco de dados em determinado momento pode ser localizado usando a consulta:  
  
```  
SELECT SUM(df.size) * 8 / 1024 AS [On-disk size in MB]  
FROM sys.filegroups f JOIN sys.database_files df   
   ON f.data_space_id=df.data_space_id  
WHERE f.type=N'FX'  
  
```  
  
#### <a name="initial-state"></a>Estado inicial  
 Quando o grupo de arquivos de exemplo e as tabelas com otimização de memória de exemplo são criados inicialmente, um número de arquivos de ponto de verificação são pré-criados e o sistema começa a preencher os arquivos – o número de arquivos de ponto de verificação pré-criados depende do número de processadores lógicos no sistema. Como o exemplo é inicialmente muito pequeno, os arquivos pré-criados serão os mais vazios após a criação inicial.  
  
 O seguinte exemplo mostra o tamanho inicial em disco para o exemplo em um computador com 16 processadores lógicos:  
  
```  
SELECT SUM(df.size) * 8 / 1024 AS [On-disk size in MB]  
FROM sys.filegroups f JOIN sys.database_files df   
   ON f.data_space_id=df.data_space_id  
WHERE f.type=N'FX'  
```  
  
||  
|-|  
|**Tamanho em disco em MB**|  
|2312|  
  
 Como você pode observar, há uma discrepância grande entre o tamanho em disco dos arquivos de ponto de verificação, que é de 2,3 GB, e o tamanho real dos dados, que é em torno de 30 MB.  
  
 Levando em conta a origem da utilização do espaço em disco, você pode usar a seguinte consulta. O tamanho do disco retornado por esta consulta é aproximado para os arquivos com estado 5 (NECESSÁRIO PARA BACKUP/AD), 6 (EM TRANSIÇÃO PARA MARCA DE EXCLUSÃO) ou 7 (MARCA DE EXCLUSÃO).  
  
```  
SELECT state_desc  
 , file_type_desc  
 , COUNT(*) AS [count]  
 , SUM(CASE  
   WHEN state = 5 AND file_type=0 THEN 128*1024*1024  
   WHEN state = 5 AND file_type=1 THEN 8*1024*1024  
   WHEN state IN (6,7) THEN 68*1024*1024  
   ELSE file_size_in_bytes  
    END) / 1024 / 1024 AS [on-disk size MB]   
FROM sys.dm_db_xtp_checkpoint_files  
GROUP BY state, state_desc, file_type, file_type_desc  
ORDER BY state, file_type  
```  
  
 Para o estado inicial do exemplo, o resultado terá a seguinte aparência para um servidor com 16 processadores lógicos:  
  
|||||  
|-|-|-|-|  
|**state_desc**|**file_type_desc**|**contagem**|**tamanho em disco em MB**|  
|PRECREATED|DATA|16|2048|  
|PRECREATED|DELTA|16|128|  
|UNDER CONSTRUCTION|DATA|1|128|  
|UNDER CONSTRUCTION|DELTA|1|8|  
  
 Como você pode ver, a maior parte do espaço é usado por dados e arquivos delta criados anteriormente. O [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] criou previamente um par de arquivos (dados, delta) por processador lógico. Além disso, os arquivos de dados são dimensionados previamente em 128MB, e os arquivos delta em 8MB, para tornar a inserção de dados nesses arquivos mais eficiente.  
  
 Os dados reais nas tabelas com otimização de memória estão no único arquivo de dados.  
  
#### <a name="after-running-the-workload"></a>Após executar a carga de trabalho  
 Após a execução de um único teste que insere 10 milhões de pedidos de vendas, o tamanho geral em disco tem a seguinte aparência (para um servidor de teste com 16 núcleos):  
  
```  
SELECT SUM(df.size) * 8 / 1024 AS [On-disk size in MB]  
FROM sys.filegroups f JOIN sys.database_files df   
   ON f.data_space_id=df.data_space_id  
WHERE f.type=N'FX'  
```  
  
||  
|-|  
|**Tamanho em disco em MB**|  
|8828|  
  
 O tamanho em disco é em torno de 9GB, um valor próximo ao tamanho dos dados na memória.  
  
 Verificando melhor os tamanhos dos arquivos de ponto de verificação em vários estados:  
  
```  
SELECT state_desc  
 , file_type_desc  
 , COUNT(*) AS [count]  
 , SUM(CASE  
   WHEN state = 5 AND file_type=0 THEN 128*1024*1024  
   WHEN state = 5 AND file_type=1 THEN 8*1024*1024  
   WHEN state IN (6,7) THEN 68*1024*1024  
   ELSE file_size_in_bytes  
    END) / 1024 / 1024 AS [on-disk size MB]   
FROM sys.dm_db_xtp_checkpoint_files  
GROUP BY state, state_desc, file_type, file_type_desc  
ORDER BY state, file_type  
```  
  
|||||  
|-|-|-|-|  
|**state_desc**|**file_type_desc**|**contagem**|**tamanho em disco em MB**|  
|PRECREATED|DATA|16|2048|  
|PRECREATED|DELTA|16|128|  
|UNDER CONSTRUCTION|DATA|1|128|  
|UNDER CONSTRUCTION|DELTA|1|8|  
  
 Temos ainda 16 pares de arquivos pré-criados, prontos para uso pois os pontos de verificação estão fechados.  
  
 Há um par em construção, que é usado até que o ponto de verificação atual seja fechado. Junto com os arquivos de ponto de verificação ativos, isso representa em torno de 6,5 GB de utilização de disco para 6,5 GB de dados na memória. Lembre-se de que os índices não são mantidos em disco e, assim, o tamanho geral em disco é menor do que o tamanho da memória, nesse caso.  
  
#### <a name="after-demo-reset"></a>Após a redefinição de demonstração  
 Após a redefinição de demonstração, o espaço em disco não é recuperado imediatamente se não há carga de trabalho transacional no sistema, e não há pontos de verificação de banco de dados. Para que os arquivos de ponto de verificação sejam executados em suas várias fases e acabem sendo descartados, é necessário que ocorram alguns pontos de verificação e eventos de truncamento de log, a fim de iniciar a mesclagem de arquivos de pontos de verificação, bem como a coleta de lixo. Isso ocorrerá automaticamente se você tiver uma carga de trabalho transacional no sistema [e fizer backups de log regulares, caso você esteja usando o modelo de recuperação completa], mas não quando o sistema estiver ocioso, como em um cenário de demonstração.  
  
 No exemplo, após a redefinição de demonstração, você verá algo semelhante a  
  
```  
SELECT SUM(df.size) * 8 / 1024 AS [On-disk size in MB]  
FROM sys.filegroups f JOIN sys.database_files df   
   ON f.data_space_id=df.data_space_id  
WHERE f.type=N'FX'  
```  
  
||  
|-|  
|**Tamanho em disco em MB**|  
|11839|  
  
 Com quase 12GB, isso é significativamente mais do que os 9GB que tínhamos antes da redefinição de demonstração. Isso ocorre porque algumas mesclagens do arquivo de ponto de verificação foram iniciadas, mas alguns dos destinos de mesclagem ainda não foram instalados, e alguns dos arquivos de origem de mesclagem ainda não foram limpos, como podemos observar aqui:  
  
```  
SELECT state_desc  
 , file_type_desc  
 , COUNT(*) AS [count]  
 , SUM(CASE  
   WHEN state = 5 AND file_type=0 THEN 128*1024*1024  
   WHEN state = 5 AND file_type=1 THEN 8*1024*1024  
   WHEN state IN (6,7) THEN 68*1024*1024  
   ELSE file_size_in_bytes  
    END) / 1024 / 1024 AS [on-disk size MB]   
FROM sys.dm_db_xtp_checkpoint_files  
GROUP BY state, state_desc, file_type, file_type_desc  
ORDER BY state, file_type  
```  
  
|||||  
|-|-|-|-|  
|**state_desc**|**file_type_desc**|**contagem**|**tamanho em disco em MB**|  
|PRECREATED|DATA|16|2048|  
|PRECREATED|DELTA|16|128|  
|ACTIVE|DATA|38|5152|  
|ACTIVE|DELTA|38|1331|  
|MERGE TARGET|DATA|7|896|  
|MERGE TARGET|DELTA|7|56|  
|MERGED SOURCE|DATA|13|1772|  
|MERGED SOURCE|DELTA|13|455|  
  
 Os destinos de mesclagem serão instalados e a origem mesclada será limpa à medida que a atividade transacional ocorrer no sistema.  
  
 Após uma segunda execução da carga de trabalho de demonstração, inserindo 10 milhões de pedidos de vendas após a redefinição de demonstração, você verá que os arquivos criados durante a primeira execução da carga de trabalho foram limpos. Se você executar a consulta anterior várias vezes enquanto a carga de trabalho estiver em execução, verá que os arquivos de ponto de verificação passarão por várias fases.  
  
 Após a segunda execução da carga de trabalho inserir 10 milhões de pedidos de vendas, você notará que a utilização de disco é bem semelhante, embora não necessariamente igual, à da primeira execução, pois o sistema é dinâmico por natureza. Por exemplo:   
  
```  
SELECT state_desc  
 , file_type_desc  
 , COUNT(*) AS [count]  
 , SUM(CASE  
   WHEN state = 5 AND file_type=0 THEN 128*1024*1024  
   WHEN state = 5 AND file_type=1 THEN 8*1024*1024  
   WHEN state IN (6,7) THEN 68*1024*1024  
   ELSE file_size_in_bytes  
    END) / 1024 / 1024 AS [on-disk size MB]   
FROM sys.dm_db_xtp_checkpoint_files  
GROUP BY state, state_desc, file_type, file_type_desc  
ORDER BY state, file_type  
```  
  
|||||  
|-|-|-|-|  
|**state_desc**|**file_type_desc**|**contagem**|**tamanho em disco em MB**|  
|PRECREATED|DATA|16|2048|  
|PRECREATED|DELTA|16|128|  
|UNDER CONSTRUCTION|DATA|2|268|  
|UNDER CONSTRUCTION|DELTA|2|16|  
|ACTIVE|DATA|41|5608|  
|ACTIVE|DELTA|41|328|  
  
 Nesse caso, há dois pares de arquivos do ponto de verificação no estado "em construção", o que significa que vários pares de arquivos foram movidos para o estado "em construção", provavelmente devido ao nível alto de simultaneidade na carga de trabalho. Vários threads simultâneos exigiam um novo par de arquivos ao mesmo tempo e, portanto, moviam um par de "pré-criados" para "em construção".  
  
## <a name="see-also"></a>Consulte também  
 [OLTP in-memory &#40;Otimização na memória&#41;](../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
